## Send Console Log

The plugin can send console logs to the server while fetching or publishing artifacts.

<p class='request-name-heading'>Request name</p>

`go.processor.artifact.console-log`

<p class='request-body-heading'>Request version</p>

The request version must be set to `1.0`.

<p class='request-name-heading'>Request body</p>

The request body must contain the logLevel and a message string. The logLevel must be `INFO` or `ERROR`.

> Example Request Body

```json
{
  "logLevel": "INFO",
  "message" : "This is an info message."
}
```

<p class='request-name-heading'>Response code</p>

The server is expected to return status `200` if it could process the request.

<p class='request-name-heading'>Response body</p>

The server will not send a response body.

> Console Logger Example

```java
import com.google.gson.Gson;
import com.thoughtworks.go.plugin.api.GoApplicationAccessor;
import com.thoughtworks.go.plugin.api.GoPluginIdentifier;
import com.thoughtworks.go.plugin.api.logging.Logger;
import com.thoughtworks.go.plugin.api.request.DefaultGoApiRequest;
import com.thoughtworks.go.plugin.api.response.DefaultGoApiResponse;
import com.thoughtworks.go.plugin.api.response.GoApiResponse;

import java.util.Collections;

public class ConsoleLogger {
    private static final String SEND_CONSOLE_LOG = "go.processor.artifact.console-log";
    private static final String API_VERSION = "1.0";
    private GoPluginIdentifier PLUGIN_IDENTIFIER = new GoPluginIdentifier("artifact", Collections.singletonList(API_VERSION));
    private static final Logger LOG = Logger.getLoggerFor(DockerRegistryArtifactPlugin.class);
    private static ConsoleLogger consoleLogger;
    private final GoApplicationAccessor accessor;

    private ConsoleLogger(GoApplicationAccessor accessor) {
        this.accessor = accessor;
    }

    public void info(String message) {
        sendLog(new ConsoleLogMessage(ConsoleLogMessage.LogLevel.INFO, message));
    }

    public void error(String message) {
        sendLog(new ConsoleLogMessage(ConsoleLogMessage.LogLevel.ERROR, message));
    }

    private void sendLog(ConsoleLogMessage consoleLogMessage) {
        DefaultGoApiRequest request = new DefaultGoApiRequest(SEND_CONSOLE_LOG, API_VERSION, PLUGIN_IDENTIFIER);
        request.setRequestBody(consoleLogMessage.toJSON());

        GoApiResponse response = accessor.submit(request);
        if (response.responseCode() != DefaultGoApiResponse.SUCCESS_RESPONSE_CODE) {
            LOG.error(String.format("Failed to submit console log: %s", response.responseBody()));
        }
    }

    public static ConsoleLogger getLogger(GoApplicationAccessor accessor) {
        if (consoleLogger == null) {
            synchronized (ConsoleLogger.class) {
                if (consoleLogger == null) {
                    consoleLogger = new ConsoleLogger(accessor);
                }
            }
        }

        return consoleLogger;
    }

    static class ConsoleLogMessage {
        private LogLevel logLevel;
        private String message;

        public ConsoleLogMessage(LogLevel logLevel, String message) {
            this.message = message;
            this.logLevel = logLevel;
        }

        public String toJSON() {
            return new Gson().toJson(this);
        }

        enum LogLevel {
            INFO, ERROR
        }
    }
}
```

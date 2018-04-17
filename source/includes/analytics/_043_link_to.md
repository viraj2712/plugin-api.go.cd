## go.cd.analytics.v1.link-to

Any links opened directly from the plugin's front-end will open inside the iframe. For security reasons, the iframe cannot affect the
navigation of the parent GoCD window directly. Instead, the iframe can send a message with the key `go.cd.analytics.v1.link-to` to the
parent window to link to one of a specific set of GoCD pages.

The version `v1` of the message supports linking to Job Details page and first Stage of a Pipeline Instance.

Upon receiving this message with correct parameters the parent window will open the linked pages in a new tab.

### Linking to: Job details page

> An example message from iframe to parent window to link to job details page -

```json
{
    "head": {
        "reqId": 1,
        "type": "request",
        "key": "go.cd.analytics.v1.link-to"
    },
    "body": {
        "link_to": "job_details_page",
        "pipeline_name": "my_pipeline",
        "pipeline_counter": 10,
        "stage_name": "my_stage",
        "stage_counter": 1,
        "job_name": "job1"
    }
}
```

> This will be the equivalent of opening a new tab with the URL: `http://ci.example.com/go/tab/build/detail/my_pipeline/10/my_stage/1/job1`.

The head object should contain:

| Key     | Description                              |
|---------|------------------------------------------|
| `reqId` | A unique request ID.                     |
| `type`  | Should be: `request`.                    |
| `key`   | Should be: `go.cd.analytics.v1.link-to`. |

The body object should contain these keys:

| Key                | Description                             |
|--------------------|-----------------------------------------|
| `link_to`          | The value should be `job_details_page`. |
| `pipeline_name`    | The name of the pipeline the job is in. |
| `pipeline_counter` | The counter of the pipeline.            |
| `stage_name`       | The stage name the job is in.           |
| `stage_counter`    | The stage counter.                      |
| `job_name`         | The name of the job.                    |


### Linking to: Pipeline Instance page

> An example message from iframe to parent window to link to pipeline instance page -

```json
{
    "head": {
        "reqId": 1,
        "type": "request",
        "key": "go.cd.analytics.v1.link-to"
    },
    "body": {
        "link_to": "pipeline_instance_page",
        "pipeline_name": "my_pipeline",
        "pipeline_counter": "10"
    }
}
```

> This will be the equivalent of opening a new tab with the URL: `http://ci.example.com/go/pipelines/my_pipeline/10/my_first_stage/1`.

The head object should contain:

| Key     | Description                              |
|---------|------------------------------------------|
| `reqId` | A unique request ID.                     |
| `type`  | Should be: `request`.                    |
| `key`   | Should be: `go.cd.analytics.v1.link-to`. |

The body object should contain these keys:

| Key                | Description                                   |
|--------------------|-----------------------------------------------|
| `link_to`          | The value should be `pipeline_instance_page`. |
| `pipeline_name`    | The name of the pipeline to link to.          |
| `pipeline_counter` | The counter of the pipeline.                  |

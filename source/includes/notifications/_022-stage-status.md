## Stage Status Changed

This message is sent by the server, when it wants to notify the plugin about a "stage status change". Some tips on stage status changes:

Stage status changed notifications only get sent when a stage gets scheduled or when it completes.

<p class='request-name-heading'>Request name</p>

`stage-status`

<p class='request-body-heading'>Request body for stage start notifications</p>

> A sample body when a stage with three jobs gets scheduled.

```json
{
  "pipeline": {
    "name": "pipeline-name",
    "counter": "9",
    "group": "defaultGroup",
    "build-cause": [
      {
        "material": {
          "git-configuration": {
            "shallow-clone": false,
            "branch": "2.x",
            "url": "https://github.com/organization/repository"
          },
          "type": "git"
        },
        "changed": false,
        "modifications": [
          {
            "revision": "8f60b12439840e5a0a4d464379dd3a48881008b4",
            "modified-time": "2017-03-23T17:27:58.000Z",
            "data": {}
          }
        ]
      }
    ],
    "stage": {
      "name": "stageOne",
      "counter": "1",
      "approval-type": "success",
      "approved-by": "timer",
      "state": "Building",
      "result": "Unknown",
      "create-time": "2017-03-23T20:44:02.119Z",
      "jobs": [
        {
          "name": "job1",
          "schedule-time": "2017-03-23T20:44:02.119Z",
          "state": "Scheduled",
          "result": "Unknown"
        },
        {
          "name": "job2",
          "schedule-time": "2017-03-23T20:44:02.119Z",
          "state": "Scheduled",
          "result": "Unknown"
        },
        {
          "name": "job3",
          "schedule-time": "2017-03-23T20:44:02.119Z",
          "state": "Scheduled",
          "result": "Unknown"
        }
      ]
    }
  }
}
```

The request body will contain a JSON representing the stage.

* A stage start notification can be identified by the `.pipeline.stage.state` attribute set to `'Building'`.

* For a stage with multiple jobs, `.pipeline.stage.jobs[].state` will at least be `'Scheduled'`.

* All jobs will be made available in JSON.

<p class='request-body-heading'>Request body for stage completion notifications</p>

> A sample body when a stage with one job completes successfully.

```json
{
  "pipeline": {
    "name": "pipeline-name",
    "counter": "1",
    "label": "pipeline-label",
    "group": "pipeline-group",
    "build-cause": [
      {
        "material": {
          "git-configuration": {
            "shallow-clone": false,
            "branch": "branch",
            "url": "http://user:******@gitrepo.com"
          },
          "type": "git"
        },
        "changed": true,
        "modifications": [
          {
            "revision": "1",
            "modified-time": "2016-04-06T12:50:03.317Z",
            "data": {}
          }
        ]
      }
    ],
    "stage": {
      "name": "stage-name",
      "counter": "1",
      "approval-type": "success",
      "approved-by": "changes",
      "state": "Passed",
      "result": "Passed",
      "create-time": "2011-07-13T19:43:37.100Z",
      "last-transition-time": "2011-07-13T19:43:39.100Z",
      "jobs": [
        {
          "name": "job-name",
          "schedule-time": "2011-07-13T19:43:37.100Z",
          "assign-time": "2011-07-13T19:43:38.100Z",
          "complete-time": "2011-07-13T19:43:39.100Z",
          "state": "Completed",
          "result": "Passed",
          "agent-uuid": "uuid"
        }
      ]
    }
  }
}
```

The request body will contain a JSON representing the stage.

* Stage completion notifications can be identified when the `.pipeline.stage.state` is something other than `'Building'`. Other valid values are `'Passed'`, `'Failed'` and `'Cancelled'`.

* For a completed stage with multiple jobs, `.pipeline.stage.jobs[].job_result` will at either `'Passed'`, `'Failed'` or `'Cancelled'`.

<p class='response-code-heading'>Response code</p>

The plugin is expected to return status `200` if it can understand the request.

<p class='response-body-heading'>Response Body</p>

> An example response body if the plugin could send the notification successfully

```json
{
  "status": "success"
}
```

> An example response body if the plugin could not send the notification

```json
{
  "status": "failure",
  "messages": ["Could not send email for build/1/compile/1"]
}
```

The plugin is expected to return a JSON object to indicate if the notifications could be processed.

<aside class="warning">
  <strong>Note</strong>: If plugin responds with error messages Go Server shows those in "server health messages".
</aside>

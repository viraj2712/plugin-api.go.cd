## go.cd.analytics.v1.link-to

The iframe can send a message with the key `go.cd.analytics.v1.link-to` to the parent window to link to a GoCD page. The version v1 of the message supports linking to Job Details page and first Stage of a Pipeline Instance.

Upon receiving this message with correct parameters the parent window would open the linked pages in a new tab. 


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


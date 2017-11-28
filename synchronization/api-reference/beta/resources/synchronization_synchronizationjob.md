# synchronizationJob resource type

Synchronization job performs synchronization by periodically running in the background, polling for changes in one directory and pushing them to another directory. Synchronization job is always specific to a particular instance of an application in your tenant. As part of the synchronization job setup, generally you would need to give authorization to read/write objects in your target directory, and customize job's synchronization schema to suit your needs.

## Methods

| Method        | Return Type               | Description                  |
|:--------------|:--------------------------|:-----------------------------|
|[List](../api/synchronization_list_jobs.md)             |[synchronizationJob](synchronization_synchronizationjob.md) collection  |List existing jobs for a given application instance (service principal).|
|[Get synchronizationJob](../api/synchronization_synchornizationjob_get.md) | [synchronizationJob](synchronization_synchronizationjob.md) |Read properties and relationships of synchronizationJob object.|
|[Create](../api/synchronization_post_jobs.md)         |[synchronizationJob](synchronization_synchronizationjob.md)   |Create new job for a given application.|
|[Start](../api/synchronization_synchronizationjob_start.md)          |None   |Start synchronization. If job is in paused state, it continues from the point where job was paused. If job is in quarantine, quarantine status is cleared.|
|[Restart](../api/synchronization_synchronizationjob_restart.md)      |None   |Force job to start from scratch and re-process all the objects in the directory.|
|[Pause](../api/synchronization_synchronizationjob_pause.md)          |None   |Temporarily stop synchronizaion. All the progress including job state is persisted, and upon [Start](../api/synchronization_synchronizationjob_start.md) call job execution will continue from where it left off.|
|[Delete](../api/synchronization_synchronizationjob_delete.md)        |None   |Stop synchronization, and permanently delete all the state associated with the job.|
|[Get synchrnoizationSchema](../api/synchronization_synchronizationschema_get.md)    |[synchronizationSchema](synchronization_synchronizationschema.md)   |Retreive job's effective synchronization schema.|
|[Update synchroizationSchema](../api/synchronization_synchronizationschema_put.md)    |None   |Updates job's synchronization schema. |
|[Validate credentials](../api/synchronization_synchronizationjob_validatecredentials.md)|None|Test provided credentials against target directory.|

## Properties

| Property      | Type      | Description    |
|:--------------|:----------|:---------------|
|id             |String                     |Unique synchronization job identifier. Read-only.|
|schedule       |[synchronizationSchedule](synchronizationschedule.md)|Schedule used to execute the job. Read-only.|
|status         |[synchronizationStatus](synchronization_synchronizationstatus.md)     |Status of the job, which includes when the job was last executed, current job state and errors.|
|templateId     |String    |Identifier of the [synchronization template](synchronization_template.md) this job is based on.|

## Relationships
| Relationship | Type	|Description|
|:---------------|:--------|:----------|
|schema|[synchronizationSchema](synchronizationschema.md)| Synchronization schema configured for the job.|

## JSON representation

Here is a JSON representation of the resource.

<!-- {
  "blockType": "resource",
  "optionalProperties": [

  ],
  "@odata.type": "microsoft.graph.synchronizationJob"
}-->

```json
{
  "id": "String (identifier)",
  "schedule": {"@odata.type": "microsoft.graph.synchronizationSchedule"},
  "status": {"@odata.type": "microsoft.graph.synchronizationStatus"},
  "templateId": "String"
}

```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "synchronizationJob resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->
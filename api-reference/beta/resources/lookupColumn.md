# LookupColumn resource type

> **Important:** APIs under the /beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

The **lookupColumn** on a [columnDefinition](columnDefinition.md) resource indicates that the column's values are looked up from another source in the site.

## JSON representation

Here is a JSON representation of a **lookupColumn** resource.
<!-- { "blockType": "resource", "@odata.type": "microsoft.graph.lookupColumn" } -->

```json
{
  "allowMultipleValues": true,
  "columnName": "string",
  "listId": "string",
  "primaryLookupColumnId": "string"
}
```

## Properties

| Property name             | Type    | Description
|:--------------------------|:--------|:---------------------------------------
| **allowMultipleValues**   | boolean | Indicates whether multiple values can be selected from the source.
| **columnName**            | string  | The name of the lookup source column.
| **listId**                | string  | The unique identifier of the lookup source list.
| **primaryLookupColumnId** | string  | If specified, this column is a *secondary lookup*, pulling an additional field from the list item looked up by the *primary lookup*. Use the list item looked up by the *primary* as the source for the column named here.

<!-- {
  "type": "#page.annotation",
  "description": "",
  "keywords": "",
  "section": "documentation",
  "tocPath": "Resources/LookupColumn"
} -->

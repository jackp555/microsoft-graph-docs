# Azure AD synchronization API overview

> **Important:** APIs under the /beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

Azure Active Directory (Azure AD) identity synchronization (also called "provisioning") allows you to automate the creation, maintenance, and removal of identities in cloud (software as a service, or SaaS) applications such as Dropbox, Salesforce, ServiceNow, and more. You can use the synchronization APIs in Microsoft Graph to manage identity synchronization programmatically, including:

- Create, start, and stop synchronization jobs
- Make changes to the synchronization schema for jobs
- Verify the current synchronization status 

For more information about synchronization in Azure AD, see:

* [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-app-provisioning)
* [Managing user account provisioning for enterprise apps in the Azure portal](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-enterprise-apps-manage-provisioning)

You can also try the API in the [Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer) in a sample tenant or your own tenant.

## Authorization

The Azure AD synchronization API uses OAuth 2.0 for authorization. Before making any requests to the API, you need to get an access token. For more information, see [Get access tokens to call Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/auth_overview). To access synchronization resources, your application needs Directory.ReadWrite.All permissions. For more information, see [Directory permissions](../../../concepts/permissions_reference.md#directory-permissions).

## Synchronization job

Synchronization jobs perform synchronization by periodically running in the background, polling for changes in one directory, and pushing them to another directory. The synchronization job is always specific to a particular instance of an application in your tenant. As part of the synchronization job setup, you need to give authorization to read and write objects in your target directory, and customize the job's synchronization schema.

For more information, see [synchronization job](synchronization_synchronizationjob.md).

## Synchronization schema

The synchronization schema defines what objects will be synchronized and how they will be synchronized. The synchronization schema contains most of the setup information for a particular synchronization job. Typically, you will customize some of the [attribute mappings](synchronization_attributemapping.md), or add a [scoping filter](synchronization_filter.md) to synchronize only objects that satisfy a certain condition.

The synchronization schema includes the following components:

- Directory definitions
- Synchronization rules
- Object mappings

For more information, see [synchronization schema](synchronization_synchronizationschema.md).

## Synchronization template

The synchronization template provides pre-configured synchronization settings for a particular application. These settings (most importantly, [synchronization schema](synchronization_synchronizationschema.md)) will be used by default for any [synchronization job](synchronization_synchronizationjob.md) that is based on the template. Templates are specified by the application developer.

For more information, see [synchronization template](synchronization_synchronizationtemplate.md).

## Working with the synchronization API

Working with synchronization API primarily involves accessing the [synchronizationJob](synchronization_synchronizationjob.md) and [synchronizationSchema](synchronization_synchronizationschema.md) resources. To find your [synchronizationJob](synchronization_synchronizationjob.md) resource, you need to know the ID of the service principal object that the synchronization job belongs to. The following examples show you how to work with the **synchronizationJob** and **synchronizationSchema** resources.

### Find the service principal object

To make requests to the synchronization API, you need to know the ID of the [service principal object](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-dev-glossary#service-principal-object). This example assumes that the you have already added the service principal for your application to the tenant (by adding the application to your tenant in the Azure portal). You can find the service principal object by either display name or app ID.

#### Find service principal object by display name

The following example shows how to find service principal object by display name.

**Request** 

<!-- { "blockType": "ignored" } -->
```http
GET https://graph.microsoft.com/beta/servicePrincipals?$select=id,appId,displayName&$filter=startswith(displayName, 'salesforce')
```

**Response**

<!-- { "blockType": "ignored" } -->
```http
HTTP/1.1 200 OK
{
    "value": [
    {
        "id": "bc0dc311-87df-48ac-91b1-259bd2c3a31c",
        "appId": "f7808c5e-cb57-4e37-8094-406d302c0f8d",
        "displayName": "Salesforce"
    },
    {
        "id": "d813d7d7-0f41-4edc-b284-d0dfaf399d15",
        "appId": "219561ee-1480-4c67-9aa6-63d861fae3ef",
        "displayName": "salesforce 3"
    }
    ]
}
```

#### Find service principal object by app ID

The following example shows how to find the service principal object by app ID.

**Request** 
<!-- { "blockType": "ignored" } -->
```http
GET https://graph.microsoft.com/beta/servicePrincipals?$select=id,appId,displayName&$filter=AppId eq '219561ee-1480-4c67-9aa6-63d861fae3ef'
```

**Response**
<!-- { "blockType": "ignored" } -->
```http
HTTP/1.1 200 OK
{
    "value": [
        {
            "id": "d813d7d7-0f41-4edc-b284-d0dfaf399d15",
            "appId": "219561ee-1480-4c67-9aa6-63d861fae3ef",
            "displayName": "salesforce 3"
        }
    ]
}
```

### List existing synchronization jobs

The following example shows you how to list existing synchronization jobs.

**Request**
<!-- { "blockType": "ignored" } -->
```http
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs
GET https://graph.microsoft.com/beta/servicePrincipals/60443998-8cf7-4e61-b05c-a53b658cb5e1/synchronization/jobs
```

**Response**
<!-- { "blockType": "ignored" } -->
```http
HTTP/1.1 200 OK
{
    "value": [
        {
            "id": "SfSandboxOutDelta.e4bbf44533ea4eabb17027f3a92e92aa",
            "templateId": "SfSandboxOutDelta",
            "schedule": {
                "expiration": null,
                "interval": "PT20M",
                "state": "Active"
            },
            "status": {}
        }
    ]
}
```

### Get synchronization job status
The following example shows you how to get the status of a synchronization job.

**Request**
<!-- { "blockType": "ignored" } -->
```http
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs/{jobId}

GET https://graph.microsoft.com/beta/servicePrincipals/60443998-8cf7-4e61-b05c-a53b658cb5e1/synchronization/jobs/SfSandboxOutDelta.e4bbf44533ea4eabb17027f3a92e92aa
```

**Response**
<!-- { "blockType": "ignored" } -->
```http
    HTTP/1.1 200 OK
    {
        "id": "SfSandboxOutDelta.e4bbf44533ea4eabb17027f3a92e92aa",
        "templateId": "SfSandboxOutDelta",
        "schedule": {
            "expiration": null,
            "interval": "PT20M",
            "state": "Active"
        },
        "status": {}
    }
```

### Get synchronization schema
The following example shows you how to get the synchronization schema.

**Request**
<!-- { "blockType": "ignored" } -->
```http
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/synchronization/jobs/{jobId}/schema
```

**Response**
<!-- { "blockType": "ignored" } -->
```http
HTTP/1.1 200 OK
{
    "directories": [],
    "synchronizationRules": []
}
```
## See also

* [Configure synchronization with directory extension attributes](../resources/synchronization-configure-with-directory-extension-attributes.md)
* [Configure synchronization with custom target attributes](../resources/synchronization-configure-with-custom-target-attributes.md)



# Synchronization Overview

## Synchronization API Object Model Overview

### Synchronization Template

Synchronization template provides default synchronization settings for a particular application. Template is controlled by the developer of the application, although anyone can retrieve the template to see the default settings. One of the most important settings template provides is synchronization schema, which will be used as default one for any synchronization job based on this template. Template is required to create a synchronization job. For more information, please see [synchronization template](synchronization-template.md)

Application developer may provide multiple templates for a given application, and designate a default one. If multiple templates are available for the application you are interested in, seek application-specific guidance on which one better suits your case.

### Synchronization Job

Synchronization job performs synchronization by periodically running in the background, polling for changes in one directory and pushing them to another directory. Synchronization job is always specific to a particular instance of an application in your tenant. As part of the synchronization job setup, generally you would need to give authorization to read/write objects in your target directory, and customize job's synchronization schema to suit your needs. For more information, please see [synchronization job](synchronization-job.md)

### Synchronization Schema

Synchronization schema contains the bulk of a particular synchronization setup. On a high level, it defines what objects will be synchronized and how. Most often you will want to customize some of the attribute mappings to suit your needs, or add a scoping filter to synchronize only objects which satisfy a certain condition. For more information, please see [synchronization schema](synchronization-schema-overview.md)

#### Directory Definitions

Directory definitions are part of the [synchronization schema](synchronization-schema-overview.md) and provide synchronization engine information about directories and their objects. It tells synchronization engine, for example, that directory "Azure AD" has objects named "User" and "Group", which attributes are supported for those objects, and what is the type of those attributes. In order for a particular object and attribute to be used in synchronization rules / object mappings, they have to be defined as part of the directory definition. For more information, please see [directory definition](synchronization-directoryDefinition.md)

#### Synchronization Rules

Synchronization rules area part of the [synchronization schema](synchronization-schema-overview.md) and are at the core of the synchronization setup. They give synchronization engine crucial information regarding how the synchronization should be performed. That includes what objects should be synchronized, how objects from source directory should be matched with objects in target directory, and how attributes should be transformed going from source to target directory. For more information, please see [synchronization rule](synchronization-rule.md)

#### Object mappings

Object mappings are the main part of the synchronization rule. Each object mapping defines how a given object should be synchronized from source directory to target. In particular, it defines how object in source directory should be matched with an object in target directory, what (if any) scoping filters should be used to decide if we want to provision a given object, and how object attributes should be transformed going from source to target directory. For more information, please see [object mapping](synchronization-objectMapping.md)
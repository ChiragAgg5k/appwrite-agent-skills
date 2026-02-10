# Migrations

The Migrations service allows you to migrate third-party data to your Appwrite project.

## List migrations

`list`
List all migrations in the current project. This endpoint returns a list of all migrations including their status, progress, and any errors that occurred during the migration process.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/databases#querying-documents). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: status, stage, source, destination, resources, statusCounters, resourceData, errors (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `migrationList`

## Create Appwrite migration

`createAppwriteMigration`
Migrate data from another Appwrite project to your current project. This endpoint allows you to migrate resources like databases, collections, documents, users, and files from an existing Appwrite project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `endpoint` | string | Yes | Source Appwrite endpoint |
| `projectId` | string | Yes | Source Project ID |
| `apiKey` | string | Yes | Source API Key |

**Response:** `migration`

## Get Appwrite migration report

`getAppwriteReport`
Generate a report of the data in an Appwrite project before migrating. This endpoint analyzes the source project and returns information about the resources that can be migrated.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `endpoint` | string | Yes | Source&#039;s Appwrite Endpoint |
| `projectID` | string | Yes | Source&#039;s Project ID |
| `key` | string | Yes | Source&#039;s API Key |

**Response:** `migrationReport`

## Export documents to CSV

`createCSVExport`
Export documents to a CSV file from your Appwrite database. This endpoint allows you to export documents to a CSV file stored in a secure internal bucket. You&#039;ll receive an email with a download link when the export is complete.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resourceId` | string | Yes | Composite ID in the format {databaseId:collectionId}, identifying a collection within a database to export. |
| `filename` | string | Yes | The name of the file to be created for the export, excluding the .csv extension. |
| `columns` | array\<string\> | No | List of attributes to export. If empty, all attributes will be exported. You can use the `*` wildcard to export all attributes from the collection. (default: `[]`) |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK to filter documents to export. [Learn more about queries](https://appwrite.io/docs/databases#querying-documents). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `delimiter` | string | No | The character that separates each column value. Default is comma. (default: `,`) |
| `enclosure` | string | No | The character that encloses each column value. Default is double quotes. (default: `&quot;`) |
| `escape` | string | No | The escape character for the enclosure character. Default is double quotes. (default: `&quot;`) |
| `header` | boolean | No | Whether to include the header row with column names. Default is true. (default: `1`) |
| `notify` | boolean | No | Set to true to receive an email when the export is complete. Default is true. (default: `1`) |

**Response:** `migration`

## Import documents from a CSV

`createCSVImport`
Import documents from a CSV file into your Appwrite database. This endpoint allows you to import documents from a CSV file uploaded to Appwrite Storage bucket.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID. |
| `resourceId` | string | Yes | Composite ID in the format {databaseId:collectionId}, identifying a collection within a database. |
| `internalFile` | boolean | No | Is the file stored in an internal bucket? |

**Response:** `migration`

## Create Firebase migration

`createFirebaseMigration`
Migrate data from a Firebase project to your Appwrite project. This endpoint allows you to migrate resources like authentication and other supported services from a Firebase project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `serviceAccount` | string | Yes | JSON of the Firebase service account credentials |

**Response:** `migration`

## Get Firebase migration report

`getFirebaseReport`
Generate a report of the data in a Firebase project before migrating. This endpoint analyzes the source project and returns information about the resources that can be migrated.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `serviceAccount` | string | Yes | JSON of the Firebase service account credentials |

**Response:** `migrationReport`

## Create NHost migration

`createNHostMigration`
Migrate data from an NHost project to your Appwrite project. This endpoint allows you to migrate resources like authentication, databases, and other supported services from an NHost project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `subdomain` | string | Yes | Source&#039;s Subdomain |
| `region` | string | Yes | Source&#039;s Region |
| `adminSecret` | string | Yes | Source&#039;s Admin Secret |
| `database` | string | Yes | Source&#039;s Database Name |
| `username` | string | Yes | Source&#039;s Database Username |
| `password` | string | Yes | Source&#039;s Database Password |
| `port` | integer | No | Source&#039;s Database Port (default: `5432`) |

**Response:** `migration`

## Get NHost migration report

`getNHostReport`
Generate a detailed report of the data in an NHost project before migrating. This endpoint analyzes the source project and returns information about the resources that can be migrated. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate. |
| `subdomain` | string | Yes | Source&#039;s Subdomain. |
| `region` | string | Yes | Source&#039;s Region. |
| `adminSecret` | string | Yes | Source&#039;s Admin Secret. |
| `database` | string | Yes | Source&#039;s Database Name. |
| `username` | string | Yes | Source&#039;s Database Username. |
| `password` | string | Yes | Source&#039;s Database Password. |
| `port` | integer | No | Source&#039;s Database Port. (default: `5432`) |

**Response:** `migrationReport`

## Create Supabase migration

`createSupabaseMigration`
Migrate data from a Supabase project to your Appwrite project. This endpoint allows you to migrate resources like authentication, databases, and other supported services from a Supabase project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `endpoint` | string | Yes | Source&#039;s Supabase Endpoint |
| `apiKey` | string | Yes | Source&#039;s API Key |
| `databaseHost` | string | Yes | Source&#039;s Database Host |
| `username` | string | Yes | Source&#039;s Database Username |
| `password` | string | Yes | Source&#039;s Database Password |
| `port` | integer | No | Source&#039;s Database Port (default: `5432`) |

**Response:** `migration`

## Get Supabase migration report

`getSupabaseReport`
Generate a report of the data in a Supabase project before migrating. This endpoint analyzes the source project and returns information about the resources that can be migrated. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `resources` | array\<string\> | Yes | List of resources to migrate |
| `endpoint` | string | Yes | Source&#039;s Supabase Endpoint. |
| `apiKey` | string | Yes | Source&#039;s API Key. |
| `databaseHost` | string | Yes | Source&#039;s Database Host. |
| `username` | string | Yes | Source&#039;s Database Username. |
| `password` | string | Yes | Source&#039;s Database Password. |
| `port` | integer | No | Source&#039;s Database Port. (default: `5432`) |

**Response:** `migrationReport`

## Get migration

`get`
Get a migration by its unique ID. This endpoint returns detailed information about a specific migration including its current status, progress, and any errors that occurred during the migration process. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `migrationId` | string | Yes | Migration unique ID. |

**Response:** `migration`

## Update retry migration

`retry`
Retry a failed migration. This endpoint allows you to retry a migration that has previously failed.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `migrationId` | string | Yes | Migration unique ID. |

**Response:** `migration`

## Delete migration

`delete`
Delete a migration by its unique ID. This endpoint allows you to remove a migration from your project&#039;s migration history. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `migrationId` | string | Yes | Migration ID. |



# Databases

The Databases service allows you to create structured collections of documents, query and filter lists of documents

## list

`list` **(DEPRECATED — use `tablesDB.list` instead)**
Get a list of all databases from the current Appwrite project. You can use the search parameter to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `databaseList`

## create

`create` **(DEPRECATED — use `tablesDB.create` instead)**
Create a new Database.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Database name. Max length: 128 chars. |
| `enabled` | boolean | No | Is the database enabled? When set to &#039;disabled&#039;, users cannot access the database but Server SDKs with an API key can still read and write to the database. No data is lost when this is toggled. (default: `1`) |

**Response:** `database`

## List transactions

`listTransactions`
List transactions across all databases.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). (default: `[]`) |

**Response:** `transactionList`

## Create transaction

`createTransaction`
Create a new transaction.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `ttl` | integer | No | Seconds before the transaction expires. (default: `300`) |

**Response:** `transaction`

## Get transaction

`getTransaction`
Get a transaction by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `transactionId` | string | Yes | Transaction ID. |

**Response:** `transaction`

## Update transaction

`updateTransaction`
Update a transaction, to either commit or roll back its operations.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `transactionId` | string | Yes | Transaction ID. |
| `commit` | boolean | No | Commit transaction? |
| `rollback` | boolean | No | Rollback transaction? |

**Response:** `transaction`

## Delete transaction

`deleteTransaction`
Delete a transaction by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `transactionId` | string | Yes | Transaction ID. |


## Create operations

`createOperations`
Create multiple operations in a single transaction.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `transactionId` | string | Yes | Transaction ID. |
| `operations` | array\<object\> | No | Array of staged operations. (default: `[]`) |

**Response:** `transaction`

## listUsage

`listUsage` **(DEPRECATED — use `tablesDB.listUsage` instead)**
List usage metrics and statistics for all databases in the project. You can view the total number of databases, collections, documents, and storage usage. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageDatabases`

## get

`get` **(DEPRECATED — use `tablesDB.get` instead)**
Get a database by its unique ID. This endpoint response returns a JSON object with the database metadata.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |

**Response:** `database`

## update

`update` **(DEPRECATED — use `tablesDB.update` instead)**
Update a database by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `name` | string | No | Database name. Max length: 128 chars. |
| `enabled` | boolean | No | Is database enabled? When set to &#039;disabled&#039;, users cannot access the database but Server SDKs with an API key can still read and write to the database. No data is lost when this is toggled. (default: `1`) |

**Response:** `database`

## delete

`delete` **(DEPRECATED — use `tablesDB.delete` instead)**
Delete a database by its unique ID. Only API keys with with databases.write scope can delete a database.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |


## List collections

`listCollections` **(DEPRECATED — use `tablesDB.listTables` instead)**
Get a list of all collections that belong to the provided databaseId. You can use the search parameter to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, enabled, documentSecurity (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `collectionList`

## Create collections

`createCollection` **(DEPRECATED — use `tablesDB.createTable` instead)**
Create a new Collection. Before using this route, you should create a new database resource using either a [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Collection name. Max length: 128 chars. |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, no user is granted with any permissions. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `documentSecurity` | boolean | No | Enables configuring permissions for individual documents. A user needs one of document or collection level permissions to access a document. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `enabled` | boolean | No | Is collection enabled? When set to &#039;disabled&#039;, users cannot access the collection but Server SDKs with and API key can still read and write to the collection. No data is lost when this is toggled. (default: `1`) |
| `attributes` | array\<object\> | No | Array of attribute definitions to create. Each attribute should contain: key (string), type (string: string, integer, float, boolean, datetime), size (integer, required for string type), required (boolean, optional), default (mixed, optional), array (boolean, optional), and type-specific options. (default: `[]`) |
| `indexes` | array\<object\> | No | Array of index definitions to create. Each index should contain: key (string), type (string: key, fulltext, unique, spatial), attributes (array of attribute keys), orders (array of ASC/DESC, optional), and lengths (array of integers, optional). (default: `[]`) |

**Response:** `collection`

## Get collection

`getCollection` **(DEPRECATED — use `tablesDB.getTable` instead)**
Get a collection by its unique ID. This endpoint response returns a JSON object with the collection metadata.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |

**Response:** `collection`

## Update collection

`updateCollection` **(DEPRECATED — use `tablesDB.updateTable` instead)**
Update a collection by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `name` | string | No | Collection name. Max length: 128 chars. |
| `permissions` | array\<string\> | No | An array of permission strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `documentSecurity` | boolean | No | Enables configuring permissions for individual documents. A user needs one of document or collection level permissions to access a document. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `enabled` | boolean | No | Is collection enabled? When set to &#039;disabled&#039;, users cannot access the collection but Server SDKs with and API key can still read and write to the collection. No data is lost when this is toggled. (default: `1`) |

**Response:** `collection`

## Delete collection

`deleteCollection` **(DEPRECATED — use `tablesDB.deleteTable` instead)**
Delete a collection by its unique ID. Only users with write permissions have access to delete this resource.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |


## List attributes

`listAttributes` **(DEPRECATED — use `tablesDB.listColumns` instead)**
List attributes in the collection.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: key, type, size, required, array, status, error (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `attributeList`

## Create boolean attribute

`createBooleanAttribute` **(DEPRECATED — use `tablesDB.createBooleanColumn` instead)**
Create a boolean attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | boolean | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeBoolean`

## Update boolean attribute

`updateBooleanAttribute` **(DEPRECATED — use `tablesDB.updateBooleanColumn` instead)**
Update a boolean attribute. Changing the `default` value will not update already existing documents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#createCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | boolean | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New attribute key. |

**Response:** `attributeBoolean`

## Create datetime attribute

`createDatetimeAttribute` **(DEPRECATED — use `tablesDB.createDatetimeColumn` instead)**
Create a date time attribute according to the ISO 8601 standard.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#createCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for the attribute in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeDatetime`

## Update datetime attribute

`updateDatetimeAttribute` **(DEPRECATED — use `tablesDB.updateDatetimeColumn` instead)**
Update a date time attribute. Changing the `default` value will not update already existing documents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New attribute key. |

**Response:** `attributeDatetime`

## Create email attribute

`createEmailAttribute` **(DEPRECATED — use `tablesDB.createEmailColumn` instead)**
Create an email attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeEmail`

## Update email attribute

`updateEmailAttribute` **(DEPRECATED — use `tablesDB.updateEmailColumn` instead)**
Update an email attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeEmail`

## Create enum attribute

`createEnumAttribute` **(DEPRECATED — use `tablesDB.createEnumColumn` instead)**
Create an enum attribute. The `elements` param acts as a white-list of accepted values for this attribute. 


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `elements` | array\<string\> | Yes | Array of enum values. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeEnum`

## Update enum attribute

`updateEnumAttribute` **(DEPRECATED — use `tablesDB.updateEnumColumn` instead)**
Update an enum attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `elements` | array\<string\> | Yes | Updated list of enum values. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeEnum`

## Create float attribute

`createFloatAttribute` **(DEPRECATED — use `tablesDB.createFloatColumn` instead)**
Create a float attribute. Optionally, minimum and maximum values can be provided.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `min` | number | No | Minimum value. |
| `max` | number | No | Maximum value. |
| `default` | number | No | Default value. Cannot be set when required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeFloat`

## Update float attribute

`updateFloatAttribute` **(DEPRECATED — use `tablesDB.updateFloatColumn` instead)**
Update a float attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | number | Yes | Default value. Cannot be set when required. |
| `min` | number | No | Minimum value. |
| `max` | number | No | Maximum value. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeFloat`

## Create integer attribute

`createIntegerAttribute` **(DEPRECATED — use `tablesDB.createIntegerColumn` instead)**
Create an integer attribute. Optionally, minimum and maximum values can be provided.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `min` | integer | No | Minimum value |
| `max` | integer | No | Maximum value |
| `default` | integer | No | Default value. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeInteger`

## Update integer attribute

`updateIntegerAttribute` **(DEPRECATED — use `tablesDB.updateIntegerColumn` instead)**
Update an integer attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | integer | Yes | Default value. Cannot be set when attribute is required. |
| `min` | integer | No | Minimum value |
| `max` | integer | No | Maximum value |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeInteger`

## Create IP address attribute

`createIpAttribute` **(DEPRECATED — use `tablesDB.createIpColumn` instead)**
Create IP address attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeIp`

## Update IP address attribute

`updateIpAttribute` **(DEPRECATED — use `tablesDB.updateIpColumn` instead)**
Update an ip attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeIp`

## Create line attribute

`createLineAttribute` **(DEPRECATED — use `tablesDB.createLineColumn` instead)**
Create a geometric line attribute.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | array | No | Default value for attribute when not provided, two-dimensional array of coordinate pairs, [[longitude, latitude], [longitude, latitude], …], listing the vertices of the line in order. Cannot be set when attribute is required. |

**Response:** `attributeLine`

## Update line attribute

`updateLineAttribute` **(DEPRECATED — use `tablesDB.updateLineColumn` instead)**
Update a line attribute. Changing the `default` value will not update already existing documents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#createCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | array | No | Default value for attribute when not provided, two-dimensional array of coordinate pairs, [[longitude, latitude], [longitude, latitude], …], listing the vertices of the line in order. Cannot be set when attribute is required. |
| `newKey` | string | No | New attribute key. |

**Response:** `attributeLine`

## Create longtext attribute

`createLongtextAttribute`
Create a longtext attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeLongtext`

## Update longtext attribute

`updateLongtextAttribute`
Update a longtext attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeLongtext`

## Create mediumtext attribute

`createMediumtextAttribute`
Create a mediumtext attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeMediumtext`

## Update mediumtext attribute

`updateMediumtextAttribute`
Update a mediumtext attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeMediumtext`

## Create point attribute

`createPointAttribute` **(DEPRECATED — use `tablesDB.createPointColumn` instead)**
Create a geometric point attribute.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | array | No | Default value for attribute when not provided, array of two numbers [longitude, latitude], representing a single coordinate. Cannot be set when attribute is required. |

**Response:** `attributePoint`

## Update point attribute

`updatePointAttribute` **(DEPRECATED — use `tablesDB.updatePointColumn` instead)**
Update a point attribute. Changing the `default` value will not update already existing documents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#createCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | array | No | Default value for attribute when not provided, array of two numbers [longitude, latitude], representing a single coordinate. Cannot be set when attribute is required. |
| `newKey` | string | No | New attribute key. |

**Response:** `attributePoint`

## Create polygon attribute

`createPolygonAttribute` **(DEPRECATED — use `tablesDB.createPolygonColumn` instead)**
Create a geometric polygon attribute.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | array | No | Default value for attribute when not provided, three-dimensional array where the outer array holds one or more linear rings, [[[longitude, latitude], …], …], the first ring is the exterior boundary, any additional rings are interior holes, and each ring must start and end with the same coordinate pair. Cannot be set when attribute is required. |

**Response:** `attributePolygon`

## Update polygon attribute

`updatePolygonAttribute` **(DEPRECATED — use `tablesDB.updatePolygonColumn` instead)**
Update a polygon attribute. Changing the `default` value will not update already existing documents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#createCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | array | No | Default value for attribute when not provided, three-dimensional array where the outer array holds one or more linear rings, [[[longitude, latitude], …], …], the first ring is the exterior boundary, any additional rings are interior holes, and each ring must start and end with the same coordinate pair. Cannot be set when attribute is required. |
| `newKey` | string | No | New attribute key. |

**Response:** `attributePolygon`

## Create relationship attribute

`createRelationshipAttribute` **(DEPRECATED — use `tablesDB.createRelationshipColumn` instead)**
Create relationship attribute. [Learn more about relationship attributes](https://appwrite.io/docs/databases-relationships#relationship-attributes).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `relatedCollectionId` | string | Yes | Related Collection ID. |
| `type` | string | Yes | Relation type |
| `twoWay` | boolean | No | Is Two Way? |
| `key` | string | No | Attribute Key. |
| `twoWayKey` | string | No | Two Way Attribute Key. |
| `onDelete` | string | No | Constraints option (default: `restrict`) |

**Response:** `attributeRelationship`

## Create string attribute

`createStringAttribute` **(DEPRECATED — use `tablesDB.createStringColumn` instead)**
Create a string attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `size` | integer | Yes | Attribute size for text attributes, in number of characters. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |
| `encrypt` | boolean | No | Toggle encryption for the attribute. Encryption enhances security by not storing any plain text values in the database. However, encrypted attributes cannot be queried. |

**Response:** `attributeString`

## Update string attribute

`updateStringAttribute` **(DEPRECATED — use `tablesDB.updateStringColumn` instead)**
Update a string attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `size` | integer | No | Maximum size of the string attribute. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeString`

## Create text attribute

`createTextAttribute`
Create a text attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeText`

## Update text attribute

`updateTextAttribute`
Update a text attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeText`

## Create URL attribute

`createUrlAttribute` **(DEPRECATED — use `tablesDB.createUrlColumn` instead)**
Create a URL attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeUrl`

## Update URL attribute

`updateUrlAttribute` **(DEPRECATED — use `tablesDB.updateUrlColumn` instead)**
Update an url attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeUrl`

## Create varchar attribute

`createVarcharAttribute`
Create a varchar attribute.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `size` | integer | Yes | Attribute size for varchar attributes, in number of characters. Maximum size is 16381. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | No | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `array` | boolean | No | Is attribute an array? |

**Response:** `attributeVarchar`

## Update varchar attribute

`updateVarcharAttribute`
Update a varchar attribute. Changing the `default` value will not update already existing documents.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Attribute Key. |
| `required` | boolean | Yes | Is attribute required? |
| `default` | string | Yes | Default value for attribute when not provided. Cannot be set when attribute is required. |
| `size` | integer | No | Maximum size of the varchar attribute. |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeVarchar`

## Get attribute

`getAttribute` **(DEPRECATED — use `tablesDB.getColumn` instead)**
Get attribute by ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |

**Response:** `attributeBoolean`

## Delete attribute

`deleteAttribute` **(DEPRECATED — use `tablesDB.deleteColumn` instead)**
Deletes an attribute.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |


## Update relationship attribute

`updateRelationshipAttribute` **(DEPRECATED — use `tablesDB.updateRelationshipColumn` instead)**
Update relationship attribute. [Learn more about relationship attributes](https://appwrite.io/docs/databases-relationships#relationship-attributes).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `key` | string | Yes | Attribute Key. |
| `onDelete` | string | No | Constraints option |
| `newKey` | string | No | New Attribute Key. |

**Response:** `attributeRelationship`

## List documents

`listDocuments` **(DEPRECATED — use `tablesDB.listRows` instead)**
Get a list of all the user&#039;s documents in a given collection. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID to read uncommitted changes within the transaction. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `documentList`

## createDocument

`createDocument` **(DEPRECATED — use `tablesDB.createRow` instead)**
Create a new Document. Before using this route, you should create a new collection resource using either a [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). Make sure to define attributes before creating documents. |
| `documentId` | string | Yes | Document ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `data` | object | Yes | Document data as JSON object. (default: `{}`) |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, only the current user is granted all permissions. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `document`

## createDocuments

`createDocuments` **(DEPRECATED — use `tablesDB.createRows` instead)**
Create new Documents. Before using this route, you should create a new collection resource using either a [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). Make sure to define attributes before creating documents. |
| `documents` | array\<object\> | Yes | Array of documents data as JSON objects. (default: `[]`) |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `documentList`

## upsertDocuments

`upsertDocuments` **(DEPRECATED — use `tablesDB.upsertRows` instead)**
Create or update Documents. Before using this route, you should create a new collection resource using either a [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection) API or directly from your database console.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `documents` | array\<object\> | Yes | Array of document data as JSON objects. May contain partial documents. |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `documentList`

## Update documents

`updateDocuments` **(DEPRECATED — use `tablesDB.updateRows` instead)**
Update all documents that match your queries, if no queries are submitted then all documents are updated. You can pass only specific fields to be updated.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `data` | object | No | Document data as JSON object. Include only attribute and value pairs to be updated. (default: `{}`) |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `documentList`

## Delete documents

`deleteDocuments` **(DEPRECATED — use `tablesDB.deleteRows` instead)**
Bulk delete documents using queries, if no queries are passed then all documents are deleted.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `documentList`

## Get document

`getDocument` **(DEPRECATED — use `tablesDB.getRow` instead)**
Get a document by its unique ID. This endpoint response returns a JSON object with the document data.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `documentId` | string | Yes | Document ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID to read uncommitted changes within the transaction. |

**Response:** `document`

## upsertDocument

`upsertDocument` **(DEPRECATED — use `tablesDB.upsertRow` instead)**
Create or update a Document. Before using this route, you should create a new collection resource using either a [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `documentId` | string | Yes | Document ID. |
| `data` | object | No | Document data as JSON object. Include all required attributes of the document to be created or updated. (default: `{}`) |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `document`

## Update document

`updateDocument` **(DEPRECATED — use `tablesDB.updateRow` instead)**
Update a document by its unique ID. Using the patch method you can pass only specific fields that will get updated.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `documentId` | string | Yes | Document ID. |
| `data` | object | No | Document data as JSON object. Include only attribute and value pairs to be updated. (default: `{}`) |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `document`

## Delete document

`deleteDocument` **(DEPRECATED — use `tablesDB.deleteRow` instead)**
Delete a document by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `documentId` | string | Yes | Document ID. |
| `transactionId` | string | No | Transaction ID for staging the operation. |


## List document logs

`listDocumentLogs` **(DEPRECATED — use `tablesDB.listRowLogs` instead)**
Get the document activity logs list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `documentId` | string | Yes | Document ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |

**Response:** `logList`

## Decrement document attribute

`decrementDocumentAttribute` **(DEPRECATED — use `tablesDB.decrementRowColumn` instead)**
Decrement a specific attribute of a document by a given value.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `documentId` | string | Yes | Document ID. |
| `attribute` | string | Yes | Attribute key. |
| `value` | number | No | Value to increment the attribute by. The value must be a number. (default: `1`) |
| `min` | number | No | Minimum value for the attribute. If the current value is lesser than this value, an exception will be thrown. |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `document`

## Increment document attribute

`incrementDocumentAttribute` **(DEPRECATED — use `tablesDB.incrementRowColumn` instead)**
Increment a specific attribute of a document by a given value.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `documentId` | string | Yes | Document ID. |
| `attribute` | string | Yes | Attribute key. |
| `value` | number | No | Value to increment the attribute by. The value must be a number. (default: `1`) |
| `max` | number | No | Maximum value for the attribute. If the current value is greater than this value, an error will be thrown. |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `document`

## List indexes

`listIndexes` **(DEPRECATED — use `tablesDB.listIndexes` instead)**
List indexes in the collection.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: key, type, status, attributes, error (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `indexList`

## Create index

`createIndex` **(DEPRECATED — use `tablesDB.createIndex` instead)**
Creates an index on the attributes listed. Your index should include all the attributes you will query in a single request.
Attributes can be `key`, `fulltext`, and `unique`.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Index Key. |
| `type` | string | Yes | Index type. |
| `attributes` | array\<string\> | Yes | Array of attributes to index. Maximum of 100 attributes are allowed, each 32 characters long. |
| `orders` | array\<string\> | No | Array of index orders. Maximum of 100 orders are allowed. (default: `[]`) |
| `lengths` | array\<integer\> | No | Length of index. Maximum of 100 (default: `[]`) |

**Response:** `index`

## Get index

`getIndex` **(DEPRECATED — use `tablesDB.getIndex` instead)**
Get an index by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Index Key. |

**Response:** `index`

## Delete index

`deleteIndex` **(DEPRECATED — use `tablesDB.deleteIndex` instead)**
Delete an index.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. You can create a new collection using the Database service [server integration](https://appwrite.io/docs/server/databases#databasesCreateCollection). |
| `key` | string | Yes | Index Key. |


## List collection logs

`listCollectionLogs` **(DEPRECATED — use `tablesDB.listTableLogs` instead)**
Get the collection activity logs list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |

**Response:** `logList`

## Get collection usage stats

`getCollectionUsage` **(DEPRECATED — use `tablesDB.getTableUsage` instead)**
Get usage metrics and statistics for a collection. Returning the total number of documents. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `collectionId` | string | Yes | Collection ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageCollection`

## listLogs

`listLogs` **(DEPRECATED — use `tablesDB.listDatabaseLogs` instead)**
Get the database activity logs list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |

**Response:** `logList`

## getUsage

`getUsage` **(DEPRECATED — use `tablesDB.getUsage` instead)**
Get usage metrics and statistics for a database. You can view the total number of collections, documents, and storage usage. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageDatabase`


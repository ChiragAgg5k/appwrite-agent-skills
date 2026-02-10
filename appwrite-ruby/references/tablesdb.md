# TablesDB



## List databases

`list`
Get a list of all databases from the current Appwrite project. You can use the search parameter to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following columns: name (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `databaseList`

## Create database

`create`
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

`listUsage`
List usage metrics and statistics for all databases in the project. You can view the total number of databases, tables, rows, and storage usage. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageDatabases`

## Get database

`get`
Get a database by its unique ID. This endpoint response returns a JSON object with the database metadata.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |

**Response:** `database`

## Update database

`update`
Update a database by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `name` | string | No | Database name. Max length: 128 chars. |
| `enabled` | boolean | No | Is database enabled? When set to &#039;disabled&#039;, users cannot access the database but Server SDKs with an API key can still read and write to the database. No data is lost when this is toggled. (default: `1`) |

**Response:** `database`

## Delete database

`delete`
Delete a database by its unique ID. Only API keys with with databases.write scope can delete a database.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |


## List tables

`listTables`
Get a list of all tables that belong to the provided databaseId. You can use the search parameter to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following columns: name, enabled, rowSecurity (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `tableList`

## Create table

`createTable`
Create a new Table. Before using this route, you should create a new database resource using either a [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Table name. Max length: 128 chars. |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, no user is granted with any permissions. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `rowSecurity` | boolean | No | Enables configuring permissions for individual rows. A user needs one of row or table level permissions to access a row. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `enabled` | boolean | No | Is table enabled? When set to &#039;disabled&#039;, users cannot access the table but Server SDKs with and API key can still read and write to the table. No data is lost when this is toggled. (default: `1`) |
| `columns` | array\<object\> | No | Array of column definitions to create. Each column should contain: key (string), type (string: string, integer, float, boolean, datetime, relationship), size (integer, required for string type), required (boolean, optional), default (mixed, optional), array (boolean, optional), and type-specific options. (default: `[]`) |
| `indexes` | array\<object\> | No | Array of index definitions to create. Each index should contain: key (string), type (string: key, fulltext, unique, spatial), attributes (array of column keys), orders (array of ASC/DESC, optional), and lengths (array of integers, optional). (default: `[]`) |

**Response:** `table`

## Get table

`getTable`
Get a table by its unique ID. This endpoint response returns a JSON object with the table metadata.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |

**Response:** `table`

## Update table

`updateTable`
Update a table by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `name` | string | No | Table name. Max length: 128 chars. |
| `permissions` | array\<string\> | No | An array of permission strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `rowSecurity` | boolean | No | Enables configuring permissions for individual rows. A user needs one of row or table-level permissions to access a row. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `enabled` | boolean | No | Is table enabled? When set to &#039;disabled&#039;, users cannot access the table but Server SDKs with and API key can still read and write to the table. No data is lost when this is toggled. (default: `1`) |

**Response:** `table`

## Delete table

`deleteTable`
Delete a table by its unique ID. Only users with write permissions have access to delete this resource.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |


## List columns

`listColumns`
List columns in the table.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following columns: key, type, size, required, array, status, error (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `columnList`

## Create boolean column

`createBooleanColumn`
Create a boolean column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | boolean | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnBoolean`

## Update boolean column

`updateBooleanColumn`
Update a boolean column. Changing the `default` value will not update already existing rows.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | boolean | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnBoolean`

## Create datetime column

`createDatetimeColumn`
Create a date time column according to the ISO 8601 standard.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for the column in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnDatetime`

## Update dateTime column

`updateDatetimeColumn`
Update a date time column. Changing the `default` value will not update already existing rows.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnDatetime`

## Create email column

`createEmailColumn`
Create an email column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnEmail`

## Update email column

`updateEmailColumn`
Update an email column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnEmail`

## Create enum column

`createEnumColumn`
Create an enumeration column. The `elements` param acts as a white-list of accepted values for this column.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `elements` | array\<string\> | Yes | Array of enum values. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnEnum`

## Update enum column

`updateEnumColumn`
Update an enum column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `elements` | array\<string\> | Yes | Updated list of enum values. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnEnum`

## Create float column

`createFloatColumn`
Create a float column. Optionally, minimum and maximum values can be provided.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `min` | number | No | Minimum value |
| `max` | number | No | Maximum value |
| `default` | number | No | Default value. Cannot be set when required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnFloat`

## Update float column

`updateFloatColumn`
Update a float column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | number | Yes | Default value. Cannot be set when required. |
| `min` | number | No | Minimum value |
| `max` | number | No | Maximum value |
| `newKey` | string | No | New Column Key. |

**Response:** `columnFloat`

## Create integer column

`createIntegerColumn`
Create an integer column. Optionally, minimum and maximum values can be provided.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `min` | integer | No | Minimum value |
| `max` | integer | No | Maximum value |
| `default` | integer | No | Default value. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnInteger`

## Update integer column

`updateIntegerColumn`
Update an integer column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | integer | Yes | Default value. Cannot be set when column is required. |
| `min` | integer | No | Minimum value |
| `max` | integer | No | Maximum value |
| `newKey` | string | No | New Column Key. |

**Response:** `columnInteger`

## Create IP address column

`createIpColumn`
Create IP address column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnIp`

## Update IP address column

`updateIpColumn`
Update an ip column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnIp`

## Create line column

`createLineColumn`
Create a geometric line column.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | array | No | Default value for column when not provided, two-dimensional array of coordinate pairs, [[longitude, latitude], [longitude, latitude], …], listing the vertices of the line in order. Cannot be set when column is required. |

**Response:** `columnLine`

## Update line column

`updateLineColumn`
Update a line column. Changing the `default` value will not update already existing rows.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | array | No | Default value for column when not provided, two-dimensional array of coordinate pairs, [[longitude, latitude], [longitude, latitude], …], listing the vertices of the line in order. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnLine`

## Create longtext column

`createLongtextColumn`
Create a longtext column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnLongtext`

## Update longtext column

`updateLongtextColumn`
Update a longtext column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnLongtext`

## Create mediumtext column

`createMediumtextColumn`
Create a mediumtext column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnMediumtext`

## Update mediumtext column

`updateMediumtextColumn`
Update a mediumtext column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnMediumtext`

## Create point column

`createPointColumn`
Create a geometric point column.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | array | No | Default value for column when not provided, array of two numbers [longitude, latitude], representing a single coordinate. Cannot be set when column is required. |

**Response:** `columnPoint`

## Update point column

`updatePointColumn`
Update a point column. Changing the `default` value will not update already existing rows.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | array | No | Default value for column when not provided, array of two numbers [longitude, latitude], representing a single coordinate. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnPoint`

## Create polygon column

`createPolygonColumn`
Create a geometric polygon column.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | array | No | Default value for column when not provided, three-dimensional array where the outer array holds one or more linear rings, [[[longitude, latitude], …], …], the first ring is the exterior boundary, any additional rings are interior holes, and each ring must start and end with the same coordinate pair. Cannot be set when column is required. |

**Response:** `columnPolygon`

## Update polygon column

`updatePolygonColumn`
Update a polygon column. Changing the `default` value will not update already existing rows.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | array | No | Default value for column when not provided, three-dimensional array where the outer array holds one or more linear rings, [[[longitude, latitude], …], …], the first ring is the exterior boundary, any additional rings are interior holes, and each ring must start and end with the same coordinate pair. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnPolygon`

## Create relationship column

`createRelationshipColumn`
Create relationship column. [Learn more about relationship columns](https://appwrite.io/docs/databases-relationships#relationship-columns).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `relatedTableId` | string | Yes | Related Table ID. |
| `type` | string | Yes | Relation type |
| `twoWay` | boolean | No | Is Two Way? |
| `key` | string | No | Column Key. |
| `twoWayKey` | string | No | Two Way Column Key. |
| `onDelete` | string | No | Constraints option (default: `restrict`) |

**Response:** `columnRelationship`

## Create string column

`createStringColumn` **(DEPRECATED — use `tablesDB.createTextColumn` instead)**
Create a string column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `size` | integer | Yes | Column size for text columns, in number of characters. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |
| `encrypt` | boolean | No | Toggle encryption for the column. Encryption enhances security by not storing any plain text values in the database. However, encrypted columns cannot be queried. |

**Response:** `columnString`

## Update string column

`updateStringColumn` **(DEPRECATED — use `tablesDB.updateTextColumn` instead)**
Update a string column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `size` | integer | No | Maximum size of the string column. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnString`

## Create text column

`createTextColumn`
Create a text column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnText`

## Update text column

`updateTextColumn`
Update a text column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnText`

## Create URL column

`createUrlColumn`
Create a URL column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnUrl`

## Update URL column

`updateUrlColumn`
Update an url column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnUrl`

## Create varchar column

`createVarcharColumn`
Create a varchar column.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `size` | integer | Yes | Column size for varchar columns, in number of characters. Maximum size is 16381. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | No | Default value for column when not provided. Cannot be set when column is required. |
| `array` | boolean | No | Is column an array? |

**Response:** `columnVarchar`

## Update varchar column

`updateVarcharColumn`
Update a varchar column. Changing the `default` value will not update already existing rows.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Column Key. |
| `required` | boolean | Yes | Is column required? |
| `default` | string | Yes | Default value for column when not provided. Cannot be set when column is required. |
| `size` | integer | No | Maximum size of the varchar column. |
| `newKey` | string | No | New Column Key. |

**Response:** `columnVarchar`

## Get column

`getColumn`
Get column by ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |

**Response:** `columnBoolean`

## Delete column

`deleteColumn`
Deletes a column.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |


## Update relationship column

`updateRelationshipColumn`
Update relationship column. [Learn more about relationship columns](https://appwrite.io/docs/databases-relationships#relationship-columns).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `key` | string | Yes | Column Key. |
| `onDelete` | string | No | Constraints option |
| `newKey` | string | No | New Column Key. |

**Response:** `columnRelationship`

## List indexes

`listIndexes`
List indexes on the table.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following columns: key, type, status, attributes, error (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `columnIndexList`

## Create index

`createIndex`
Creates an index on the columns listed. Your index should include all the columns you will query in a single request.
Type can be `key`, `fulltext`, or `unique`.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Index Key. |
| `type` | string | Yes | Index type. |
| `columns` | array\<string\> | Yes | Array of columns to index. Maximum of 100 columns are allowed, each 32 characters long. |
| `orders` | array\<string\> | No | Array of index orders. Maximum of 100 orders are allowed. (default: `[]`) |
| `lengths` | array\<integer\> | No | Length of index. Maximum of 100 (default: `[]`) |

**Response:** `columnIndex`

## Get index

`getIndex`
Get index by ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Index Key. |

**Response:** `columnIndex`

## Delete index

`deleteIndex`
Delete an index.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `key` | string | Yes | Index Key. |


## List table logs

`listTableLogs`
Get the table activity logs list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |

**Response:** `logList`

## List rows

`listRows`
Get a list of all the user&#039;s rows in a given table. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the TablesDB service [server integration](https://appwrite.io/docs/products/databases/tables#create-table). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID to read uncommitted changes within the transaction. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `rowList`

## createRow

`createRow`
Create a new Row. Before using this route, you should create a new table resource using either a [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). Make sure to define columns before creating rows. |
| `rowId` | string | Yes | Row ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `data` | object | Yes | Row data as JSON object. (default: `{}`) |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, only the current user is granted all permissions. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `row`

## createRows

`createRows`
Create new Rows. Before using this route, you should create a new table resource using either a [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). Make sure to define columns before creating rows. |
| `rows` | array\<object\> | Yes | Array of rows data as JSON objects. (default: `[]`) |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `rowList`

## upsertRows

`upsertRows`
Create or update Rows. Before using this route, you should create a new table resource using either a [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable) API or directly from your database console.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `rows` | array\<object\> | Yes | Array of row data as JSON objects. May contain partial rows. |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `rowList`

## Update rows

`updateRows`
Update all rows that match your queries, if no queries are submitted then all rows are updated. You can pass only specific fields to be updated.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `data` | object | No | Row data as JSON object. Include only column and value pairs to be updated. (default: `{}`) |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `rowList`

## Delete rows

`deleteRows`
Bulk delete rows using queries, if no queries are passed then all rows are deleted.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `rowList`

## Get row

`getRow`
Get a row by its unique ID. This endpoint response returns a JSON object with the row data.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `rowId` | string | Yes | Row ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. (default: `[]`) |
| `transactionId` | string | No | Transaction ID to read uncommitted changes within the transaction. |

**Response:** `row`

## upsertRow

`upsertRow`
Create or update a Row. Before using this route, you should create a new table resource using either a [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable) API or directly from your database console.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `rowId` | string | Yes | Row ID. |
| `data` | object | No | Row data as JSON object. Include all required columns of the row to be created or updated. (default: `{}`) |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `row`

## Update row

`updateRow`
Update a row by its unique ID. Using the patch method you can pass only specific fields that will get updated.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `rowId` | string | Yes | Row ID. |
| `data` | object | No | Row data as JSON object. Include only columns and value pairs to be updated. (default: `{}`) |
| `permissions` | array\<string\> | No | An array of permissions strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `row`

## Delete row

`deleteRow`
Delete a row by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. You can create a new table using the Database service [server integration](https://appwrite.io/docs/references/cloud/server-dart/tablesDB#createTable). |
| `rowId` | string | Yes | Row ID. |
| `transactionId` | string | No | Transaction ID for staging the operation. |


## List row logs

`listRowLogs`
Get the row activity logs list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `rowId` | string | Yes | Row ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |

**Response:** `logList`

## Decrement row column

`decrementRowColumn`
Decrement a specific column of a row by a given value.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `rowId` | string | Yes | Row ID. |
| `column` | string | Yes | Column key. |
| `value` | number | No | Value to increment the column by. The value must be a number. (default: `1`) |
| `min` | number | No | Minimum value for the column. If the current value is lesser than this value, an exception will be thrown. |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `row`

## Increment row column

`incrementRowColumn`
Increment a specific column of a row by a given value.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `rowId` | string | Yes | Row ID. |
| `column` | string | Yes | Column key. |
| `value` | number | No | Value to increment the column by. The value must be a number. (default: `1`) |
| `max` | number | No | Maximum value for the column. If the current value is greater than this value, an error will be thrown. |
| `transactionId` | string | No | Transaction ID for staging the operation. |

**Response:** `row`

## Get table usage stats

`getTableUsage`
Get usage metrics and statistics for a table. Returning the total number of rows. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `tableId` | string | Yes | Table ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageTable`

## getUsage

`getUsage`
Get usage metrics and statistics for a database. You can view the total number of tables, rows, and storage usage. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `databaseId` | string | Yes | Database ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageDatabase`


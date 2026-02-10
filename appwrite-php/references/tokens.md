# Tokens



## List tokens

`list`
List all the tokens created for a specific file or bucket. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File unique ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: expire (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `resourceTokenList`

## Create file token

`createFileToken`
Create a new token. A token is linked to a file. Token can be passed as a request URL search parameter.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File unique ID. |
| `expire` | string | No | Token expiry date |

**Response:** `resourceToken`

## Get token

`get`
Get a token by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `tokenId` | string | Yes | Token ID. |

**Response:** `resourceToken`

## Update token

`update`
Update a token by its unique ID. Use this endpoint to update a token&#039;s expiry date.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `tokenId` | string | Yes | Token unique ID. |
| `expire` | string | No | File token expiry date |

**Response:** `resourceToken`

## Delete token

`delete`
Delete a token by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `tokenId` | string | Yes | Token ID. |



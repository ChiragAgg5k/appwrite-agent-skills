# Storage

The Storage service allows you to manage your project files.

## List buckets

`listBuckets`
Get a list of all the storage buckets. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: enabled, name, fileSecurity, maximumFileSize, encryption, antivirus, transformations (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `bucketList`

## Create bucket

`createBucket`
Create a new storage bucket.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Bucket name |
| `permissions` | array\<string\> | No | An array of permission strings. By default, no user is granted with any permissions. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `fileSecurity` | boolean | No | Enables configuring permissions for individual file. A user needs one of file or bucket level permissions to access a file. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `enabled` | boolean | No | Is bucket enabled? When set to &#039;disabled&#039;, users cannot access the files in this bucket but Server SDKs with and API key can still access the bucket. No files are lost when this is toggled. (default: `1`) |
| `maximumFileSize` | integer | No | Maximum file size allowed in bytes. Maximum allowed value is 30MB. (default: `[]`) |
| `allowedFileExtensions` | array\<string\> | No | Allowed file extensions. Maximum of 100 extensions are allowed, each 64 characters long. (default: `[]`) |
| `compression` | string | No | Compression algorithm chosen for compression. Can be one of none,  [gzip](https://en.wikipedia.org/wiki/Gzip), or [zstd](https://en.wikipedia.org/wiki/Zstd), For file size above 20MB compression is skipped even if it&#039;s enabled (default: `none`) |
| `encryption` | boolean | No | Is encryption enabled? For file size above 20MB encryption is skipped even if it&#039;s enabled (default: `1`) |
| `antivirus` | boolean | No | Is virus scanning enabled? For file size above 20MB AntiVirus scanning is skipped even if it&#039;s enabled (default: `1`) |
| `transformations` | boolean | No | Are image transformations enabled? (default: `1`) |

**Response:** `bucket`

## Get bucket

`getBucket`
Get a storage bucket by its unique ID. This endpoint response returns a JSON object with the storage bucket metadata.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Bucket unique ID. |

**Response:** `bucket`

## Update bucket

`updateBucket`
Update a storage bucket by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Bucket unique ID. |
| `name` | string | Yes | Bucket name |
| `permissions` | array\<string\> | No | An array of permission strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `fileSecurity` | boolean | No | Enables configuring permissions for individual file. A user needs one of file or bucket level permissions to access a file. [Learn more about permissions](https://appwrite.io/docs/permissions). |
| `enabled` | boolean | No | Is bucket enabled? When set to &#039;disabled&#039;, users cannot access the files in this bucket but Server SDKs with and API key can still access the bucket. No files are lost when this is toggled. (default: `1`) |
| `maximumFileSize` | integer | No | Maximum file size allowed in bytes. Maximum allowed value is 30MB. (default: `[]`) |
| `allowedFileExtensions` | array\<string\> | No | Allowed file extensions. Maximum of 100 extensions are allowed, each 64 characters long. (default: `[]`) |
| `compression` | string | No | Compression algorithm chosen for compression. Can be one of none, [gzip](https://en.wikipedia.org/wiki/Gzip), or [zstd](https://en.wikipedia.org/wiki/Zstd), For file size above 20MB compression is skipped even if it&#039;s enabled (default: `none`) |
| `encryption` | boolean | No | Is encryption enabled? For file size above 20MB encryption is skipped even if it&#039;s enabled (default: `1`) |
| `antivirus` | boolean | No | Is virus scanning enabled? For file size above 20MB AntiVirus scanning is skipped even if it&#039;s enabled (default: `1`) |
| `transformations` | boolean | No | Are image transformations enabled? (default: `1`) |

**Response:** `bucket`

## Delete bucket

`deleteBucket`
Delete a storage bucket by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Bucket unique ID. |


## List files

`listFiles`
Get a list of all the user files. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, signature, mimeType, sizeOriginal, chunksTotal, chunksUploaded (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `fileList`

## Create file

`createFile`
Create a new file. Before using this route, you should create a new bucket resource using either a [server integration](https://appwrite.io/docs/server/storage#storageCreateBucket) API or directly from your Appwrite console.

Larger files should be uploaded using multiple requests with the [content-range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Range) header to send a partial request with a maximum supported chunk of `5MB`. The `content-range` header values should always be in bytes.

When the first request is sent, the server will return the **File** object, and the subsequent part request must include the file&#039;s **id** in `x-appwrite-id` header to allow the server to know that the partial upload is for the existing file and not for a new one.

If you&#039;re creating a new file using one of the Appwrite SDKs, all the chunking logic will be managed by the SDK internally.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `file` | file | Yes | Binary file. Appwrite SDKs provide helpers to handle file input. [Learn about file input](https://appwrite.io/docs/products/storage/upload-download#input-file). |
| `permissions` | array\<string\> | No | An array of permission strings. By default, only the current user is granted all permissions. [Learn more about permissions](https://appwrite.io/docs/permissions). |

**Response:** `file`

## Get file

`getFile`
Get a file by its unique ID. This endpoint response returns a JSON object with the file metadata.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID. |

**Response:** `file`

## Update file

`updateFile`
Update a file by its unique ID. Only users with write permissions have access to update this resource.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Bucket unique ID. |
| `fileId` | string | Yes | File ID. |
| `name` | string | No | File name. |
| `permissions` | array\<string\> | No | An array of permission strings. By default, the current permissions are inherited. [Learn more about permissions](https://appwrite.io/docs/permissions). |

**Response:** `file`

## Delete file

`deleteFile`
Delete a file by its unique ID. Only users with write permissions have access to delete this resource.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID. |


## Get file for download

`getFileDownload`
Get a file content by its unique ID. The endpoint response return with a &#039;Content-Disposition: attachment&#039; header that tells the browser to start downloading the file to user downloads directory.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID. |
| `token` | string | No | File token for accessing this file. |


## Get file preview

`getFilePreview`
Get a file preview image. Currently, this method supports preview for image files (jpg, png, and gif), other supported formats, like pdf, docs, slides, and spreadsheets, will return the file icon image. You can also pass query string arguments for cutting and resizing your preview image. Preview is supported only for image files smaller than 10MB.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID |
| `width` | integer | No | Resize preview image width, Pass an integer between 0 to 4000. (default: `0`) |
| `height` | integer | No | Resize preview image height, Pass an integer between 0 to 4000. (default: `0`) |
| `gravity` | string | No | Image crop gravity. Can be one of center,top-left,top,top-right,left,right,bottom-left,bottom,bottom-right (default: `center`) |
| `quality` | integer | No | Preview image quality. Pass an integer between 0 to 100. Defaults to keep existing image quality. (default: `-1`) |
| `borderWidth` | integer | No | Preview image border in pixels. Pass an integer between 0 to 100. Defaults to 0. (default: `0`) |
| `borderColor` | string | No | Preview image border color. Use a valid HEX color, no # is needed for prefix. |
| `borderRadius` | integer | No | Preview image border radius in pixels. Pass an integer between 0 to 4000. (default: `0`) |
| `opacity` | number | No | Preview image opacity. Only works with images having an alpha channel (like png). Pass a number between 0 to 1. (default: `1`) |
| `rotation` | integer | No | Preview image rotation in degrees. Pass an integer between -360 and 360. (default: `0`) |
| `background` | string | No | Preview image background color. Only works with transparent images (png). Use a valid HEX color, no # is needed for prefix. |
| `output` | string | No | Output format type (jpeg, jpg, png, gif and webp). |
| `token` | string | No | File token for accessing this file. |


## Get file for view

`getFileView`
Get a file content by its unique ID. This endpoint is similar to the download method but returns with no  &#039;Content-Disposition: attachment&#039; header.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Storage bucket unique ID. You can create a new storage bucket using the Storage service [server integration](https://appwrite.io/docs/server/storage#createBucket). |
| `fileId` | string | Yes | File ID. |
| `token` | string | No | File token for accessing this file. |


## Get storage usage stats

`getUsage`
Get usage metrics and statistics for all buckets in the project. You can view the total number of buckets, files, storage usage. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageStorage`

## Get bucket usage stats

`getBucketUsage`
Get usage metrics and statistics a specific bucket in the project. You can view the total number of files, storage usage. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bucketId` | string | Yes | Bucket ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageBuckets`


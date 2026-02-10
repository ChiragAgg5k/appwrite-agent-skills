# Vcs



## Create repository detection

`createRepositoryDetection`
Analyze a GitHub repository to automatically detect the programming language and runtime environment. This endpoint scans the repository&#039;s files and language statistics to determine the appropriate runtime settings for your function. The GitHub installation must be properly configured and the repository must be accessible through your installation for this endpoint to work.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `providerRepositoryId` | string | Yes | Repository Id |
| `type` | string | Yes | Detector type. Must be one of the following: runtime, framework |
| `providerRootDirectory` | string | No | Path to Root Directory |

**Response:** `detectionFramework`

## List repositories

`listRepositories`
Get a list of GitHub repositories available through your installation. This endpoint returns repositories with their basic information, detected runtime environments, and latest push dates. You can optionally filter repositories using a search term. Each repository&#039;s runtime is automatically detected based on its contents and language statistics. The GitHub installation must be properly configured for this endpoint to work.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `type` | string | Yes | Detector type. Must be one of the following: runtime, framework |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |

**Response:** `providerRepositoryFrameworkList`

## Create repository

`createRepository`
Create a new GitHub repository through your installation. This endpoint allows you to create either a public or private repository by specifying a name and visibility setting. The repository will be created under your GitHub user account or organization, depending on your installation type. The GitHub installation must be properly configured and have the necessary permissions for repository creation.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `name` | string | Yes | Repository name (slug) |
| `private` | boolean | Yes | Mark repository public or private |

**Response:** `providerRepository`

## Get repository

`getRepository`
Get detailed information about a specific GitHub repository from your installation. This endpoint returns repository details including its ID, name, visibility status, organization, and latest push date. The GitHub installation must be properly configured and have access to the requested repository for this endpoint to work.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `providerRepositoryId` | string | Yes | Repository Id |

**Response:** `providerRepository`

## List repository branches

`listRepositoryBranches`
Get a list of all branches from a GitHub repository in your installation. This endpoint returns the names of all branches in the repository and their total count. The GitHub installation must be properly configured and have access to the requested repository for this endpoint to work.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `providerRepositoryId` | string | Yes | Repository Id |

**Response:** `branchList`

## Get files and directories of a VCS repository

`getRepositoryContents`
Get a list of files and directories from a GitHub repository connected to your project. This endpoint returns the contents of a specified repository path, including file names, sizes, and whether each item is a file or directory. The GitHub installation must be properly configured and the repository must be accessible through your installation for this endpoint to work.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `providerRepositoryId` | string | Yes | Repository Id |
| `providerRootDirectory` | string | No | Path to get contents of nested directory |
| `providerReference` | string | No | Git reference (branch, tag, commit) to get contents from |

**Response:** `vcsContentList`

## Update external deployment (authorize)

`updateExternalDeployments`
Authorize and create deployments for a GitHub pull request in your project. This endpoint allows external contributions by creating deployments from pull requests, enabling preview environments for code review. The pull request must be open and not previously authorized. The GitHub installation must be properly configured and have access to both the repository and pull request for this endpoint to work.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |
| `repositoryId` | string | Yes | VCS Repository Id |
| `providerPullRequestId` | string | Yes | GitHub Pull Request Id |


## List installations

`listInstallations`
List all VCS installations configured for the current project. This endpoint returns a list of installations including their provider, organization, and other configuration details.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: provider, organization (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `installationList`

## Get installation

`getInstallation`
Get a VCS installation by its unique ID. This endpoint returns the installation&#039;s details including its provider, organization, and configuration. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |

**Response:** `installation`

## Delete installation

`deleteInstallation`
Delete a VCS installation by its unique ID. This endpoint removes the installation and all its associated repositories from the project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `installationId` | string | Yes | Installation Id |



---
title: Data Sources API
description: Use Analytics Data Sources APIs to manage accounts and upload data.
---

# Data Sources Guide

The Analytics 2.0 Data Sources API endpoints provide methods for you to create, delete, and view Data Sources accounts and perform and view data uploads to Data Sources accounts. See the [Data Sources overview](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/overview) for more information regarding the Data Sources service and functions.

The endpoints described in this guide are routed through `analytics.adobe.io`. To use them, you must first create a client with access to the Adobe Developer Console. For more information, see [Getting started with the Analytics API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/) for more information.

**Data Sources Accounts**

These endpoints provide methods for viewing, creating, and deleting Data Sources accounts

* GET retrieve all accounts: Retrieves all Data Sources accounts for a given RSID
* GET retrieve a single account: Retrieves a single Data Sources account by ID
* POST create an account: Create a Data Sources account
* DELETE account: Deletes a Data Sources account

**Data Sources Jobs**

These endpoints provide methods for uploading data to a Data Source account and viewing previous uploads

* PUT upload data: Uploads a file to a Data Sources account
* GET retrieve all jobs: Retrieves all jobs associated with a Data Sources account
* GET retrieve a single job: Retrieves a single job by ID

<InlineAlert variant="info" slots="text" />

Adobe may add optional request and response members (name/value pairs) to existing API objects at any time and without notice or changes in versioning. Adobe recommends that you refer to the API documentation of any third-party tool you integrate with our APIs so that such additions are ignored in processing if not understood. If implemented properly, such additions are non-breaking changes for your implementation. Adobe will not remove parameters or add required parameters without first providing standard notification through release notes.

## GET retrieve all accounts

Use this endpoint to retrieve all Data Sources accounts for a given report suite ID. For more information regarding Data Sources accounts, see the [Getting started with data sources](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/getting-started) guide.

`GET https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/account/{REPORT_SUITE_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'GET' \
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/data_sources/account/{REPORT_SUITE_ID}" \
  -H "accept: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
```

#### Response

```json
[
  {
    "name": "Account 1",
    "email": "noreply@mycompany.com",
    "data_source_id": 1,
    "type": "generic",
    "ftp_hostname": "ftp.omniture.com",
    "ftp_username": "my_username",
    "ftp_password": "3z1475tf"
  },
  {
    "name": "Account 2",
    "email": "noreply@mycompany.com",
    "data_source_id": 2,
    "type": "generic",
    "ftp_hostname": "ftp.omniture.com",
    "ftp_username": "my_username",
    "ftp_password": "85txc712"
  }
]
```

#### Request example details

The example above requests all Data Sources accounts for `{REPORT_SUITE_ID}`.

#### Response example details

The example above returns the accounts with the following details:

* Two accounts named `Account 1` and `Account 2` belong to the `{REPORT_SUITE_ID}`.
* Each account has an `ftp_username` and `ftp_password` for use in the [Data Sources manager](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/manage).

### Request Parameters

The following table describes the retrieve Data Sources accounts request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID to retrieve Data Sources accounts for |

### Response Parameters

The following table describes the retrieve Data Sources accounts response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the Data Sources account |
| `email` | string | The email address to recieve notifications regarding this Data Sources account |
| `data_source_id` | integer | The ID of the data source |
| `type` | string | The type of data associated with the account |
| `ftp_hostname` | string | The FTP host address |
| `ftp_username` | string | The FTP username |
| `ftp_password` | string | The FTP password |

## GET retrieve a single account

Use this endpoint to retrieve information about a single Data Sources account. For more information regarding Data Sources accounts, see the [Getting started with data sources](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/getting-started) guide.

`GET https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/account/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'GET' \
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/data_sources/account/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}" \
  -H "accept: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
```

#### Response

```json
{
  "name": "My Data Sources Account",
  "email": "noreply@mycompany.com",
  "data_source_id": 1,
  "type": "generic",
  "ftp_hostname": "ftp.omniture.com",
  "ftp_username": "my_username",
  "ftp_password": "3z1475tf"
}
```

#### Request example details

The example above requests the Data Sources account associated with the given `DATA_SOURCE_ID`.

#### Response example details

The example above returns the account with the following details:

* The account is named `My Data Sources Account`.
* The account has a `data_source_id` of `1`.
* The account has an `ftp_username` and `ftp_password` for use in the [Data Sources manager](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/manage).

### Request Parameters

The following table describes the retrieve a single Data Sources account request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID associated with the Data Sources account |
| `data_source_id` | required | string | The Data Source ID of the account to retrieve |

### Response Parameters

The following table describes the retrieve a single Data Sources account response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the Data Sources account |
| `email` | string | The email address to recieve notifications regarding this Data Sources account |
| `data_source_id` | integer | The data source ID |
| `type` | string | The type of data associated with the account |
| `ftp_hostname` | string | The FTP host address |
| `ftp_username` | string | The FTP username |
| `ftp_password` | string | The FTP password |

## POST create an account

Use this endpoint to creata a Data Sources account. For more information regarding Data Sources accounts, see the [Getting started with data sources](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/getting-started) guide.

`POST https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/account/{REPORT_SUITE_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'POST' \
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/data_sources/account/{REPORT_SUITE_ID}?type=generic&name=My%20Data%20Sources%20Account&email=noreply%40mycompany.com" \
  -H "accept: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
```

#### Response

```json
{
  "name": "My Data Sources Account",
  "email": "noreply@mycompany.com",
  "data_source_id": 1,
  "type": "generic",
  "ftp_hostname": "ftp.omniture.com",
  "ftp_username": "my_username",
  "ftp_password": "3z1475tf"
}
```

#### Request example details

The example above requests to create an account with the following details:

* The account `type` is `generic`.
* The account `name` is `My Data Sources Account`. Note that query parameters cannot contain true "space" characters, and must be replaced with `%20` as shown in the example.
* The `email` where notifications are sent is `noreply@mycompany.com`. Note that query parameters cannot contain true `@` characters, and must be replaced with `%40` as shown in the example.

#### Response example details

The example above responds with the following details:

* The account `name` is `My Data Sources Account`.
* The `email` where notifications are sent is `noreply@mycompany.com`.
* The `data_source_id` is `1`.
* The account has an `ftp_username` and `ftp_password` for use in the [Data Sources manager](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/manage).

### Request Parameters

The following table describes the create a Data Sources account request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID the new account will belong to |
| `type` | optional | string | The type of data associated with the account |
| `name` | optional | string | The name of the Data Sources account |
| `email` | optional | string | The email address to recieve notifications regarding this Data Sources account |

### Response Parameters

The following table describes the create a Data Sources account response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the Data Sources account |
| `email` | string | The email address to recieve notifications regarding this Data Sources account |
| `data_source_id` | integer | The data source ID |
| `type` | string | The type of data associated with the account |
| `ftp_hostname` | string | The FTP host address |
| `ftp_username` | string | The FTP username |
| `ftp_password` | string | The FTP password |

## DELETE account

Use this endpoint to delete a Data Sources account. This action cannot be undone. For more information regarding Data Sources accounts, see the [Getting started with data sources](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/getting-started) guide.

`DELETE https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/account/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'DELETE' \
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/data_sources/account/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}" \
  -H "accept: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
```

#### Response

```json
{
  "success": true,
  "message": "Operation successful"
}
```

#### Request example details

The example above requests to `DELETE` the Data Sources account with the corresponding `DATA_SOURCE_ID`.

#### Response example details

The example above responds the deletion was successful.

### Request Parameters

The following table describes the DELETE Data Sources account request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID associated with the Data Sources account |
| `data_source_id` | required | string | The data source ID of the account to delete |

### Response Parameters

The following table describes the DELETE Data Sources account response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `success` | boolean | Whether the delete succeeded |
| `message` | string | Message regarding the status of the operation |

## PUT upload data

Use this endpoint to upload a data file to a Data Sources account. Data files must be uploaded in the methods described in the [Upload data sources file to Adobe](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/file-upload) guide.

`PUT https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/job/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'PUT'
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/job/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -d '{
  "contentType": "string",
  "originalFilename": "string",
  "name": "string",
  "bytes": [
    "string"
  ],
  "empty": true,
  "resource": {
    "file": "string",
    "uri": "string",
    "url": "string",
    "description": "string",
    "readable": true,
    "filename": "string",
    "open": true,
    "inputStream": {}
  },
  "size": 0,
  "inputStream": {}
}'
```

#### Response

```json
{
  "Filename": "my_data_file.txt",
  "The number of rows successfully processed": 100,
  "Job ID": 12345,
  "Status of the job": "processing",
  "Date the job was created": "1/1/2024 00:00:00",
  "Date the job began processing": "1/1/2024 00:00:00",
  "Date the job finished processing": "1/1/2024 00:00:00"
}
```

#### Request example details

#### Response example details

### Request Parameters

The following table describes the upload data request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID associated with the Data Sources account |
| `data_source_id` | required | string | The Data Source ID of the account to receive the file |
| `contentType` |  | string |  |
| `originalFilename` |  | string |  |
| `name` |  | string |  |
| `bytes` |  | string |  |
| `empty` |  | boolean | Whether the file is empty |
| `resource` |  | container | Information regarding the file to upload. Contains the `file`, `uri`, `url`, `description`, `readable`, `filename`, `open`, and `inputStream` parameters. |
| `file` |  | string |  |
| `uri` |  | string |  |
| `url` |  | string |  |
| `description` |  | string | Description of the file |
| `readable` |  | boolean |  |
| `filename` |  | string |  |
| `open` |  | boolean |  |
| `inputStream` |  |  |  |
| `size` |  | integer |  |
| `inputStream` |  |  |  |

### Response Parameters

The following table describes the upload data response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `Filename` | string | The filename of the file ingested by the Data Sources job |
| `The number of rows successfully processed` | integer | The number of rows successfully processed by the Data Sources job |
| `Job ID` | integer | The Data Source job ID |
| `Status of the job` | string | The status of the Data Source job |
| `Date the job was created` | string | The date the Data Source job was created |
| `Date the job began processing` | string | The date the Data Source job began processing |
| `Date the job finished processing` | string | The date the Data Source job finished processing |

## GET retrieve all jobs

Use this endpoint to retrieve all jobs associated with a Data Sources account.

`GET https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/job/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'GET' \
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/job/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}" \
  -H "accept: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
```

#### Response

```json
{
  "page": 1,
  "jobs": [
    {
      "Filename": "my_data_file.txt",
      "The number of rows successfully processed": 100,
      "Job ID": 12345,
      "Status of the job": "processing",
      "Date the job was created": "1/1/YYYY 00:00:00",
      "Date the job began processing": "1/1/YYYY 00:00:00",
      "Date the job finished processing": "1/1/YYYY 00:00:00"
    },
    {
      "Filename": "my_data_file.fin",
      "The number of rows successfully processed": 0,
      "Job ID": 67890,
      "Status of the job": "processing",
      "Date the job was created": "1/1/YYYY 01:00:00",
      "Date the job began processing": "1/1/YYYY 01:00:00",
      "Date the job finished processing": "1/1/YYYY 01:00:00"
    }
  ],
  "total_pages": 1
}
```

#### Request example details

#### Response example details

### Request Parameters

The following table describes the retrieve all jobs request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID associated with the Data Sources account |
| `data_source_id` | required | string | The data source ID of the account to retrieve jobs from |
| `status` | optional | string | Filters search by job status |
| `start_date` | optional | string | How far back to begin the search. Should be earlier than `end_date`. Defaults to one month ago. Should be formatted as "yyyy-mm-dd hh:mm:ss". |
| `end_date` | optional | string | How far back to end the search. Should be more recent than `start_date`. Defaults to today. Should be formatted as "yyyy-mm-dd hh:mm:ss". |
| `page` | optional | string | Which page of the results to retrieve. Page `1` is the first page. If this value exceeds the available pages, no results will be returned. |

### Response Parameters

The following table describes the retrieve all jobs response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `page` | integer | Which page of the results was retrieved. Page `1` is the first page. |
| `jobs` | container | The jobs retrieved in the search. Contains the `Filename`, `The number of rows successfully processed`, `Job ID`, `Status of the job`, `Date the job was created`, `Date the job began processing`, and `Date the job finished processing` parameters. |
| `Filename` | string | The filename of the file ingested by the Data Sources job |
| `The number of rows successfully processed` | integer | The number of rows successfully processed by the Data Sources job |
| `Job ID` | integer | The data source job ID |
| `Status of the job` | string | The status of the data source job |
| `Date the job was created` | string | The date the data source job was created |
| `Date the job began processing` | string | The date the data source job began processing |
| `Date the job finished processing` | string | The date the data source job finished processing |
| `total_pages` | integer | The total number of pages returned by the search |

## GET retrieve a single job

Use this endpoint to retrieve information regarding a single job by its job ID.

`GET https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/datasources/job/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}/{JOB_ID}`

### Request and Response Examples

Click the **Request** tab in the following example to see a cURL request for this endpoint. Click the **Response** tab to see a successful JSON response for the request.

<CodeBlock slots="heading, code" repeat="2" languages="CURL,JSON"/>

#### Request

```sh
curl -X 'GET' \
  "https://analytics.adobe.io/api/{GLOBAL_COMPANY_ID}/job/{REPORT_SUITE_ID}/{DATA_SOURCE_ID}/{JOB_ID}" \
  -H "accept: application/json" \
  -H "x-api-key: {CLIENT_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
```

#### Response

```json
{
  "Filename": "my_data_file.txt",
  "The number of rows successfully processed": 100,
  "Job ID": 12345,
  "Status of the job": "processing",
  "Date the job was created": "1/1/2024 00:00:00",
  "Date the job began processing": "1/1/2024 00:00:00",
  "Date the job finished processing": "1/1/2024 00:00:00"
}
```

#### Request example details

#### Response example details

### Request Parameters

The following table describes the retrieve a single job request parameters:

| Name | Required | Type | Description |
| --- | --- | --- | --- |
| `report_suite_id` | required | string | The report suite ID associated with the Data Sources account |
| `data_source_id` | required | string | The data source ID associated with the job |
| `job_id` | required | string | The job ID of the job to retrieve |

### Response Parameters

The following table describes the retrieve a single job response parameters:

| Name | Type | Description |
| --- | --- | --- |
| `Filename` | string | The filename of the file ingested by the Data Sources job |
| `The number of rows successfully processed` | integer | The number of rows successfully processed by the Data Sources job |
| `Job ID` | integer | The data source job ID |
| `Status of the job` | string | The status of the data source job |
| `Date the job was created` | string | The date the data source job was created |
| `Date the job began processing` | string | The date the data source job began processing |
| `Date the job finished processing` | string | The date the data source job finished processing |

## Status codes

Each API request returns an HTTP status code that reflects the result, as follows:

| HTTP code | Meaning | Description |
| --- | --- | --- |
| 200 | Success | The request is successful. |
| 400 | Bad Request | The request was improperly constructed, missing key information, and/or contained incorrect syntax. This error code could indicate a problem such as a missing required parameter or the supplied data did not pass validation. |
| 401 | Authentication failed | The request did not pass an authentication check. Your access token may be missing or invalid. Similarly, you may have attempted to access an object that requires administrator permissions. |
| 403 | Forbidden | The resource was found, but you do not have the right credentials to view it. You might not have the required permissions to access or edit the resource for reasons not applicable to status code 401. |
| 404 | Not found | The requested resource could not be found on the server. The resource may have been deleted, or the requested path was entered incorrectly. |
| 500 | Internal server errors | This is a server-side error. If you are making many simultaneous calls, you may be reaching the API limit and need to filter your results. Wait for a moment before trying your request again, and contact your administrator if the problem persists. |

For more information, or for trouble-shooting help, see the following:

* [Data sources overview](https://experienceleague.adobe.com/en/docs/analytics/import/data-sources/overview).
* [API Status Codes](https://experienceleague.adobe.com/en/docs/experience-platform/landing/troubleshooting#api-status-codes).
* [API request error headers](https://experienceleague.adobe.com/en/docs/experience-platform/landing/troubleshooting#request-header-errors).

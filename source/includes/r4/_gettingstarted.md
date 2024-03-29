# Getting Started

All API requests are performed over HTTPS, and **must** use TLS 1.2. Although the [FHIR® standard](https://www.hl7.org/fhir/R4/index.html) supports both JSON and XML, this API currently only supports JSON. Therefore any type explicitly defined in the request's `Accept` header will be ignored.

Before you can access the Nextech API you must have the proper credentials for authorization. These credentials will be provided to you by your Nextech representative, and vary depending on how you wish to integrate with the Nextech API. There are two different authorization models available for accessing the Nextech API: [SMART App authorization](#smart-app-authorization), and [partner authorization](#partner-authorization). See each linked authorization section for more information on each, including how to register your application with the Nextech API and acquire the necessary credentials.

**Base API Endpoint**
`https://icp.nextech-api.com/`

**API Limitations**

- Users of the Nextech API are restricted to a rate limit of 20 requests per second per endpoint
- Nextech is not responsible for the development or maintenance of any third-party application

## Rate Limiting

Rate limiting of the API is primarily on a per-user, per-endpoint basis. The default rate limit of 20 requests per second per endpoint. When a user exceeds the rate limit for a given API endpoint, the API will reject the request and return a HTTP 429 “Too Many Requests” response code. The API rate limit is subjet to change.

**Handling 429 response codes**

If your API user exceeds the rate limit, you will receive a HTTP 429 response code. We advise to design to handle these requests with [Exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff).

**Best practices to avoid Rate Limiting**

- The API is intended for on-demand requests for user interaction in real-time, try to avoid synchronizing data.
- Requests should be staggered as much as possible to avoid bursts of high traffic volume.
- Cache your own data when you need to store specialized values or rapidly review very large data sets.
- Query with \_lastUpdated search parameters to avoid re-querying unmodified data.
- If you need to synchronize data, it is best to do so during non-peak business hours. Which vary on a per practice basis.

## Using Postman

You can use Postman to make a simple request to the [metadata](#metadata) endpoint:
&nbsp;

<pre class="center-column">
GET https://icp.nextech-api.com/metadata
</pre>

&nbsp;
Each `rest.resource` member in the metadata response contains information about all FHIR resources that are supported, along with the supported interactions and search parameters for each resource.

## Searching

Searches may be performed via HTTPS calls to the API where supported.

A search is executed by performing a `GET` operation in the RESTful framework
`GET https://icp.nextech-api.com/[type]?[field1][:modifier1]=[value1]&[field2][:modifier2]=[value2]...`
where \[type\] refers to a resource such as Patient or Immunization followed by one or more query filters and optional modifiers.

- Matching is always case-insensitive and always ignores whitespace before and after the data.
- The default search attempts to match with just the start of the data.

### Multiple Values on One Field

To search for a field that meets at least one of several values, each value should be specified and separated by a comma.

**Example: Get patients who live in several nearby cities**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?address-postalcode=33609,33625,33647
</pre>

&nbsp;

### Multiple Fields

To search for multiple fields that all must meet certain criteria, each field should be specified and separated by an ampersand.

**Example: Search for encounters for the patient with the id '9D0B7ADE-4B5B-41DD-8AC4-88DB4C93B192' that took place between and including 1/1/2022 through 11/14/2022**

<pre class="center-column">
GET https://icp.nextech-api.com/Encounter?patient=patient/9D0B7ADE-4B5B-41DD-8AC4-88DB4C93B192&date=ge2022-01-01&date=lt2022-11-14
</pre>

&nbsp;

### Modifiers

A modifier defines how a search match should be performed for a field. A modifier must appear after the field name with a preceeding colon followed by the modifier name.

| Modifier | Description                           |
| -------- | ------------------------------------- |
| exact    | The value must match the data exactly |
| contains | The data must contain the value       |

**Example: Get all patients whose last name is Smith**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?family:exact=Smith
</pre>

&nbsp;

**Example: Get all patients whose last name contains the text "mit"**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?family:contains=mit
</pre>

&nbsp;

### Operators

Numeric and date values can be combined with operators to search on ranges of values. The following operators are supported:

| Operator | Description              |
| -------- | ------------------------ |
| gt       | Greater Than             |
| ge       | Greater Than or Equal to |
| lt       | Less Than                |
| le       | Less Than or Equal to    |
| eq       | Equals                   |
| ne       | Not Equal to             |

**Example: Get the patients with chart numbers between and including 100 and 200**

<pre class="center-column">
GET https://icp.nextech-api.com/api/Patient/r4?identifier=ge100&identifier=le200
</pre>

&nbsp;

**Example: Search for immunizations for the patient with the id '9D0B7ADE-4B5B-41DD-8AC4-88DB4C93B192' administered between and including 1/1/2022 through 11/14/2022**

<pre class="center-column">
GET https://icp.nextech-api.com/Immunization?patient=patient/9D0B7ADE-4B5B-41DD-8AC4-88DB4C93B192&date=ge2022-01-01&date=lt2022-11-14
</pre>

&nbsp;

### Search Parameter Types

#### String

When matching a simple text string with data, the match is always case-insensitive and always ignores whitespace before and after the data. The default search attempts to match just the start of the data, and you may use a modifier to force an exact match or a match where the data contains the string.

**Example: Get all patients whose last name begins with Smith**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?family=Smith
</pre>

&nbsp;

#### Number

By default, exact matches are performed in numeric searches. You may use operators to specify a numeric range.

**Example: Get the patient with chart number 3442**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?identifier=3442
</pre>

&nbsp;

#### Date

By default, exact matches are performed in date searches. You may use operators to specify a date range.

**Example: Get immunizations for the month of October 2022**

<pre class="center-column">
GET https://icp.nextech-api.com/Immunization?date=ge2022-10-01&date=lt2022-11-01
</pre>

&nbsp;

#### Human Name

Some resources have abstract fields which contain a first name, last name, prefix and suffix. When searching on names, each of those fields are searched individually. The way those fields are matched are consistent with how String searches work, and modifiers may be used to change how the matching works.

**Example: Get the patients whose first name, last name, prefix or suffix begins with Doe**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?name=doe
</pre>

&nbsp;

#### Address

Some resources have abstract fields which contain an Address 1, Address 2, City, State and Postal Code field. When searching on address, each of these fields are searched individually. The way those fields are matched are consistent with how String searches work, and modifiers may be used to change how the matching works.

**Example: Get the patients whose Address 1, Address 2, City, State or Zip code begins with 1500**

<pre class="center-column">
GET https://icp.nextech-api.com/Patient?address=1500
</pre>

&nbsp;

## Writing

Currently, only creating a document via a `POST https://icp.nextech-api.com/DocumentReference` call is supported.

&nbsp;

## Pagination

When a search results in multiple matches, the first ten matches ordered by entered date are returned by default. Included in the result are links to the first set of matches, the following set of matches, the previous set of matches and the last set of matches.

You may overide the number of matches returned, up to fifty, by including `_count={number}` in your search.

`GET http://icp.nextech-api.com/Patient?_count=25`

<aside class="notice">
Search results are limited to 50 matches per page.
</aside>

## Response Codes

The Nextech IntelleChartPRO APIs use the standard HTTP response codes to indicate success or failure of an API request.

| Code | Description                                                                          |
| ---- | ------------------------------------------------------------------------------------ |
| 200  | OK - Successful request                                                              |
| 400  | Bad Request - The request is missing information or is malformed                     |
| 401  | Unauthorized - The request lacks valid authentication credentials                    |
| 403  | Forbidden - The request is valid, but the server is refusing action                  |
| 404  | Not Found - The requested resource cannot be found                                   |
| 408  | Request Timeout - Client did not send a request in the time the server was expecting |
| 422  | Unprocessable Entity - Unable to process the contained instructions                  |
| 429  | Too Many Requests - The user has sent too many requests in a given amount of time    |
| 500  | Internal Server Error - We had a problem with our server                             |
| 501  | Not Implemented Error - Requested implementation is not available                    |
| 502  | Bad Gateway - Communication has been disrupted                                       |
| 523  | Authentication Fault - Unexpected exception in regards to authentication             |

### Exception Handling

- Exceptions are logged and monitored by the Nextech staff.
- Any request related exceptions will be returned to the user with the appropriate 4xx/5xx code as noted above.
- Any unexpected exceptions will result in a 500 error response and indicate there is an issue with the API and/or connected services.

## Remarks

Some resources contain a Remarks section at the end of its documentation page, which contains details on common questions and solutions for that resource.

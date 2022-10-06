# Location

### Overview

A [Location](https://hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-location.html) resource represents a physical location where services are provided. This may or may not be under the practice's management.

### Fields

| Name                 | Description                                                                                                                                                                                                                         | Type                                                                                                                                                                              | Initial Version |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| id                   | The unique value assigned to each location which discerns it from all others                                                                                                                                                        | [string](https://www.hl7.org/fhirdatatypes.html#string)                                                                                                                           | _1.0_          |
| identifier           | The unique value assigned to each location which discerns it from all others                                                                                                                                                        | [Identifier](https://www.hl7.org/fhirdatatypes.html#Identifier)                                                                                                                   | _1.0_          |
| meta.lastUpdated     | The last time the location was modified                                                                                                                                                                                             | [instant](https://www.hl7.org/fhirdatatypes.html#instant)                                                                                                                         | _1.0_          |
| status               | The status of the location (ie. active, inactive)                                                                                                                                                                                   | [code](https://www.hl7.org/fhirdatatypes.html#code)                                                                                                                               | _1.0_          |
| managed              | True if this location is under practice management, for example the practice's primary office location. False if this location is not under practice management, but where services are provided, for example a hospital or clinic. | [boolean](https://www.hl7.org/fhirdatatypes.html#boolean)                                                                                                                         | _14.4_          |
| name                 | The name of the location                                                                                                                                                                                                            | [string](https://www.hl7.org/fhirdatatypes.html#string)                                                                                                                           | _1.0_          |
| telecom              | The contact details of communication at the location                                                                                                                                                                                | [ContactPoint](https://www.hl7.org/fhirdatatypes.html#ContactPoint)                                                                                                               | _1.0_          |
| address              | The address of the location                                                                                                                                                                                                         | [Address](https://www.hl7.org/fhirdatatypes.html#Address)                                                                                                                         | _1.0_          |
| managingOrganization | The reference to the associated organization                                                                                                                                                                                        | [Reference](http://hl7.org/fhirreferences.html#Reference) [(US Core Organization Profile)](http://hl7.org/fhir/r4/us/core/STU3.1.1/StructureDefinition-us-core-organization.html) | _1.0_          |

### Example

<pre class="center-column">
{
    "resourceType": "Location",
    "id": "2",
    "meta":
    {
   	    "lastUpdated": "2022-04-02T14:04:35.9+00:00"
    },
    "extension": [
        {
            "url": "https://select.nextech-api.com/api/structuredefinition/managed",
            "valueBoolean": true
        }
    ],
    "identifier": [
        {
            "use": "official",
            "value": "2"
        }
    ],
    "status": "active",
    "name": "South Dermatology",
    "telecom": [
        {
            "system": "phone",
            "value": "(727) 623-6100",
            "use": "work"
        },
        {
            "system": "other",
            "value": "(727) 718-9884",
            "use": "work"
        },
        {
            "system": "fax",
            "value": "(727) 623-6187",
            "use": "work"
        }
    ],
    "address": {
        "use": "work",
        "type": "both",
        "line": [
            "1234 Central Ave., Suite N"
        ],
        "city": "St. Petersburg",
        "state": "FL",
        "postalCode": "11598"
    },
	"managingOrganization": {
		"reference": "Organization/1",
		"display": "Tampa Dermatology"
	}
}
</pre>

&nbsp;

### _Get_

Returns a single Location result based on the Location ID.

#### HTTP Request

`GET /Location/{LocationID}`

#### Parameters

| Name       | Located in | Description                    | Required | Initial Version |
| ---------- | ---------- | ------------------------------ | -------- | --------------- |
| locationID | path       | The location unique identifier | Yes      | _1.0_          |

#### Example: Get an location with an ID of '123'

<pre class="center-column">
GET https://qa.intellechartbeta.net/icp-fhir-api/Location/123
</pre>

&nbsp;

### _Search_

Searches for all locations based on the given search criteria.

#### HTTP Requests

- `GET /Location?{parameters}`
- `POST /Location/_search?{parameters}`
  - _application/x-www-form-urlencoded body:_ `{parameters}`

**_Note:_** For POST based searches the parameters can be provided in either the URL, the body, or both.

#### Parameters

| Name          | Located in    | Description                                                                  | Required | Initial Version |
| ------------- | ------------- | ---------------------------------------------------------------------------- | -------- | --------------- |
| identifier    | query or body | The unique value assigned to each location which discerns it from all others | No       | _1.0_          |
| name          | query or body | The name of the location                                                     | No       | _1.0_          |
| address       | query or body | A (part of the) address of the location                                      | No       | _1.0_          |
| \_id          | query or body | The location unique identifier                                               | No       | _1.0_          |
| \_lastUpdated | query or body | The last time the location was modified                                      | No       | _1.0_          |

**_Note:_** The possible filter values for the `_lastUpdated` parameter are: `eq`, `ne`, `le`, `lt`, `ge` and `gt`.

#### Example: Get all active locations

#### Example: Get all locations, including managed and non-managed locations

<pre class="center-column">
POST https://qa.intellechartbeta.net/icp-fhir-api/Location/_search?includeAll=true
</pre>

&nbsp;

#### Example: Get all locations whose name contains 'dermatology'

<pre class="center-column">
POST https://qa.intellechartbeta.net/icp-fhir-api/Location/_search?name:contains=dermatology
</pre>

&nbsp;

#### Example: Get a specific location based on identifier

<pre class="center-column">
POST https://qa.intellechartbeta.net/icp-fhir-api/Location/_search?identifier=123
</pre>

&nbsp;

#### Example: Get all locations whose name contains 'dermatology'

<pre class="center-column">
GET https://qa.intellechartbeta.net/icp-fhir-api/Location?name:contains=dermatology
</pre>

&nbsp;

#### Example: Get a specific location based on identifier

<pre class="center-column">
GET https://qa.intellechartbeta.net/icp-fhir-api/Location?identifier=123
</pre>

&nbsp;

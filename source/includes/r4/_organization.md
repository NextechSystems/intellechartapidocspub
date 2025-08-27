# Organization

### Overview

An [Organization](http://hl7.org/fhir/r4/us/core/STU3.1.1/StructureDefinition-us-core-organization.html) resource represents a physical location where services are provided. This may or may not be under the practice's management.

### Fields

| Name             | Description                                                                                                     | Type                                                                                                                                          | Initial Version |
| ---------------- | --------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| id               | The unique value assigned to each location which discerns it from all others                                    | [string](https://www.hl7.org/fhir/r4/datatypes.html#string)                                                                                       | _1.0_          |
| identifier       | The unique value assigned to each location which discerns it from all others                                    | [Identifier](https://www.hl7.org/fhir/r4/datatypes.html#Identifier)                                                                               | _1.0_          |
| identifier:NPI   | NPI identifier for the organization that is used to identify the organization across multiple disparate systems | [Identifier](https://www.hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-organization-definitions.html#Organization.identifier:NPI) | _1.0_          |
| meta.lastUpdated | The last time the organization was modified                                                                     | [instant](https://www.hl7.org/fhir/r4/datatypes.html#instant)                                                                                     | _1.0_          |
| name             | The name of the location                                                                                        | [string](https://www.hl7.org/fhir/r4/datatypes.html#string)                                                                                       | _1.0_          |
| telecom          | The contact details of communication at the location                                                            | [ContactPoint](https://www.hl7.org/fhir/r4/datatypes.html#ContactPoint)                                                                           | _1.0_          |
| address          | The address of the location                                                                                     | [Address](https://www.hl7.org/fhir/r4/datatypes.html#Address)                                                                                     | _1.0_          |
| address.country  | The country of the location address                                                                             | [string](https://www.hl7.org/fhir/r4/datatypes.html#string)                                                                                       | _1.0_          |
| active           | Whether the organization's record is still in active use                                                        | [boolean](http://hl7.org/fhir/R4/datatypes.html#boolean)                                                                                      | _1.0_          |

### Example

<pre class="center-column">
{
    "resourceType": "Organization",
    "id": "2",
    "meta":
    {
   	    "lastUpdated": "2022-04-02T14:04:35.9+00:00"
    },
    "identifier": [
        {
            "use": "official",
            "value": "2"
        },
        {
            "system": "http://hl7.org/fhir/r4/sid/us-npi",
            "value": "ABCDE1234"
        }
    ],
    "active": true,
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
    "address": [{
        "use": "work",
        "type": "both",
        "line": [
            "1234 Central Ave., Suite N"
        ],
        "city": "St. Petersburg",
        "state": "FL",
        "postalCode": "11598",
        "country": "US"
    }]
}
</pre>

&nbsp;

### _Get_

Returns a single Organization result based on the Organization ID.

#### HTTP Request

`GET /Organization/{OrganizationID}`

#### Parameters

| Name           | Located in | Description                        | Required | Initial Version |
| -------------- | ---------- | ---------------------------------- | -------- | --------------- |
| OrganizationID | path       | The organization unique identifier | Yes      | _1.0_          |

#### Example: Get an organization with an ID of '123'

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Organization/123
</pre>

&nbsp;

### _Search_

Searches for all organizations based on the given search criteria.

#### HTTP Requests

- `GET /Organization?{parameters}`
- `POST /Organization/_search?{parameters}`
  - _application/x-www-form-urlencoded body:_ `{parameters}`

**_Note:_** For POST based searches the parameters can be provided in either the URL, the body, or both.

#### Parameters

| Name          | Located in    | Description                                                                      | Required | Initial Version |
| ------------- | ------------- | -------------------------------------------------------------------------------- | -------- | --------------- |
| identifier    | query or body | The unique value assigned to each organization which discerns it from all others | No       | _1.0_          |
| name          | query or body | The name of the organization                                                     | No       | _1.0_          |
| address       | query or body | A (part of the) address of the organization                                      | No       | _1.0_          |
| \_id          | query or body | The organization unique identifier                                               | No       | _1.0_          |
| \_lastUpdated | query or body | The last time the organization was modified                                      | No       | _1.0_          |

**_Note:_** The possible filter values for the `_lastUpdated` parameter are: `eq`, `ne`, `le`, `lt`, `ge` and `gt`.

#### Example: Get all organizations whose name contains 'dermatology'

<pre class="center-column">
POST https://api.intellechart.net/icp-fhir-api/Organization/_search?name:contains=dermatology
</pre>

&nbsp;

#### Example: Get a specific organization based on identifier

<pre class="center-column">
POST https://api.intellechart.net/icp-fhir-api/Organization/_search?identifier=123
</pre>

&nbsp;

#### Example: Get all organizations whose name contains 'dermatology'

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Organization?name:contains=dermatology
</pre>

&nbsp;

#### Example: Get a specific organization based on identifier

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Organization?identifier=123
</pre>

&nbsp;

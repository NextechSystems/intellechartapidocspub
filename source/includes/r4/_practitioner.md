# Practitioner

### Overview

A [Practitioner](https://hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-practitioner.html) resource represents an individual who is engaged in the healthcare process and healthcare-services. In the Nextech Software, these are providers who are linked to users.

### Fields

| Name       | Description                                                                      | Type                                                                | Initial Version |
| ---------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------- | --------------- |
| identifier | The unique value assigned to each Practitioner which discerns it from all others | [Identifier](https://www.hl7.org/fhir/r4/datatypes.html#Identifier)     | _1.0_          |
| active     | Whether this practitioner's record is in active use.                             | [boolean](https://www.hl7.org/fhir/r4/datatypes.html#boolean)           | _1.0_          |
| name       | The name(s) associated with the practitioner                                     | [HumanName](https://www.hl7.org/fhir/r4/datatypes.html#HumanName)       | _1.0_          |
| telecom    | Contact detail(s) for the practitioner (that apply to all roles)                 | [ContactPoint](https://www.hl7.org/fhir/r4/datatypes.html#ContactPoint) | _1.0_          |
| address    | Address(es) of the practitioner that are not role specific                       | [Address](https://www.hl7.org/fhir/r4/datatypes.html#Address)           | _1.0_          |
| gender     | Gender of the practitioner                                                       | [Code](https://www.hl7.org/fhir/r4/valueset-administrative-gender.html) | _1.0_          |
| birthDate  | The date of birth of the practitioner                                            | [date](https://www.hl7.org/fhir/r4/datatypes.html#date)                 | _1.0_          |

### Example

<pre class="center-column">
{
    "resourceType": "Practitioner",
    "identifier": [
        {
            "use": "official",
            "system": "https://api.intellechart.net/icp-fhir-api/api/structuredefinition/practitioner-id"
            "value": "9219"
        },
        {
            "system": "http://hl7.org/fhir/r4/sid/us-npi",
            "value": "1245319599"
        }
    ],
    "active": true,
    "name": [
        {
            "text": "Davis, Albert Edward",
            "family": "Davis",
            "given": [
                "Albert",
                "Edward"
            ]
        }
    ],
    "telecom": [
        {
            "system": "phone",
            "value": "(813) 324-2391",
            "use": "work"
        },
        {
            "system": "email",
            "value": "provider@nextech.com",
            "use": "work"
        }
    ],
    "address": [
        {
            "use": "work",
            "type": "both",
            "line": [
                "550 W N ST"
            ],
            "city": "Tampa",
            "state": "FL",
            "postalCode": "33609"
        }
    ],
    "gender": "male",
    "birthDate": "1970-09-27"
</pre>

&nbsp;

### _Get_

Returns a single Practitioner result based on the Practitioner ID.

#### HTTP Request

`GET /Practitioner/{practitionerID}`

#### Parameters

| Name           | Located in | Description                                | Required | Initial Version |
| -------------- | ---------- | ------------------------------------------ | -------- | --------------- |
| practitionerID | path       | The unique identifier for the practitioner | Yes      | _1.0_          |

#### Example: Get a specific Practitioner based on identifier

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Practitioner/12
</pre>

&nbsp;

### _Search_

Searches for all based on the given search criteria.

#### HTTP Request

- `GET /Practitioner?{parameters}`
- `POST /Practitioner/_search?{parameters}`
  - _application/x-www-form-urlencoded body:_ `{parameters}`

#### Parameters

| Name       | Located in   | Description                                                                      | Required | Initial Version |
| ---------- | ------------ | -------------------------------------------------------------------------------- | -------- | --------------- |
| identifier | query or uri | The unique value assigned to each Practitioner which discerns it from all others | No       | _1.0_          |
| name       | query        | The name of the Practitioner                                                     | No       | _1.0_          |

#### Example: Get all Practitioners

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Practitioner
</pre>

&nbsp;

#### Example: Get a specific Practitioner based on identifier

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Practitioner?identifier=12
</pre>

&nbsp;

#### Example: Get a specific Practitioner based on National Provider Identifier (NPI)

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Practitioner?identifier=http://hl7.org/fhir/r4/sid/us-npi|1245319599
</pre>

&nbsp;

#### Example: Get all Practitioners whose name contains 'smith'

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Practitioner?name:contains=smith
</pre>

&nbsp;

### Remarks

- To get a specific Practitioner by the National Provider Identifier (NPI), the system (http://hl7.org/fhir/r4/sid/us-npi) must be included in the query.
- Providers will not show up as Practitioners unless their Contacts module record has the Linked User setting configured.
  - Prior to version 14.1, Practitioners could be returned more than once if multiple users are assigned to use the same provider in their Contacts module User properties.

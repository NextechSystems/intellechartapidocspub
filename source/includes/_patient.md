# Patient

## Patient

### Overview

Basic information about a patient.

### Fields

| Name | Description | Type | Initial Version |
| ---- | ----------- | ---- | --------------- |
| patientId | Unique identifier for a patient. | integer | _1.0_ |
| chartNumber | Unique identifier for a patient's chart. | string | _1.0_ |
| firstName | Patient's first (given) name. | string | _1.0_ |
| lastName | Patient's last (family) name. | string | _1.0_ |
| middleName | Patient's middle name. | string | _1.0_ |
| dob | Patient's date of birth | date | _1.0_ |
| ssn | Patient's social security number | string | _1.0_ |
| homePhone | Patient's home phone number | string | _1.0_ |

### Sample
<pre class="center-column">
{
    "patientId": 0,
    "chartNumber": "string",
    "firstName": "string",
    "lastName": "string",
    "middleName": "string",
    "dob": "2017-12-14T15:08:59.934Z",
    "ssn": "string",
    "homePhone": "string"
  }
</pre>
&nbsp;

### *Search*
Searches for all appointments matching the given search criteria. See [https://www.hl7.org/fhir/search.html](https://www.hl7.org/fhir/search.html) for instructions on formatting search criteria.

#### HTTP Request 
`GET GET /api/search?{parameters}`

#### Parameters
| Name | Located in | Description | Required | Initial Version |
| ---- | ---------- | ----------- | -------- | --------------- |
| term | string | String to search patients for. Will attempt to match the patient's name or chart number. | yes | _1.0_ |

#### Example: Get a patient with a specific chart number

<pre class="center-column">
GET https://mdi.nextech-api.com/api/search?term=ABC12345
</pre>
&nbsp;

#### Example: Get all patients with a specific name

<pre class="center-column">
GET https://mdi.nextech-api.com/api/search?term=william
</pre>
&nbsp;

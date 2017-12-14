# Encounter

## Encounter CCD

### Overview
Encounter data includes a summary of the encounters basic properties and the CCD in HTML format.

### Fields
| Name | Description | Type | Initial Version |
| ---- | ----------- | ---- | --------------- |
| summary.encounterId | Unique for the encounter | integer | _1.0_ |
| summary.doctorId | Unique identifier for the doctor associated with this encounter | integer | _1.0_ |
| summary.doctorFirstName | Doctor's first name. | string | _1.0_ |
| summary.doctorLastName | Doctor's last name. | string | _1.0_ |
| summary.doctorProfessionalDesignation | Doctor's professional designation suffix. (e.g. MD)  | string | _1.0_ |
| summary.department | Practice department associated with this encounter. | string | _1.0_ |
| summary.location | Location of the practice this encounter is associated with. | string | _1.0_ |
| summary.encounterDate | Date when this encounter occurred. | UTC date / time | _1.0_ |
| summary.type | Description of what type of encounter this was. | string | _1.0_ |
| summary.encounterLocked | Whether this encounter's data has been locked. | string | _1.0_ |
| ccd | CCD in HTML format | string | _1.0_ |

### Example
<pre class="center-column">
[
  {
    "summary": {
      "encounterId": 0,
      "doctorId": 0,
      "doctorFirstName": "string",
      "doctorLastName": "string",
      "doctorProfessionalDesignation": "string",
      "department": "string",
      "location": "string",
      "encounterDate": "2017-12-14T15:08:59.924Z",
      "type": "string",
      "encounterLocked": true
    },
    "ccd": "string"
  }
]
</pre>
&nbsp;

### *Search*
Searches for all of a one patient's encounters within a date range.

#### HTTP Request 
`GET /{patientId]/encounters/search`

#### Parameters
| Name | Located in | Description | Required | Type | Initial Version |
| ---- | ---------- | ----------- | -------- | ---- | --------------- |
| patientId | path | Unique identifier for the patient. | Yes | integer | _1.0_ |
| start | query | Earliest date included in the search. If omitted, search begins with the patient's earliest encounter. | No | date-time | _1.0_ |
| end | query | Latest date included in the search. If omitted, search ends with the current date. | No | date-time | _1.0_ |
| section | query | Section of data to include in the CCD property. If omitted, all sections are returned. (Get list of valid sections via */encounters/categories*) | No | string | _1.0_ |

#### Example: Get the CCDs for all of a patient's encounters

<pre class="center-column">
GET https://mdi.nextech-api.com/api/1000/encounters/search
</pre>
&nbsp;

#### Example: Get the CCDs for a patient's encounters within a date range

<pre class="center-column">
GET https://mdi.nextech-api.com/api/1000/encounters?start=2-2-2000&end=5-5-2010
</pre>
&nbsp;

#### Example: Get one section of the CCDs for a patient's encounters with a date range

<pre class="center-column">
GET https://mdi.nextech-api.com/api/1000/encounter?start=2-2-2000&end=5-5-2010&section=history
</pre>
&nbsp;

### CCD Sections
List all of the valid section names for encounter CCDs.   

#### HTTP Request 
`GET /encounters/categories` 


# Provenance

### Overview

The [provenance](https://www.hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-provenance.html) of a resource is a record that describes entities and processes involved in producing and delivering or otherwise influencing that resource.

### Fields

| Name             | Description                                                                    | Type                                                                                                                                                                                                                                                                                                                                                                                                                            | Initial Version |
| ---------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| id               | The unique value assigned to each provenance which discerns it from all others | [string](https://www.hl7.org/fhir/r4/datatypes.html#string)                                                                                                                                                                                                                                                                                                                                                                         | _1.0_          |
| meta.lastUpdated | The last time the provenance was modified                                      | [instant](https://hl7.org/fhir/r4/datatypes.html#instant)                                                                                                                                                                                                                                                                                                                                                                           | _1.0_          |
| target           | The resource(s) the provenance supports                                        | [Reference](http://hl7.org/fhirreferences.html#Reference) ([Resource](http://hl7.org/fhirresource.html))                                                                                                                                                                                                                                                                                                                        | _1.0_          |
| recorded         | Timestamp of when the activity was recorded                                    | [instant](http://hl7.org/fhir/R4/datatypes.html#instant)                                                                                                                                                                                                                                                                                                                                                                        | _1.0_          |
| agent            | Actor involved                                                                 | [slice](http://hl7.org/fhirprofiling.html#slicing)                                                                                                                                                                                                                                                                                                                                                                              | _1.0_          |
| agent.type       | How the agent participated                                                     | [CodeableConcept](http://hl7.org/fhir/R4/datatypes.html#CodeableConcept)                                                                                                                                                                                                                                                                                                                                                        | _1.0_          |
| agent.who        | Who participated                                                               | [Reference](http://hl7.org/fhirreferences.html#Reference) ([US Core Practitioner Profile](https://www.hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-practitioner.html) or [US Core Organization Profile](https://www.hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-organization.html) or [US Core Patient Profile](https://www.hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-patient.html)) | _1.0_          |
| agent.onBehalfOf | Who the agent is representing                                                  | [Reference](http://hl7.org/fhirreferences.html#Reference) ([US Core Organization Profile](https://www.hl7.org/fhir/us/core/STU3.1.1/StructureDefinition-us-core-organization.html))                                                                                                                                                                                                                                             | _1.0_          |

### Example

<pre class="center-column">
{
    "resourceType": "Provenance",
    "id": "4",
    "meta": {
        "lastUpdated": "2022-08-05T14:29:08.217-04:00"
    },
    "target": [
        {
            "reference": "Immunization/145"
        },
        {
            "reference": "DocumentReference/history-131816"
        }
    ],
    "recorded": "2022-08-05T14:29:08.217-04:00",
    "agent": [
        {
            "type": {
                "coding": [
                    {
                        "system": "http://terminology.hl7.org/CodeSystem/provenance-participant-type",
                        "code": "author",
                        "display": "Author"
                    }
                ],
                "text": "Author"
            },
            "who": {
                "reference": "Practitioner/26546",
                "display": "PortalProvider, PortalProvider"
            },
            "onBehalfOf": {
                "reference": "Organization/47",
                "display": "Pawtucket Plastic Surgeons"
            }
        },
        {
            "type": {
                "coding": [
                    {
                        "system": "http://hl7.org/fhir/r4/us/core/CodeSystem/us-core-provenance-participant-type",
                        "code": "transmitter",
                        "display": "Transmitter"
                    }
                ],
                "text": "Transmitter"
            },
            "who": {
                "reference": "Practitioner/26546",
                "display": "PortalProvider, PortalProvider"
            },
            "onBehalfOf": {
                "reference": "Organization/47",
                "display": "Pawtucket Plastic Surgeons"
            }
        }
    ]
}
</pre>

&nbsp;

### _Get_

Returns a single Provenance result based on the Provenance ID.

#### HTTP Request

`GET /Provenance/{ProvenanceID}`

#### Parameters

| Name         | Located in | Description                      | Required | Initial Version |
| ------------ | ---------- | -------------------------------- | -------- | --------------- |
| ProvenanceID | path       | The provenance unique identifier | Yes      | _1.0_          |

#### Example: Get a specific provenance based on identifier

<pre class="center-column">
GET https://qa.intellechartbeta.net/icp-fhir-api/Provenance/123
</pre>

&nbsp;

# Coverage

## Coverage

### Overview
The Coverage resource provides patient insurance information which may be used to pay for the provision of health care products and services.

### Fields
| Name | Description | Type | Initial Version |
| ---- | ----------- | ---- | --------------- |
| identifier | The unique identifer for the coverage | [Identifier](https://www.hl7.org/fhir/datatypes.html#Identifier) | _1.0_ |
| status | The status of the coverage | [code](https://www.hl7.org/fhir/datatypes.html#code) | _1.0_ |
| type | The type of coverage (ie. Medical, Vision, Dental, Auto, Workers' Comp). See [Coverage Type Codes](http://hl7.org/fhir/valueset-coverage-type.html) | [CodeableConcept](http://hl7.org/fhir/datatypes.html#CodeableConcept) | _1.0_ |
| subscriber | The subscriber to the policy | [Reference(Patient or RelatedPerson)](https://www.hl7.org/fhir/references.html) | _1.0_ |
| subscriberId | The identifier assigned to the subscriber | [string](http://hl7.org/fhir/datatypes.html#string) | _1.0_ |
| beneficiary | The patient who benefits from the coverage | [Reference(Patient)](https://www.hl7.org/fhir/references.html) | _1.0_ |
| relationship | The beneficiary (or patient) relationship to the subscriber. See [Policyholder Relationship Codes](http://hl7.org/fhir/valueset-policyholder-relationship.html) | [CodeableConcept](http://hl7.org/fhir/datatypes.html#CodeableConcept) | _1.0_ |
| period | The coverage effective and expiry dates (if available) | [Period](http://hl7.org/fhir/datatypes.html#Period) | _1.0_ |
| payor | The reference to the insurance company providing the insurance coverage | [Reference(Organization)](https://www.hl7.org/fhir/references.html) | _1.0_ |
| order | The relative order of the coverage | [positiveInt](http://hl7.org/fhir/datatypes.html#positiveInt) | _1.0_ |

### Example
<pre class="center-column">
{
    "resourceType": "Coverage",
    "id": "12345",
    "identifier": [
        {
            "use": "official",
            "value": "12345"
        }
    ],
    "status": "active",
    "type": {
        "coding": [
            {
                "system": "http://hl7.org/fhir/v3/ActCode",
                "code": "EHCPOL",
                "display": "extended healthcare"
            }
        ]
    },
    "subscriber": {
        "reference": "Patient/67890",
        "display": "Smith, John"
    },
    "subscriberId": "ABC123456",
    "beneficiary": {
        "reference": "Patient/12345",
        "display": "Doe, Jane"
    },
    "relationship": {
        "coding": [
            {
                "system": "http://hl7.org/fhir/policyholder-relationship",
                "code": "self",
                "display": "Self"
            }
        ]
    },
    "period": {
        "start": "2025-01-01",
        "end": "2025-12-31"
    },
    "payor": [
        {
            "reference": "Organization/100",
            "display": "Sample Insurance Company"
        }
    ],
    "order": 1
}
</pre>
&nbsp;

### *Search*
Searches for all _active_ coverages (insured parties) based on the given search criteria.

#### HTTP Request 
`GET /Coverage?{parameters}`

#### Parameters
| Name | Located in | Description | Required | Initial Version |
| ---- | ---------- | ----------- | -------- | --------------- |
| patient | query | Search coverages by patient identifier |  N | _1.0_ |
| beneficiary | query | Search coverages by patient identifier | N | _1.0_ |

#### Example: Get coverages for a single patient

<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Coverage?patient=ce2a5ae0-3514-4f63-8609-911da841e72e
</pre>
&nbsp;

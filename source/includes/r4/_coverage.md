# Coverage

### Overview
The Coverage resource provides patient insurance information which may be used to pay for the provision of health care products and services.

### Fields
| Name | Description | Type | Initial Version |
| ---- | ----------- | ---- | --------------- |
| identifier | The unique identifier for the coverage | [Identifier](https://www.hl7.org/fhir/R4/datatypes.html#Identifier) | _1.0_ |
| status | The status of the coverage | [code](https://www.hl7.org/fhir/R4/datatypes.html#code) | _1.0_ |
| type | The type of coverage (ie. Medical, Vision, Dental, Auto, Workers' Comp). See [Coverage Type Codes](http://hl7.org/fhir/R4/valueset-coverage-type.html) | [CodeableConcept](http://hl7.org/fhir/R4/datatypes.html#CodeableConcept) | _1.0_ |
| subscriber | The subscriber to the policy | [Reference(Patient or RelatedPerson)](https://www.hl7.org/fhir/R4/references.html) | _1.0_ |
| subscriberId | The identifier assigned to the subscriber | [string](http://hl7.org/fhir/R4/datatypes.html#string) | _1.0_ |
| beneficiary | The patient who benefits from the coverage | [Reference(Patient)](https://www.hl7.org/fhir/R4/references.html) | _1.0_ |
| relationship | The beneficiary (or patient) relationship to the subscriber. See [Policyholder Relationship Codes](https://hl7.org/fhir/R4/valueset-relationship.html) | [CodeableConcept](http://hl7.org/fhir/R4/datatypes.html#CodeableConcept) | _1.0_ |
| period | The coverage effective and expiry dates (if available) | [Period](http://hl7.org/fhir/R4/datatypes.html#Period) | _1.0_ |
| payor | The reference to the insurance company providing the insurance coverage | [Reference(Organization)](https://www.hl7.org/fhir/R4/references.html) | _1.0_ |
| order | The relative order of the coverage | [positiveInt](http://hl7.org/fhir/R4/datatypes.html#positiveInt) | _1.0_ |

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

### _Search_
Searches for active coverages based on the given search criteria.

#### HTTP Request 
`GET /Coverage?{parameters}`

`POST /Coverage/_search`

#### Parameters
| Name | Located in | Description | Required | Initial Version |
| ---- | ---------- | ----------- | -------- | --------------- |
| _id | query/form | The coverage identifier | N | _1.0_ |
| patient | query/form | Search coverages by patient identifier | N | _1.0_ |
| beneficiary | query/form | Search coverages by beneficiary (patient) identifier | N | _1.0_ |
| status | query/form | The status of the coverage (e.g., active, cancelled) | N | _1.0_ |
| type | query/form | The type of coverage | N | _1.0_ |
| payor | query/form | The payor (insurance company) reference | N | _1.0_ |
| period | query/form | The coverage period. Supports prefixes: gt, lt, ge, le, eq | N | _1.0_ |
| _lastUpdate | query/form | Filter by last update timestamp. Supports prefixes: gt, lt, ge, le, eq | N | _1.0_ |
| _since | query/form | Filter by resources updated since the given timestamp | N | _1.0_ |
| _count | query/form | The maximum number of results to return | N | _1.0_ |
| _getPagesOffset | query/form | The page offset for pagination | N | _1.0_ |
| _revInclude | query/form | Reverse include related resources. Supported value: `Provenance:target` | N | _1.0_ |

#### Response
| HTTP Code | Description | Resource |
| --------- | ----------- | -------- |
| 200 | OK | [Bundle](https://www.hl7.org/fhir/bundle.html) |
| 400 | Bad Request | [OperationOutcome](https://www.hl7.org/fhir/operationoutcome.html) |
| 401 | Unauthorized | [OperationOutcome](https://www.hl7.org/fhir/operationoutcome.html) |
| 404 | Not Found | [OperationOutcome](https://www.hl7.org/fhir/operationoutcome.html) |
| 500 | Internal Server Error | [OperationOutcome](https://www.hl7.org/fhir/operationoutcome.html) |

#### Example: Get coverages for a single patient (GET)
<pre class="center-column">
GET https://api.intellechart.net/icp-fhir-api/Coverage?patient=ce2a5ae0-3514-4f63-8609-911da841e72e
</pre>
&nbsp;

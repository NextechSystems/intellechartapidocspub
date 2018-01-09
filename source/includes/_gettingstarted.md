# Getting Started #

All API requests are performed over HTTPS. Although the [FHIR® standard](https://www.hl7.org/fhir/index.html) supports both JSON and XML, this API currently only supports JSON.  Therefore any type explicitly defined in the request's `Accept` header will be ignored.

Before you can access the Nextech API you must have the proper credentials to authenticate. These credentials will be provided to you by your Nextech representative.  


**API Endpoint**  
`https://saas.nextech-api.com/ehr/api`

The following values are required in the Header for every request...

| Name | Description | Required? |
| ---- | ----------- | --------- |
| Authorization | Every request requires a Bearer token `Bearer {access_token}` | Yes |
| x-nextech-practice-id | The unique identifier for a practice | Yes |

## Authentication Test2 ##

Nextech's EHR API is protected by the [OAuth 2.0 standard](https://oauth.net/2/) for authenticating requests.  All API requests are authenticated by passing a Bearer token in the Authorization Header.

```Authorization: Bearer {access_token}```

### Request Authorization Code ###
The SAAS API authenticates requests through a user credentials grant. You must request an authorization code through an interactive login page, then use that code to request an access token.

`GET https://login.microsoftonline.com/nextechapibeta.onmicrosoft.com/oauth2/authorize`
| Parameter | Description |
| --------- | ----------- |
| client_id | Application ID |
| response_type | `code` |
| redirect_url | URL that will be called with the authorization code |
| resource | The app to consume the token |

### Request Access Token ###
Access tokens are used to make API requests on behalf of a user. These tokens are short-lived (1 hour by default) but should be kept confidential in transit and in storage. A `access_token` and `refresh_token` pair is issued when requesting an access token.

**HTTP Request**  
`POST https://login.microsoftonline.com/nextechapibeta.onmicrosoft.com/oauth2/token`

https://login.microsoftonline.com/mdidev.onmicrosoft.com/oauth2/token
Form (x-www-form-urlencoded):
   grant_type: authorization_code
   client_id: c6eef4c1-62a2-4f3f-88a6-8679639da10a
   redirect_uri: http://localhost:8000/callback/
   code: <authorization code>
   resource: https://mdidev.onmicrosoft.com/dbb380e9-5cce-42cb-87be-8920d2f0541a

| Parameter | Description |
| --------- | ----------- |
| grant_type | `authorization_code`
| client_id | Application ID |
| redirect_uri | URL that will be called with the access token |
| code | Authorization code |
| resource | The app to consume the token |

**Response Parameters**

| Parameter | Description |
| --------- | ----------- |
| code | Access token |

## Response Codes ##

The Nextech Select APIs use the standard HTTP response codes to indicate success or failure of an API request.

| Code | Description |
| ---- | ----------- |
| 200 | OK - Successful request |
| 400 | Bad Request - The request is missing information or is malformed |
| 403 | Forbidden - The request is valid, but the server is refusing action |
| 404 | Not Found - The requested resource cannot be found |
| 500 | Internal Server Error - We had a problem with our server |

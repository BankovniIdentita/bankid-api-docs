# APIs exposed by Bank iD for Service Providers

| Version | Note |
| ------------- |-------------|
| 1.3.3 | Fixed description and authentication method of```/token-info``` endpoint.<br>Fixed some typos.<br>Added 415 Unsupported Media Type error to all POST endpoints. Valid content-type has to be used.<br>Added ```/sign/audit``` endpoint for QSIGN service. |
| 1.3.2 | ```state``` in ```/logout``` endpoint is now not mandatory.<br>Fixed some typos.<br>Added ```trace_id``` to ```/auth``` endpoint.<br>Adjusted unsupported characters in ```document_title``` and ```document_subject```. |

<details>
<summary>Old change notes</summary>

| Version | Note |
| ------------- |-------------|
| 1.3.1 | New GET endpoint for ```/logout```.<br>Removed mandatory requirement for ```redirect_uri``` in ```refresh_token``` authorization request.<br>Fixed some typos.<br>```document_id``` in ```/ros``` endpoint is mandatory and could have any value, is not checked against PDF files.<br>Adjusted unsupported characters in ```document_title``` and ```document_subject```.<br>New ```/sign/status``` endpoint for sign status verification.<br>```state``` and ```nonce``` are now mandatory in ```/ros``` and ```/auth``` endpoints to strengthen security. |
| 1.3.0 | New error ```basic_registers_unavailable``` in ```ros``` endpoint.<br>Miminal value for ```max_age``` in ```/ros``` endpoint is now set to 600 seconds.<br>For PDF 2.0 files, document_id will be acquired from XMP metadata. |
| 1.2.9 | New callback ```auth_failed``` in case ```code``` has been already issued.<br>New callback ```insufficient_scope``` in case missing required scopes from IdP for SIGN service.<br>New callback ```basic_registers_unavaiable``` for QSIGN service.<br>New parameter ```seal_visibility``` in ```/ros``` endpoint. In case you require seal visible on documents in SIGN or QSIGN<br>Fixed status codes for get and post in ```/authorize``` endpoint<br>Added ```401``` status code to ```/token``` endpoint |
| 1.2.8 | fixed service name in ```available_services``` in /api/v1/banks endpoint from ```QSIGN``` to ```QUALIFIED_SIGNATURE```<br>removed ```profile.verification``` from /userinfo endpoint example to be inline with the rest of the documentation |
| 1.2.7 | ```claims``` in auth endpoint request set as deprecated. |
| 1.2.6 | Fixed missing ```hash_alg``` in ```multiDocumentObject```.<br>```primary_nationality``` set as deprecated. |
| 1.2.5 | Added ```500``` error to /profile, /token, /ros and /token-info endpoints.<br>Fixed enum in banks' ```available_services```. |
| 1.2.4 | Added support for additional types of id cards `OP` and `CA`, Czech Republic documents without machine readable zone.<br>Added unsupported characters to ```document_title``` description .<br>Added ```503``` Temporarily unavailable error to ```/ros``` endpoint in case Basic Registers have planned downtime.<br>Fixed typos in addresses and idcards scopes.<br>Fixed supported ```response_type``` in ```/ros``` endpoint.<br>```valid_to``` in ```idcards``` is now not mandatory, due to missing parameter in idcards type 'OP', in all other typess it's still mandatory on application level. |
| 1.2.3 | Fixed description for ```not_implemented```.<br>Renamed auth error callback ```client_not_eligible``` to ```user_not_eligible```. |
| 1.2.2 | Fixed description for ```document_language```. |
| 1.2.1 | New scopes for Qualified signatures ```sign.qualified``` and ```sign.officially_certified```.<br>Fixed typos and missing descriptions. |
| 1.2.0 | Fixed response code for /ros endpoint, it's now correctly 200 instead of 201.<br>New callback ```sign_error```, if PDF document(s) cannot be signed, this callback will be returned.<br>New callback ```client_not_eligible```, if authorization is not possible due to age or legal capacity restrictions.<br>Added ```traceId``` to all endpoints for support purposes.<br>Added ```sign_field``` to ```documentObject``` and ```documentObjects``` to support PDF signature field annotations.<br>```sign_area``` is now set as not mandatory.<br>Fixed ```exp``` in /ros response, it's correctly integer instead of date-time.<br>Fixed missing ```upload_uris``` in /ros response.<br>Cleanup of unused objects.<br>Modified for better code generation.<br>	|
| 1.1.21 | Fixed element ```paymentAccountsDetails```, it's array now instead of object. |
| 1.1.20 | New elements in /profile addresses (cityarea, evidencenumber) and payment accounts details<br>New types of idcards by ROB<br>New callback "eid_doesnt_exist" |
| 1.1.19 | Added ```outdated_subs``` field to IDToken and AuthorizationIDToken containing all identifiers from the associated identities provided to the application via Bank iD.<br>Some elements in Document Objects may be empty |
| 1.1.18 | Added new feature for support of signature of multiple documents. |
| 1.1.17 | Added new parameter ```available_services``` in Bank List API. |
| 1.1.16 | As part of the unification, the ```upload_url``` parameter in the GET /verification response has been renamed to ```upload_uri```<br>The query parameter ```document_id``` in GET /verification is newly defined as optional<br>New response type 501 in /ros endpoint  |
| 1.1.15 | Removed the ```whole_document``` parameter from the document /verification response |
| 1.1.14 | Updates and examples for the Sign service |
| 1.1.13 | The element time in the verification is now optional |
| 1.1.12 | The time in ```verified_clamis.verification.time``` must be **with colon in date offset** (e.g. 2015-04-05T14:31:22+02:00)<br> ```max_age``` element in ```/ros``` endpoint request is in number format now. |
| 1.1.11 | The ```priority``` parameter in the ```signObject``` element is now mandatory and unique. The affected service is /ros.<br>New element with signed signObject as part of idtoken after authorization of the document by the end user.<br>Added scope ```notification.claims_updated``` (the application wants to send notifications) for **/profile** and **/userinfo** endpoints |
| 1.1.10 | Element ```verified_claims-verification.time``` changed to mandatory. Now, in case of sending a verification element, it is always necessary to send the date and time of the verification in the ISO 8601 format. |
| 1.1.9 | For the ```max_age``` parameter in the /auth endpoint, the description and occurrence obligation changed. |
| 1.1.8 | Added ```birthcountry``` to /profile ```verified_claims``` element in response |
| 1.1.7 | Correct response ```application/json``` on POST /ros endpoint<br>Added ```birthcountry``` element to /profile response |
| 1.1.6 | Reword tags and summaries to better reflect official Bank iD product portfolio |
| 1.1.5 | Removed unnecessary specification for the document upload resource during document verification<br>Clarified `signObject` and `documentObject` specification and examples<br>Clarified various property data types and examples throughout the signing process |
| 1.1.4 | Fixed server reference to correct host oidc.sandbox.bankid.cz<br>Added code_challenge_methods_supported element to OIDCConfigure scheme |
| 1.1.3 | A more well-arranged list of scopes (directly in the description of /userinfo and /profile) |
| 1.1.2 | Fixed error response format at /userinfo and /profile |
| 1.1.1 | GET /auth endpoint specification<br>Added for better clarity complete possible list of parameters of ```claims``` element in ```verified_claims``` for services /userinfo and /profile |
| 1.1.0 |  added optional element ```bank_id``` in POST /ros endpoint<br>elements in the ```sign_area``` object are now all mandatory (POST /ros)<br>```structured_scope``` are not newly array type (POST /ros)<br>removed ```remote_authorization``` element (POST /ros)<br>format of ```max_age``` element changed from date-time to number of seconds (POST /ros)<br>changed response to the verification of the signed document. Newly, Bank iD returns a metadata collection of all signatures in the document (POST /verification)<br>the element ```verification``` changed to optional within ```verified_claims``` (GET /profile)   |
| 1.0.0 | the first version of the document    |
</details>

**Basic Information**

Bank iD is only required to implement APIs that are specified in this document, as that is what will be used by the SeP.
However for additional explanations and details, it is strongly recommended that readers are familiar with the specifications below.


**Verified Data Representation extension for /userinfo and /profile resource**

This extension to OpenID Connect wants to ensure that IDPs cannot mix up verified and unverified Claims and incidentally process unverified Claims as verified Claims.

The representation proposed therefore provides the IDP with the verified Claims within a container element verified_claims. This container is composed of the verification  evidence related to a certain verification process and the corresponding Claims about the End-User which were verified in this process.

Verification elements contains the information about the process conducted to verify a person's identity and bind the respective person data to a user account.


**Source material and relevant modifications:**

* [OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html) 

  * Signed and encrypted JWTs MAY be used for /userinfo and /profile responses
  * In Service Provider's Bank iD relationship the UserInfo Claims MUST be returned as the members of a JSON object unless a signed or encrypted response was requested during Client Registration.
  * The sub (subject) Claim MUST always be returned in the UserInfo Response.
  * If a Claim is not returned, that Claim Name SHOULD be omitted from the JSON object representing the Claims; it SHOULD NOT be present with a null or empty string value.
  * The sub Claim in the UserInfo and Profile Response MUST be verified to exactly match the sub Claim in the ID Token; if they do not match, the UserInfo Response values MUST NOT be used.
  * The UserInfo and Profile Endpoint MUST return a content-type header to indicate which format is being returned and if the response body is a text JSON object; the response body SHOULD be encoded using UTF-8.
  * If the UserInfo or Profile Response is signed and/or encrypted, then the Claims are returned in a JWT and the content-type MUST be application/jwt. The response MAY be encrypted without also being signed. If both signing and encryption are requested, the response MUST be signed then encrypted, with the result being a Nested JWT.

* [OpenID Connect for Identity Assurance 1.0](https://openid.net/specs/openid-connect-4-identity-assurance-1_0.html)

  * The `txn` Claim as defined in [RFC8417](https://tools.ietf.org/html/rfc8417) is used in the context of Bank iD data exchange to build audit trails across the parties involved in an OpenID Connect transaction. Claim txn is always REQUIRED in the userinfo response content.
  * This arrangement introduces the possibility for the bank to separate the verified Claims within a container element `verified_claims`. This container is composed of the  verification evidence related to a certain verification process and the corresponding Claims about the End-User which were verified in this process.
  * Implementations MUST ignore any sub-element not defined in this specification or extensions of this specification.
  * In the case of this definition verification element MUST consist of the following elements:
     * `trust_framework`: REQUIRED. String determining the trust framework governing the identity verification process. For example, the value of ``cz_aml`` for verification according to the Czech AML law.
     * `time`: OPTIONAL. Time stamp in ISO 8601:2004 [ISO8601-2004] YYYY-MM-DDThh:mm:ss±hh format representing the date and time when identity verification took place.
     * `verification_process`: REQUIRED. In the case of this specification, the verification process shall include the identification number of the relevant bank where the initial physical verification of the client took place. This is the bank's identification number, which is kept in the list of regulated and registered entities of the CNB JERRS.
     * `claims`: The claims element contains the claims about the End-User that were verified during the defined verification process.
     * Verified Claims can be requested on the level of individual Claims about the End-User by utilizing the claims parameter as defined in Section 5.5. of the OpenID Connect specification [OpenID](https://openid.net/specs/openid-connect-core-1_0.html#ClaimsParameter)

* [OpenID Connect Discovery 1.0](https://openid.net/specs/openid-connect-discovery-1_0.html)
* [OpenID Session Management 1.0](https://openid.net/specs/openid-connect-session-1_0.html) 
* [OpenID.Front-Channel Logout 1.0](https://openid.net/specs/openid-connect-frontchannel-1_0.html)
* [OpenID.Back-Channel Logout 1.0](https://openid.net/specs/openid-connect-backchannel-1_0.html)
* [PKCE - RFC7636](https://tools.ietf.org/html/rfc7636) Proof Key for Code Exchange by OAuth Public Clients
* [RFC6749](https://tools.ietf.org/html/rfc6749) The OAuth 2.0 Authorization Framework
* [RFC6750](https://tools.ietf.org/html/rfc6750) The OAuth 2.0 Authorization Framework: Bearer Token Usage
* [RFC7662](https://tools.ietf.org/html/rfc7662) OAuth 2.0 Token Introspection
* [RFC7517](https://tools.ietf.org/html/rfc7517) JSON Web Key (JWK)
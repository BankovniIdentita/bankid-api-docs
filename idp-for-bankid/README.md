# APIs exposed by Identity Providers for Bank iD

Banks are required to implement APIs that are specified in this document, as that is what will be used by the RP. However for additional explanations and details, it is strongly recommended that readers are familiar with the specifications below.

## Changes

| Version | Note |
| ------------- |-------------|
| 2.0.0 | ```alg``` and ```x5c``` in JWK are not mandatory.<br>Removed ```loa2``` acr value as it is unsupported anymore.<br>Added string lengths in ```/ros``` endpoint.<br>First GitHub release. |
| 1.2.8 | Fixed missing ```iss``` and ```sub``` in JWT in ```/registration``` endpoint. |
| 1.2.7 | ```claims``` in auth endpoint request set se deprecated.<br>Fixed ```signObject_hash``` in ros endpoint.   |
| 1.2.6 | ```primary_nationality``` set se deprecated.  |

<details>
<summary>Old Changes</summary>
| 1.2.5 | Added support for additional types of id cards `OP` and `CA`, Czech Republic documents without machine readable zone.<br>Fixed typos in addresses and idcards scopes.<br>Fixed supported ```response_type``` in all endpoints to 'code'.<br>Fixed description for ```redirect_uri```, only https scheme is allowed.<br>Added query parameter ```basic_register``` to /profile endpoint. |
| 1.2.4 | Removed ```certificateProviderName``` from ```structured_scope```.<br>```scope``` in RefreshTokenRequest is now not mandatory.<br>New auth error callback ```user_not_eligible``` and error code for /profile endpoint. |
| 1.2.3 | ```certificateProviderName``` can now be correctly seen in ```structured_scope```.<br>Fixed description for ```document_language```.  |
| 1.2.2 | New scopes for Qualified signatures ```sign.qualified``` and ```sign.officially_certified```.<br>```valid_to``` in ```idcard``` is not mandatory.<br>```redirect_uri``` is now not mandatory when exchanging via ```refresh_token```.<br>```refresh_token``` is now not mandatory in /token response.  |
| 1.2.1 | Added parametr for Qualified signature ```certificateProviderName```.<br>Fixed some typos.<br>traceId ranamed to X-B3-TraceId and changed to 32 characters.  |
| 1.2.0 | Added traceId to all endpoints for support purposes.<br>Fixed some typos.<br>Modified for better code generation<br>Cleanup of unused objects.  |
| 1.1.16 | Fixed element ```paymentAccountsDetails```, it's array now instead of object.  |
| 1.1.15 | Fixed element ```idcard_hashes```, it's unrequired and specified types of idcards.  |
| 1.1.14 | New elements in /profile addresses (cityarea, evidencenumber) and payment accounts details<br>New types of id_cards by ROB<br>Fixed examples with miliseconds |
| 1.1.13 | New element ```idcard_hashes``` in **IDToken** and **AuthorizationIDToken** structures<br>Some elements in Document Objects may be empty  |
| 1.1.12 | New structuredScope in ros endpoint and id_token for multidocument sign.  |
| 1.1.11 | Added a new optional field in the request to /ros endpoint. This is a ```signObject_hash``` that is intended for those IDPs who do not want or cannot calculate its value. Bank iD will always send this value.  |
| 1.1.10 | The element time in the verification is now optional  |
| 1.1.9 | The time in verified_clamis.verification.time must be **with colon in date offset** (e.g. 2015-04-05T14:31:22+02:00)  |
| 1.1.8 | The ```priority``` parameter in the ```signObject``` element is now mandatory and unique. The affected service is /ros.<br>Added scope ```notification.claims_updated``` (the application wants to send notifications) for **/profile** and **/userinfo** endpoints  |
| 1.1.7 | Element ```verified_claims-verification.time``` changed to mandatory. Now, in case of sending a verification element, it is always necessary to send the date and time of the verification in the ISO 8601 format.  |
| 1.1.6 | Added ```birthcountry``` to /profile ```verified_claims``` element in response  |
| 1.1.5 | Correct response ```application/json``` on POST /ros endpoint<br>Added ```birthcountry``` element to /profile response  |
| 1.1.4 | Added missing definitions of ```introspection_endpoint``` elements in OIDCDiscovery schema  |
| 1.1.3 | A more well-arranged list of scopes (directly in the description of /userinfo and /profile)  |
| 1.1.2 | Added missing definitions of error responses at /revoke endpoint<br>Fixed error response format at /userinfo and /profile<br>Fixed examples for Algs in Discovery and types from String -> List<String>  |
| 1.1.1 | Added optional ```document_pages``` parameter to documentObject element in POST /ros endpoint<br>Added mandatory ```revocation_endpoint``` parameter in to discovery service GET /.well-known/openid-configuration<br>Added for better clarity complete possible list of parameters of ```claims``` element in ```verified_claims``` for services /userinfo and /profile  |
| 1.1.0 | new examples of requests /token-info and /revoke endpoints<br>addition of header parameters for POST, GET, PUT and DELETE /register endpoint<br>```structured_scope``` are not newly array type (POST /ros)<br>format of ```max_age``` element changed from date-time to number of seconds (POST /ros)  |
| 1.0.0 | the first version of the document  |
</details>

## Verified Data Representation extension for /userinfo resource

This extension to OpenID Connect wants to ensure that IDPs cannot mix up verified and unverified Claims and incidentally process unverified Claims as verified Claims.

The representation proposed therefore provides the IDP with the verified Claims within a container element verified_claims. This container is composed of the verification evidence related to a certain verification process and the corresponding Claims about the End-User which were verified in this process.

Verification elements contains the information about the process conducted to verify a person's identity and bind the respective person data to a user account.

## Authenication - Source material and relevant modifications:

* [OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html)
  * Signed and encrypted JWTs are used for /userinfo and /profile responses
  * HTTP POST requests are used for /token, /token_info and /revoke instead of GET requests, this is to avoid issues with query string length
  * Signed and encrypted JWT request object is referenced by the `request_uri` for the /auth endpoint
  * ID Token only contains `aud`, rest of the other user identifying claims are to be acquired from the KYC API
  * Signed and encrypted JWTs are used for any /userinfo calls and responses
  * In Bank iD's IDP relationship the UserInfo Claims MUST be returned as the signed and encrypted JSON object as required by definition during Bank iD Client Registration to IDP.
  * In Service Provider's Bank iD relationship the UserInfo Claims MUST be returned as the members of a JSON object unless a signed or encrypted response was requested during Client Registration.
  * The sub (subject) Claim MUST always be returned in the UserInfo Response.
  * If a Claim is not returned, that Claim Name SHOULD be omitted from the JSON object representing the Claims; it SHOULD NOT be present with a null or empty string value.
  * The sub Claim in the UserInfo and Profile Response MUST be verified to exactly match the sub Claim in the ID Token; if they do not match, the UserInfo Response values MUST NOT be used.
  * The UserInfo and Profile Endpoint MUST return a content-type header to indicate which format is being returned and if the response body is a text JSON object; the response body SHOULD be encoded using UTF-8.
  * If the UserInfo or Profile Response is signed and/or encrypted, then the Claims are returned in a JWT and the content-type MUST be application/jwt. The response MAY be encrypted without also being signed. If both signing and encryption are requested, the response MUST be signed then encrypted, with the result being a Nested JWT.
* [OpenID Connect Discovery 1.0](https://openid.net/specs/openid-connect-discovery-1_0.html)
  * `jwks_uri` is mandated instead of embedding `jwks`
  * Only asymmetric crypto is allowed, other options are omitted
  * X.509 certificate is specified using the `x5u` URI reference
  * JWK signing as well as encryption is assumed
  * `x5u` is removed in favor of `x5c`
  * `claims_supported` is REQUIRED
* [OpenID Connect Dynamic Client Registration](https://openid.net/specs/openid-connect-registration-1_0.html)
  * Notably, this API assumes that JWTs with asymmetric signatures and encryption will be used for the OIDC as well as service APIs when communicating between Bank and RP. For this reason, several fields and options are omitted. 
  * `jwks_uri` will be used rather than directly embedding `jwks`.
  * `scope` and `required_scope` properties are add over list of properties defined in OpenID.DynamicRegistration
  * Dynamic registration is protected using a bearer authentication where the token is a JWT signed using the keys of the RP

* [RFC6749](https://tools.ietf.org/html/rfc6749) The OAuth 2.0 Authorization Framework
* [RFC6750](https://tools.ietf.org/html/rfc6750) The OAuth 2.0 Authorization Framework: Bearer Token Usage
* [RFC7662](https://tools.ietf.org/html/rfc7662) OAuth 2.0 Token Introspection
* [draft-ietf-oauth-dyn-reg-management-11](https://tools.ietf.org/id/draft-ietf-oauth-dyn-reg-management-11.html) OAuth 2.0 Dynamic Client Registration Management Protocol
* [RFC7517](https://tools.ietf.org/html/rfc7517) JSON Web Key (JWK)
* [RFC7009](https://tools.ietf.org/html/rfc7009) OAuth 2.0 Token Revocation
* [OpenID Connect for Identity Assurance 1.0](https://openid.net/specs/openid-connect-4-identity-assurance-1_0.html) 
  * The `txn` Claim as defined in [RFC8417](https://tools.ietf.org/html/rfc8417) is used in the context of Bank iD data exchange to build audit trails across the parties involved in an OpenID Connect transaction. Claim txn is always REQUIRED in the userinfo response content.
  * This arrangement introduces the possibility for the bank to separate the verified Claims within a container element `verified_claims`. This container is composed of the verification evidence related to a certain verification process and the corresponding Claims about the End-User which were verified in this process.
  * Implementations MUST ignore any sub-element not defined in this specification or extensions of this specification.
  * In the case of this definition verification element MUST consist of the following elements:
    * `trust_framework`: REQUIRED. String determining the trust framework governing the identity verification process. For example, the value of ``cz_aml`` for verification according to the Czech AML law.
    * `time`: OPTIONAL. Time stamp in ISO 8601:2004 [ISO8601-2004] YYYY-MM-DDThh:mm:ss±hh format representing the date and time when identity verification took place.
    * `verification_process`: REQUIRED. In the case of this specification, the verification process shall include the identification number of the relevant bank where the initial physical verification of the client took place. This is the bank's identification number, which is kept in the list of regulated and registered entities of the CNB JERRS.
    * `claims`: The claims element contains the claims about the End-User that were verified during the defined verification process.
  * Verified Claims can be requested on the level of individual Claims about the End-User by utilizing the claims parameter as defined in Section 5.5. of the OpenID Connect specification [OpenID](https://openid.net/specs/openid-connect-core-1_0.html#ClaimsParameter)

## Authorization - Source material and relevant modifications:

 * [OpenID Financial-grade API](https://openid.net/specs/openid-financial-api-part-2-ID2.html#introduction-3) OpenID Financial-grade API - Part 2: Read and Write API Security Profile
 * [RFC6749](https://tools.ietf.org/html/rfc6749) The OAuth 2.0 Authorization Framework
 * [RFC7517](https://tools.ietf.org/html/rfc7517) JSON Web Key (JWK)
 * [Czech OpenBanking Standard](https://cbaonline.cz/upload/1061-cobs-rulebook-v04-1-1.pdf)

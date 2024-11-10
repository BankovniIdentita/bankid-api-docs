# APIs to be exposed by Service Providers for Bank iD

| Version | Note |
| ------------- |-------------|
| 2.0.0      | Removed ```sid``` from ```/back-channel/logout```<br>First GidHub release. |
| 1.2.0      | Added ```traceId``` for support purposes to all endpoints<br>Cleaned up unused components |
| 1.1.0     | Fixed error status code in ```/logout``` endpoint<br>Specified the case of JWT object encryption     |
| 1.0.0 | The first version of the document    | 

{
  "issuer": "https://idp.example.com",
  "authorization_endpoint": "https://idp.example.com/auth",
  "token_endpoint": "https://idp.example.com/token",
  "userinfo_endpoint": "https://idp.example.com/userinfo",
  "jwks_uri": "https://idp.example.com/.well-known/jwks",
  "registration_endpoint": "https://idp.example.com/register",
  "scopes_supported": ["openid", "profile.email"],
  "response_types_supported": ["code"],
  "response_modes_supported": ["query"],
  "grant_types_supported": ["authorization_code", "refresh_token"],
  "acr_values_supported": ["string"],
  "subject_types_supported": ["pairwise"],
  "id_token_signing_alg_values_supported": ["PS512"],
  "id_token_encryption_alg_values_supported": ["A256GCM"],
  "id_token_encryption_enc_values_supported": ["A256GCM"],
  "userinfo_signing_alg_values_supported": ["PS512"],
  "userinfo_encryption_alg_values_supported": ["A256GCM"],
  "userinfo_encryption_enc_values_supported": ["A256GCM"],
  "profile_signing_alg_values_supported": ["PS512"],
  "profile_encryption_alg_values_supported": ["A256GCM"],
  "profile_encryption_enc_values_supported": ["A256GCM"],
  "request_object_signing_alg_values_supported": ["PS512"],
  "request_object_encryption_alg_values_supported": ["A256GCM"],
  "request_object_encryption_enc_values_supported": ["A256GCM"],
  "token_endpoint_auth_methods_supported": ["private_key_jwt"],
  "token_endpoint_auth_signing_alg_values_supported": ["PS512"],
  "display_values_supported": ["page"],
  "service_documentation": "https://idp.example.com/docs",
  "claims_locales_supported": ["en-CA", "en"],
  "ui_locales_supported": ["cs", "en-US", "en"],
  "claims_parameter_supported": false,
  "request_parameter_supported": false,
  "request_uri_parameter_supported": true,
  "require_request_uri_registration": false,
  "op_policy_uri": "https://idp.example.com/policy",
  "op_tos_uri": "https://idp.example.com/tos",
  "backchannel_logout_supported": true,
  "claims_supported": ["string"]
}
**Source material and relevant modifications:**

* [OpenID.Core](https://openid.net/specs/openid-connect-core-1_0.html) OpenID Connect Core 1.0
* [OpenID.BackChannelLogout](https://openid.net/specs/openid-connect-backchannel-1_0.html) OpenID Connect Back-Channel Logout
* [OpenID.FrontChannelLogout](https://openid.net/specs/openid-connect-frontchannel-1_0.html) OpenID Connect Front-Channel Logout
* Logout is based on combination of `sid` and `iss`
* Back-Channel logout token itself is signed and can be encrypted JWT. Encryption is only applied if SeP has encryption set for the application and has a JWK endpoint issued.

# APIs exposed by Bank iD for Identity Providers

| Version | Note |
| ------------- |-------------|
| 1.2.3   | Fixed ```/notify``` endpoint description and added example.  |
| 1.2.2   | Fixed content-type to application/json in endpoint ```user-stat-data```<br>Added number of IdP records returned and ability to limit to IdP only records.<br>Fixed wrong body for ```/back-channel/logout``` in documentation  |
| 1.2.1   | Added endpoint ```user-stat-data```<br>Fixed required fields in ```notify``` response  |
| 1.2.0   | Added traceId to all endpoints for support purposes<br>Overall cleanup  |
| 1.1.1   | Clarified `signObject` and `documentObject` specification and examples<br>Clarified various property data types and examples throughout the signing process |
| 1.1.0   | fixed error status code in /logout endpoint  |
| 1.0.0   | the first version of the document    |

**Source material and relevant modifications:**

* [OpenID Connect Core 1.0](https://openid.net/specs/openid-connect-core-1_0.html)
* [OpenID Connect Back-Channel Logout 1.0](https://openid.net/specs/openid-connect-backchannel-1_0.html)
  * Logout is based on combination of `sub` and `aud` rather than `iss`
  * Logout token itself is signed and encrypted JWT

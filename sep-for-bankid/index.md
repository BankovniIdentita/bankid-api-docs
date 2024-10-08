# APIs to be exposed by Service Providers for Bank iD

| Version | Note |
| ------------- |-------------|
| 1.2.0      | added ```traceId``` for support purposes to all endpoints<br>cleaned up unused components |
| 1.1.0     | fixed error status code in ```/logout``` endpoint<br>specified the case of JWT object encryption     |
| 1.0.0 | the first version of the document    |

**Source material and relevant modifications:**

* [OpenID.Core](https://openid.net/specs/openid-connect-core-1_0.html) OpenID Connect Core 1.0
* [OpenID.BackChannelLogout](https://openid.net/specs/openid-connect-backchannel-1_0.html) OpenID Connect Back-Channel Logout
* [OpenID.FrontChannelLogout](https://openid.net/specs/openid-connect-frontchannel-1_0.html) OpenID Connect Front-Channel Logout
* Logout is based on combination of `sid` and `iss`
* Back-Channel logout token itself is signed and can be encrypted JWT. Encryption is only applied if SeP has encryption set for the application and has a JWK endpoint issued.

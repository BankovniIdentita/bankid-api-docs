# Bank iD

Bank iD technical specification.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC2119](https://www.ietf.org/rfc/rfc2119).

## What is Bank iD?

Bank iD acts as a middleman, between the Service Provider (SeP) and the End-User's Bank. Bank iD gives the user an option to authenticate against the SeP using their Bank credentials and later allows the SeP to acquire Bank verified data and Personally Identifiable Information (PII) of the End-User.

The main goals of the Bank iD system are:
* To streamline authentication experience for the End-User during onboarding to Service Provider with the End-User's pre-existing Bank account
* To allow Service Providers access to Bank-verified personal data for
  * Authorization - for example: Is the End-User over 18 years of age? Can I sell them alcohol?
  * PII verification - Is this End-User who they claim they are?
  * Compliance with Anti-Money Laundering (AML) laws and regulations through the use of Know Your Customer (KYC) API.

## Bank iD system actors

- IdP - An entity which provides authentication and KYC services, eg. bank.
- End-User - A person that has an account in the Bank and wants to use it for authentication.
- Service Provider (SeP) - A Third party which provides service to the End-User. Uses Bank iD to get additional Bank-verified information about the End-User.
- Bank iD - A service that sits between the SeP and the Bank.

## What is Bank iD on a technical level?

Bank iD exposes two sets of REST interfaces - one for IdPs and one for Service Providers. These are based on the [OpenID Connect](https://openid.net/connect/) and [OAuth2](https://oauth.net/2/) specifications. The specification is followed as closely as possible to allow for easy interoperability with existing solutions and code - which SHOULD decrease overall development and maintenance costs.

The APIs are described using a set of OpenAPI specifications for communication between Service Providers and Bank iD:

- [Bank iD for Service Providers](https://github.com/BankovniIdentita/bankid-api-docs/tree/main/bankid-for-sep)
- [Service Providers for Bank iD](https://github.com/BankovniIdentita/bankid-api-docs/tree/main/sep-for-bankid)

The APIs are described using a set of OpenAPI specifications for communication between Identity Providers and Bank iD:

- [Bank iD for Identity Providers](https://github.com/BankovniIdentita/bankid-api-docs/tree/main/bankid-for-idp)
- [Identity Providers for Bank iD](https://github.com/BankovniIdentita/bankid-api-docs/tree/main/idp-for-bankid)

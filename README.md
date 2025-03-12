# DOME Trust Framework

## Introduction

The DOME Trust Framework is a set of rules and guidelines that define the trust relationships between the different entities in the DOME network. The framework is composed of the following trusted lists:

## Trusted Lists
* Trusted Services List
* Trusted Access Node Operators List
* Trusted Schemas List
* Revoked Credential List
* Invalid Credentials List

## How-To Guides

### How-To insert a new value in the Trusted Lists

1. Fork the repository
2. Select the environment you want to add the organization to
3. Edit the YAML file adding your values
4. Create a pull request
5. Wait for the pull request to be approved → This will need to be verified by the DOME Operator.
6. If the pull request is approved, the data will be added to the directory

### Which data is needed to set a new entry into the Trusted Services List?

The trusted services list contains all the verified and authorized services within the dome ecosystem. these services have met the required standards for secure and trusted interactions. To add a new entry to the trusted services list, specific information must be provided in a yaml file, adhering to the structure outlined below.

| **Field**                                       | **Description**                                                                                                                                                                                                                                                                          |
|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **clientId**                                    | Should be a `did:key` or a unique identifier for your client. Using a `did:key` allows the verifier to obtain your public keys for signature verification without needing a separate JWKS endpoint.                                                                                      |
| **url**                                         | The base URL of your service or application.                                                                                                                                                                                                                                             |
| **redirectUris**                                | Must include all the URLs where you expect to receive authentication responses. These should be HTTPS URLs to ensure secure communication.                                                                                                                                               |
| **scopes**                                      | Currently, only `openid_learcredential` is accepted. This scope allows your service to request the necessary credentials.                                                                                                                                                                |
| **clientAuthenticationMethods**                 | Must be set to `["client_secret_jwt"]`, as this is the only supported authentication method.                                                                                                                                                                                             |
| **authorizationGrantTypes**                     | Must be set to `["authorization_code"]`, as this is the only supported grant type.                                                                                                                                                                                                       |
| **postLogoutRedirectUris**                      | Include URLs where users should be redirected after they log out from your service.                                                                                                                                                                                                      |
| **requireAuthorizationConsent**                 | Set to `false` because explicit user consent is not required in this flow.                                                                                                                                                                                                               |
| **requireProofKey**                             | Set to `false` as PKCE is not utilized.                                                                                                                                                                                                                                                  |
| **jwkSetUrl**                                   | If you're using a `did:key` for your clientId, you do not need to provide a `jwkSetUrl` because the verifier can derive your JWKS directly from the `did:key`. However, if you're not using a unique identifier, you must provide the `jwkSetUrl` where your public keys can be fetched. |
| **tokenEndpointAuthenticationSigningAlgorithm** | Must be set to `ES256`, as this is the only supported algorithm.                                                                                                                                                                                                                         |

#### example yaml entry

```yaml
clients:
  - clientId: "did:key:zDnaeypyWjzn54GuUP7PmDXiiggCyiG7ksMF7Unm7kjtEKBez"
    url: "https://dome-marketplace-sbx.org"
    redirectUris: ["https://dome-marketplace-sbx.org/auth/vc/callback"]
    scopes: ["openid_learcredential"]
    clientAuthenticationMethods: ["client_secret_jwt"]
    authorizationGrantTypes: ["authorization_code"]
    postLogoutRedirectUris: ["https://dome-marketplace-sbx.org/"]
    requireAuthorizationConsent: false
    requireProofKey: false
    jwkSetUrl: "https://verifier.dome-marketplace-sbx.org/oidc/did/did:key:zDnaeypyWjzn54GuUP7PmDXiiggCyiG7ksMF7Unm7kjtEKBez"
    tokenEndpointAuthenticationSigningAlgorithm: "ES256"
```

### Which data is needed to set a new entry into the Trusted Invalid Credentials List?

You need to add the Verifiable Credential ID that you want to invalidate.

### Which data is needed to set a new entry into the Trusted Revoked Credentials List?

You need to add the Verifiable Credential ID that you want to invalidate.

### Which data is needed to set a new entry into the Trusted Access Node Operators List?

The Access Node directory contains the public data for organizations within the DOME network.
For detailed instructions on how to collect or create your own data,
please refer to the [How to Deploy - Previous steps](https://github.com/DOME-Marketplace/access-node#previous-steps)
section of the Access Node Guide.

The guide provides step-by-step instructions for generating your data using the 
[DOME Access Node Key Generator](https://dome-marketplace.github.io/dome-crypto-generator/).
The generated data is stored in a YAML file, which includes the following information:
```yaml
organizations:
  - name: "Organization 1"
    dlt_address: "0x43b27fef24cfe8a0b797ed8a36de2884f9963c0c2a0da640e3ec7ad6cd0c493d"
  - name: "Organization 2"
    dlt_address: "0xb794f5ea0ba39494ce83...9613fffba74279579268"
```

> NOTE: The `dlt_address`must be the Ethereum Address of the organization's Access Node.



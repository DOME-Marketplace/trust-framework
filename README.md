# DOME Trust Framework

## Introduction

> TODO: Add a brief description of the DOME Trust Framework

## Trusted Lists
* Trusted Issuers List
* Trusted Participants List
* Trusted Services List
* Trusted Access Nodes List
* Trusted Schemas List
* Revocation List

## How-To Guides

### How-To insert a new Access Node Participant in the Trusted Access Nodes List

The directory of the Access Node contains the public data of the organizations that are part of the DOME network. 
The data is stored in a YAML file that contains the following information:
```yaml
organizations:
  - name: "Organization 1"
    publicKey: "Mg5v8CDaEnJkSJfP1Q6Q6Q=="
    url: "https://organization1.com"
    dlt_address: "0x43b27fef24cfe8a0b797ed8a36de2884f9963c0c2a0da640e3ec7ad6cd0c493d"
  - name: "Organization 2"
    publicKey: "EsThbaGlaZIPB6xN6Q6Q6Q=="
    url: "https://123.162.194.139:8080"
    dlt_address: "0xb794f5ea0ba39494ce83...9613fffba74279579268"
```

> NOTE: The `publicKey` field is the public key of the organization that is used to verify the signature of the JWT token. It is the same public key related to the EthereumAddress of the organizations used in the DLT-Adapter.

> NOTE 2: The `url` must be the URL of the organization's Access Node, and it can be an IP address or a domain.

> NOTE 3: The `dlt_address`must be the Ethereum Address of the organization's Access Node.

#### Steps:
1. Fork the repository
2. Select the environment you want to add the organization to.
3. Edit the `trusted_access_nodes_list.yaml` file within the selected environment folder.
4. Create a pull request
5. Wait for the pull request to be approved --> This will need to be verified by the onboarding organization.
6. The organization will be added to the directory

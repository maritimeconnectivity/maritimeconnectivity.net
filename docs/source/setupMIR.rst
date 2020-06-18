Setting up MIR
==============
If your organizations wishes to connect to MCP as an Identity Provider, to enable your uses to authenticate in MCP, please contact Oliver Haagh at oliver@dmc.international in order to set it up. Note that currently you need to expose interfaces that supports either OpenID Connect or SAML2.

Within the scope of the EfficienSea2, STM validation, and SMART navigation projects, organizations can get users registered in a special kind of Identity Providers, supplied by MCP. To join MCP please fill out the form at Apply.

Introduction
^^^^^^^^^^^^
The MCP Identity Registry (MIR) is an identity solution targeted against actors of the maritime domain. It consists of three parts – an identity broker for logging in and federating users from other identity providers, a public key infrastructure for issuing and managing digital certificates and an API for management and access to the two first parts.
For the identity broker Keycloak has been chosen as it is open source and because it is based on OpenID Connect which is a widely used protocol for token based authentication.
This document will provide a generic guideline of how to setup and deploy the MIR on a local system.
The MCP is formerly known as the Maritime Cloud and therefore there will still be references to that in this document.
As the different components of the MIR rely on each other the configuration of one component may rely on the configuration of another component, but this will be documented as thoroughly as possible.
Complementary documentation of setup can be found at:
- https://github.com/MaritimeConnectivityPlatform/IdentityRegistry
- https://github.com/MaritimeConnectivityPlatform/MCP-PKI
- https://github.com/MaritimeConnectivityPlatform/MCPKeycloakSpi
For easier management of the IR API it is advised to also setup the MCP management portal. The code for this can be found at https://github.com/MaritimeConnectivityPlatform/MCP-Portal.
A running instance of MCC testbed can be found at https://management.maritimecloud.net/.

Prerequisites
^^^^^^^^^^^^^
- Java JDK 8 (OpenJDK is preferred, but not a requirement)
- Maven 3+
- A running MySQL/MariaDB instance with databases and users created
- Keycloak 9.0.0 (Only needed if not using the Docker image)
- NGINX
- Docker (if you want to run the identity registry using Docker containers)
- A SMTP server

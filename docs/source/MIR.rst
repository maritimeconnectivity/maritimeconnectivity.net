.. _mir:

Maritime Identity Registry (MIR)
================================
Maritime Identity Registry (MIR for short) is an identity provider and an authority for identities of persons, organizations or ships that are using the MCP.
Technically MIR consists of a PKI library and a RESTful API for managing identities and certificates which are standardized by MCC.
Under the API MIR can authenticate an user, based on two methods:

* Public Key Infrastructure (PKI): :ref:`PKI description link<mcp-pki>`.
* Open ID Connect (OIDC): :ref:`OIDC description link<mcp-oidc>`.

MIR API accepts either a certificate (PKI) or a token (OIDC) for user authentication.
After the authentication and following authorization, the user can register and manage the entities through the MIR API, with a proper right what we defined as a role.
One important feature on the management is to issue or revoke a X509 client certificate for entities that are already registered in the API database.

Identity Management
^^^^^^^^^^^^^^^^^^^
Identity management refers to the process of employing technologies to manage information about the identity of users and control access to company resources. The goal of identity management is to improve productivity and security while lowering costs associated with managing users and their identities, attributes, and credentials.

The goal of MIR is to create a solution that satisfies the most common identification needs for the entire maritime industry on a global scale.

This is not a simple task as any solution must support every possible user scenarios from small leisure sailors to multinational companies. The complexity of this task is why the functionality will be delivered over multiple milestones in the coming years. The most important things such as support for authentication will be implemented first. Additional functionality will be added based on user needs in the projects supported by MCP.

Brokered User Federation
^^^^^^^^^^^^^^^^^^^^^^^^
In most federated setups it starts from the website (Service Provider) that need authentication and the identity provider, normally presented with a "Log in with X" link, where X could be Facebook, Google, etc. MCP has 2 steps for it, where the first step is MCP Identity Broker which presents the user with a list of available identity providers, which is the second step.
For a deeper understanding of how this is actually done please read the `Identity Broker overview section from the Keycloak manual <https://www.keycloak.org/docs/latest/server_admin/index.html#_identity_broker_overview>`__.

MCP supports the brokered user federation as long as non-MCP identity providers follow OAuth 2.0 by means of the federation of identity providers.
The federation is the means of linking distinct identity management systems to a person’s electronic identity and attributes. For example, a shipping company might expose all their users in LDAP or Active Directory to MCP in such a way as they appear as MCP users. Thereby bypassing the need to manage their users directly in MCP. This also means that MCP is not responsible for management of users.
In practical terms, federation means that users asked to authenticate in MCP will be redirected to a login webpage supplied by their organization where they can login using their organizational id.
Since the authentication process is the responsibility of the organizations, it is also up to the individual organizations to choose an appropriate authentication method. While most will likely use classic username/password authentication, multi factor security, biometric security or other approaches could be used.

What MCC governs in MIR
^^^^^^^^^^^^^^^^^^^^^^^
* :ref:`MCP types and its hierarchy <mcp-type>`
* :ref:`PKI certificate profile <mcp-pki-cert-profile>`
* :ref:`OIDC Token <mcp-token>`
* REST API (https://test-api.maritimecloud.net/v2/api-docs)
* MCP Instance Provider root CA list
* MIR reference implementation

MIR reference implementation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
MCC governs the reference implementations on MIR as follows:

* MCP-PKI library for handling certificates: https://github.com/MaritimeConnectivityPlatform/MCP-PKI
* MIR API: https://github.com/MaritimeConnectivityPlatform/IdentityRegistry
* MIR Identity Broker: https://github.com/MaritimeConnectivityPlatform/MCPKeycloakSpi

MIR Identity Broker which enables the token-based user authentication is based on `Keycloak <https://www.keycloak.org/>`__ which is an OpenID Connect (OIDC) server developed by Red Hat, but including two MCP specific plugins for synchronization of user data with MIR API and converting MCP client certificates to OIDC tokens.
Giving a detailed account of the synchronization part when the API is called to create a new user with corresponding information it is registered in the API database and also the ID Broker accounts.
The synchronization is provoked when a user logs in using an external identity provider by registering the user’s information to the API database.
In our testbed we use the federation to enable the participants across different projects to register and utilize MCP services established by the projects, as well as validate the identity management concept of MCP.

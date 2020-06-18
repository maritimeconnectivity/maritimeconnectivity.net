Maritime Identity Registry (MIR)
================================
MIR is an authority for identities of persons, organizations or ships that are using the MCP.
The main technical components enabling MIR are:

* MIR API: https://github.com/MaritimeConnectivityPlatform/IdentityRegistry
* MIR Identity Broker: https://github.com/MaritimeConnectivityPlatform/MCPKeycloakSpi

Both use the special MCP-PKI library for handling certificates: https://github.com/MaritimeConnectivityPlatform/MCP-PKI

MIR itself can be described as a RESTful API for managing maritime identities and PKI.
MIR API uses ID Broker for OIDC token-based user authentication.
After the authorization, the user can register and manage the entities through the MIR API, with a proper right what we defined as a role.
One important feature on the management is to issue or revoke a X509 client certificate for entities that are already registered in the API database.

MIR Identity Broker is based on `Keycloak <https://www.keycloak.org/>`__ which is an OpenID Connect (OIDC) server developed by Red Hat, but including two MCP specific plugins for synchronization of user data with MIR API and converting MCP client certificates to OIDC tokens.
Giving a detailed account of the synchronization part when the API is called to create a new user with corresponding information it is registered in the API database and also the ID Broker accounts.
The synchronization is provoked when a user logs in using an external identity provider by registering the user’s information to the API database.
As long as the external identity provider follows OAuth 2.0, it can be configured as the federation of identity providers.
In our testbed we use the federation to enable the participants across different projects to register and utilize MCP services established by the projects, as well as validate the identity management concept of MCP.

[Configuration manual (third party dependencies of reference implementation)]

Identity Management
^^^^^^^^^^^^^^^^^^^
Identity management refers to the process of employing technologies to manage information about the identity of users and control access to company resources. The goal of identity management is to improve productivity and security while lowering costs associated with managing users and their identities, attributes, and credentials.

The goal of the Maritime Identity Registry is to create a solution that satisfies the most common identification needs for the entire maritime industry on a global scale.

This is not a simple task as any solution must support every possible user scenarios from small leisure sailors to multinational companies. The complexity of this task is why the functionality will be delivered over multiple milestones in the coming years. The most important things such as support for authentication will be implemented first. Additional functionality will be added based on user needs in the projects supported by MCP.

Brokered User Federation
^^^^^^^^^^^^^^^^^^^^^^^^
In the previous section we discussed digital certificates for use in machine to machine communication. There are no technical reasons to why human users should not be able to use digital certificates to authenticate themselves as well. However, there are some serious practical issues that make it difficult to see them as a general solution for human user authentication. The first issue being that it requires that the certificate must always be present on the computer or mobile phone from which access is made. This is normally not a problem for machine to machine communication. Because, once installed the hardware configuration almost never changes. Unlike human users that use their computer during the day to access information, their mobile phone on the way back from work and their tablet in the evening from home. Making sure that certificates are installed on all these devices and refreshing them once they expire is a lot of effort to require from users. We believe having such a complicated setup would be a major barrier towards successful adoption of MCP. So for now, authentication of human users in MCP will be based on login through a web browser, using brokered federation.

Federation is the means of linking distinct identity management systems to a person’s electronic identity and attributes. For example, a shipping company might expose all their users in LDAP or Active Directory to MCP in such a way as they appear as MCP users. Thereby bypassing the need to manage their users directly in MCP. This also means that MCP is not responsible for management of users. In practical terms, federation means that users asked to authenticate in MCP will be redirected to a login webpage supplied by their organization where they can login using their organizational id.

Since the authentication process is the responsibility of the organizations, it is also up to the individual organizations to choose an appropriate authentication method. While most will likely use classic username/password authentication, multi factor security, biometric security or other approaches could be used.

What MCC governs in MIR
^^^^^^^^^^^^^^^^^^^^^^^
* MCP types and its hierarchy
* PKI certificate profile
* OIDC Token
* REST API
* MCP Instance Provider root CA list

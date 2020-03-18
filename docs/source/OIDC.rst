Open ID Connect (OIDC)
======================
`OpenID Connect <https://openid.net/connect>`__ is the protocol chosen to be used for user federation in MCP, and it should be supported by Service Providers. It is an interoperable authentication protocol based on the `OAuth 2.0 <https://oauth.net/2/>`__ family of specifications. It uses straightforward REST/JSON message flows with a design goal of "making simple things simple and complicated things possible". It’s uniquely easy for developers to integrate, compared to any preceding Identity protocols.

OpenID Connect lets developers authenticate their users across websites and apps without having to own and manage password files. For the app builder, it provides a secure verifiable, answer to the question: "What is the identity of the person currently using the browser or native app that is connected to me?"

OpenID Connect allows for clients of all types, including browser-based JavaScript and native mobile apps, to launch sign-in flows and receive verifiable assertions about the identity of signed-in users.

OpenID Connect provides authentication details in JWT tokens, that can be encrypted or digitally signed.

MCP User Federation Setup
^^^^^^^^^^^^^^^^^^^^^^^^^^
In most federated setups there is 1 step from the website (Service Provider) that need authentication and the Identity Provider, normally presented with a "Log in with X" link, where X could be Facebook, Google, etc. The setup used in MCP has 2 steps, where the first step is MCP Identity Broker which presents the user with a list of available Identity Providers, which is the second step. For a deeper understanding of how this is actually done please read the Identity Broker overview section from the Keycloak manual. Keycloak is the software used for MCP Identity Broker.

MCP expects the following attributes in the OpenID Connect JWT Access Token:

These attributes will be directly mapped from attributes provided by the organizations Identity Provider, so the Identity Provider must also provide these attributes, except for the "org"-attribute.

Authentication Flow
^^^^^^^^^^^^^^^^^^^
To illustrate the authentication flows the sequence diagrams below is provided.

The first diagram below shows the standard `OpenID Connect Authorization Code Flow <http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth>`__ involving a browser being used by the user to access a service in the form of a webpage.

The second diagram shows the flow used when an authenticated user is accessing a backend service. For browser based services this scenario is often used when the browser retrieves data from backend services. In this scenario since the user is authenticated, the user has a token that is presented for authentication for the backend service.

Keycloack
^^^^^^^^^^
Keycloak is one of many products that includes support for OpenID Connect, and it is the product that currently provides MCP Identity Broker which is the cornerstone in MCP user federation.

Keycloak is an open source product developed by RedHat. Keycloak can be set up to work in different ways. It can be set up as an Identity Broker in which case it will link to other Identity Providers, which is what MCP Identity Broker does, or it can be set up to work as an Identity Provider, using either a database or LDAP/AD as a backend. Due the ability to connect to LDAP/AD, Keycloak can be used as quick and easy way to set up a Identity Provider.

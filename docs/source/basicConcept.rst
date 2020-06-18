.. _mcp-basic-concept:

Basic Concept
===============

Maritime Connectivity Platform (MCP) is a service-oriented architecture that is composed of three core components, namely MIR, MSR, and MMS.

  * Maritime Identity Registry (MIR): MIR has the objective to enable an authentication of all maritime stakeholders in the context of the Maritime Connectivity Platform and thus increasing the security and reliability of communication. This goal is archived by providing a trustworthy infrastructure for identity authentication of maritime entities like human actors, services and devices.
  * Maritime Service Registry (MSR): MSR is supposed to serve as a central reference point to provide and find services and thus to improve the visibility and accessibility of available information and services in the maritime domain. It’s best compared with a yellow pages phone book.
  * Maritime Messaging Service (MMS): MMS offers secure and efficient communication for the maritime domain. MMS is a message broker platform that delivers message to destination through both IP and non-IP communication channel by utilizing Maritime Resource Name (MRN) as endpoint address.

Authentication
--------------
Authentication is any process by which a system verifies the identity of a user (human or machine) who wishes to access it. Since access control is normally based on the identity of the user who requests access to a resource, authentication is essential to efficient security. In contrast to identification which refers to the act of stating a person or thing’s identity, authentication is the process of actually confirming the stated identity. It might involve verifying the authenticity of a website by a digital certificate that it provides, or validating a persons identity documents.

The way in which a human user or machine may be authenticated typically falls into three different categories, based on what is commonly known as the factors of authentication: something the user knows, something the user has, and something the user is. Each authentication factor covers a range of elements used to authenticate or verify a person’s identity prior to being granted access, approving a transaction request, signing a document or other work product, granting authority to others, and establishing a chain of authority.

* Knowledge factors: Passwords, passphrases, pins, challenge response,

* Ownership factors: ID card, Cell phone, authentication certificates,

* Inheritance factors: Fingerprint, retinal patterns, face, voice,

Currently the implementation effort in MCP is concentrating on passwords for human users and authentication certificates for machine users. In the future we will probably add more methods.

While the difference of using authentication certificates or passwords might seem minor from a user perspective the underlying implementation and usage is radically different which is why it has been split into different sections.

How MIR authenticate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Please refer 'OIDC' and 'Certificate' for the details.


OIDC Authentication Flow
^^^^^^^^^^^^^^^^^^^^^^^^^^
To illustrate the authentication flows the sequence diagrams below is provided.

The first diagram below shows the standard `OpenID Connect Authorization Code Flow <http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth>`__ involving a browser being used by the user to access a service in the form of a webpage.

.. image:: _static/image/oidc_authentication_flow.png
    :align: center
    :alt: the sequence diagram of cert authentication flow

The second diagram shows the flow used when an authenticated user is accessing a backend service. For browser based services this scenario is often used when the browser retrieves data from backend services. In this scenario since the user is authenticated, the user has a token that is presented for authentication for the backend service.

.. image:: _static/image/backend_service_authentication_flow.png
    :align: center
    :alt: the sequence diagram of cert authentication flow

Certificate Authentication Flow
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
To illustrate the authentication flow using a certificate the sequence diagram below is provided.

.. image:: _static/image/cert_authentication_flow.png
    :align: center
    :alt: the sequence diagram of cert authentication flow

Obtaining an OIDC Token using a Certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
It is possible to obtain OpenID Connect Tokens using certificate authentication. The idea is that instead of authenticating by being redirected to an Identity Provider as in the normal OpenID Connect flow, you authenticate at the Identity Broker by using your certificate (that has been issued by MCP Identity Registry). This authentication would work in the same way as when authenticating to any service. When authentication has been succesful the Identity Broker can then issue a JWT-token, which is what the OpenId Connect authentication use. So in effect what we have is a "bridge" between the 2 authentication approaches.

An example of use could be that a device (which has been issued certificates) wishes to authenticate securely with a service, but the service only supports OpenId Connect authentication. Using the approach mentioned above, the device can use its certificate to get an OpenId Connect token, which can then be used to authenticate to the service.

The flow looks like the diagram below:

.. image:: _static/image/diagram_oidc_authentication_using_cert.png
    :align: center
    :alt: getting a token from certificate

Example of Obtaining a OpenId Connect Token using a Certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In this simple example we will assume that a certificate and key—​pair has been issued to the entity who wishes to authenticate. This example makes use of curl a commandline tool available on Linux and Mac OS X.

The authentication involves 2 steps:

1. Obtaining a temporary Authorization Code using a certificate.
2. Obtaining a OpenId Connect Token using the Authorization Code.

These 2 steps are actually standard in the OpenID Connect Authorization Code Flow, though normally certificates are not the standard authentication method.

First we obtain the code by issuing this command::

  curl --verbose --location --cookie "" --key PrivateKey.pem --cert Certificate.pem 'https://maritimeid.maritimecloud.net/auth/realms/MaritimeCloud/protocol/openid-connect/auth?client_id=cert2oidc&redirect_uri=http%3A%2F%2Flocalhost%3A99&response_type=code&kc_idp_hint=certificates&scope=openid'

Let us break down the command:

* ``curl --verbose --location --cookie ""``: ``curl`` is the tool itself. ``--verbose`` means it will be in verbose mode, ``--location`` means curl will follow HTTP redirects and ``--cookie ""`` activates the use of HTTP cookies which means that cookies received will be remember and used during redirects. We need to follow redirects since that is used by OpenID Connect to go back and forth between servers, and the verbose mode is needed because we would like to see where we are redirected — especially the last redirect, but more about that later.

* ``--key PrivateKey.pem --cert Certificate.pem``: Here the private key and the certificate is given to curl in PEM format.

* The last part is the URL which itself is multiple parts:

   * Address of the authentication endpoint: ``https://maritimeid.maritimecloud.net/auth/realms/MaritimeCloud/protocol/openid-connect/auth``

   * Parameters: ``client_id=cert2oidc&redirect_uri=http%3A%2F%2Flocalhost&response_type=code&kc_idp_hint=certificates&scope=openid``. These can be also be broken down:

    + ``client_id=cert2oidc``: This is a special OpenID Connect client setup to be used for certificate authentication.

    + ``redirect_uri=http%3A%2F%2Flocalhost%3A99``: This is where the authentication server will redirect to at the end of the authentication. The parameter is URL encoded and decoded looks like this: http://localhost:99. This address is meant to be invalid, since we want the last redirect to fail.

    + ``response_type=code``: This defines that we uses the Authorization Flow as mentioned above.

    + ``kc_idp_hint=certificates``: This tells the Identity Broker that we wants to authenticate using the Certificate Identity Provider.

    + ``scope=openid``: And finally, this define that we are using OpenID Connect.

When the command runs it returns a lot of output, due to being in verbose mode. We will not go into detail, but quite a few redirects happens, as described in the sequences diagram above. The last redirect however fails, which is intended. The final output will look something like this::

  * Issue another request to this URL: 'http://localhost:99?code=uss.Yw6k4rXOJiR6IF4a2Y7tYC1-Eqoo8dHSUwjfuIFDfpI.543a63db-9d22-45f7-85b6-a258059c0825.6826c662-6b68-423a-a248-71bd3e69dab0'
  * Rebuilt URL to: http://localhost:99/?code=uss.Yw6k4rXOJiR6IF4a2Y7tYC1-Eqoo8dHSUwjfuIFDfpI.543a63db-9d22-45f7-85b6-a258059c0825.6826c662-6b68-423a-a248-71bd3e69dab0
  *   Trying 127.0.0.1...
  * connect to 127.0.0.1 port 99 failed: Connection refused
  * Failed to connect to localhost port 99: Connection refused
  * Closing connection 1
  curl: (7) Failed to connect to localhost port 99: Connection refused


Here we can recognize ``http://localhost:99`` from the ``redirect_uri`` parameter described earlier. We can also see that the ``code`` parameter is in the url, in this case with the value ``uss.Yw6k4rXOJiR6IF4a2Y7tYC1-Eqoo8dHSUwjfuIFDfpI.543a63db-9d22-45f7-85b6-a258059c0825.6826c662-6b68-423a-a248-71bd3e69dab0``. It is this code we need to in the second step of authentication to get the OpenID Connect Tokens. The code is only valid for a very limited time (less than a minute) and can only be used once. We will again use ``curl`` in the second step::

  curl --data "grant_type=authorization_code&client_id=cert2oidc&code=uss.Yw6k4rXOJiR6IF4a2Y7tYC1-Eqoo8dHSUwjfuIFDfpI.543a63db-9d22-45f7-85b6-a258059c0825.6826c662-6b68-423a-a248-71bd3e69dab0&redirect_uri=http%3A%2F%2Flocalhost%3A99" https://maritimeid.maritimecloud.net/auth/realms/MaritimeCloud/protocol/openid-connect/token

Again, let us break down the command. In this case the command consist of 3 parts, ``curl`` — the tool itself, data-parameters and an URL. We will concentrated on the data-parameters. Note that this is a HTTP POST request, which is why the parameters is supplied in a separate argument and not as part of the URL.

* ``grant_type=authorization_code``: This specifies that we will use an authorization code to authenticate ourself in this call.

* ``client_id=cert2oidc``: The id of the special client, as mentioned above.

* ``code=uss.Yw6k4rXOJiR6IF4a2Y7tYC1-Eqoo8dHSUwjfuIFDfpI.543a63db-9d22-45f7-85b6-a258059c0825.6826c662-6b68-423a-a248-71bd3e69dab0``: The code we obtained earlier.

* ``redirect_uri=http%3A%2F%2Flocalhost%3A99``: The redirect url, the same as before, though not used for actual redirection in this case.

When this call runs there will be no redirection, so we do not need to tell curl to follow redirects. Instead the returned output will be the tokens that we wish to use, in a format like this::

  {
    "access_token":"eyJhbGciOiJ...uXoHudIM1yiDBYj8g",
    "expires_in":300,
    "refresh_expires_in":1800,
    "refresh_token":"eyJhbGciOiJ...iv7rKSa__IKy983Gg",
    "token_type":"bearer",
    "id_token":"eyJhbGciOiJ...Ycp2GupfpTTgRkhtnw",
    "not-before-policy":0,
    "session_state":"94487eaa-b77f-4b6c-8db1-c574fc6a09da"
  }

The access_token is the token that should be used we communicating with services in MCP context. The token should be embedded in the HTTP header. When using curl it can be done like this::

  curl -H "Authorization: Bearer eyJhbGciOiJ...uXoHudIM1yiDBYj8g" https://api.maritimecloud.net/oidc/api/org/DMA

The refresh_token is used to re-authenticate to get a new set of tokens when the access_token has expired, in this case 300 seconds after it has been issued, as seen in the expires_in attribute. The new set of tokens can then be obtain with a HTTP POST like this::

  curl --data "grant_type=refresh_token&client_id=cert2oidc&refresh_token=eyJhbGciOiJ...iv7rKSa__IKy983Gg" https://maritimeid.maritimecloud.net/auth/realms/MaritimeCloud/protocol/openid-connect/token

Authorization
--------------
Another central aspect of Identity Management is the concept of authorization which is the process of determining a set of permissions that is granted to a specific trusted identity. In all practical senses, authorization follows authentication. Once a system knows who you are, the system can determine what is appropriate for you to be able to see or do. authorization can be determined based on the user identity alone, but in most cases requires additional attributes about the user, such as role, title, flag state, etc.

Authorization can typically be handled in two ways.

Locally by the application or service that is being accessed.

Centralizing the authorization policy decisions regardless of the location of the user or the application/service

Since authorization can always be done locally by the application that is being accessed, for example by storing user rights in a local database, we have decided that MCP will not prioritize central support for authorization for the next milestones. Instead focusing on getting authentication right.

Before implementation of centralized support for authorization can begin there are some obstacles that lie ahead. Mainly because there, unlike authentication, are no good standards for doing authorization.

Even though there are no real standards there are a number of approaches that are commonly used. The most commonly used probably being role-based access control (RBAC). RBAC is an access control mechanism defined around roles and privileges. The components of RBAC such as role-permissions, user-role and role-role relationships make it simple to do user assignments of entitlements. However, adopting RBAC for MCP opens some questions. For example, who defines the roles and are they global roles. Or are they local to a particular service or a particular organization. For example, an "administrator" role might entail a list of certain privileges in one organization and another list of privileges in another organization.

Given these issues and many other we have to decide not to implement central authorization in MCP. Instead MCP will provide the information that can be used for authorization in the services.

As described in the sections about [OpenID Connect] and [Certificate Attributes], both authentication methods provides information about the authenticated user that can be used for authorization:

* The organization the entity belong to.

* The permissions/roles/groups the entity has been assigned by the organization.

When an organization wishes to use a service, the organization will then make an agreement with that about how access levels shall be defined in that service, based on the permissions. This will have to be done for each service the organization wishes to use.

Authorization in MIR
^^^^^^^^^^^^^^^^^^^^

As an example of how authorization can be done, let us have a look at how it is handled inside the MCP Identity Registry. When it comes to authorization, the Identity Registry will have the same information about its users as any other service in MCP.

The Identity Registry currently has these roles:

A few things should be noted:

* "Maintain" (as mentioned in the table above) means to be able to create, update and delete, as well as issuing and revoking certificates.

* Excluding entities with the role ROLE_SITE_ADMIN, it is not possible for entities to see entities from other organizations.

* A ROLE_SITE_ADMIN can maintain entities and organizations beyond his own organization.

* Any entity, regardless of roles, can see all entities from its own organization, though some sensitive information from services is filtered for non-admins.

* Only a ROLE_SITE_ADMIN can assign ROLE_SITE_ADMIN and ROLE_APPROVE_ORG roles.

* A ROLE_APPROVE_ORG can create a user for an organization if and only if there is no users for the organization (this is used for creating the first administrative user for an organization).

In this example we will focus on ROLE_USER and ROLE_ORG_ADMIN. Let us assume that an Organization (DMA) wants to grant members of the internal "E-navigation" department administrative rights in the MCP Identity Registry. In DMAs Identity Provider setup the department name is automatically added to the "permissions" attribute. So to make this mapping the current DMA administrator sets up a role mapping between the permission "E-navigation" and the role ROLE_ORG_ADMIN. Once this is done, all members of the DMA E-navigation department will have administrative rights for the DMA organization inside the Identity Registry. As noted earlier, these rights only apply inside the Identity Registry. Other services must create a similar setup with mapping of roles and permissions.

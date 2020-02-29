MCP Terminology
===============

  * Maritime Connectivity Platform (from D3.7 Technical Specification)
    ◦ “A communication framework enabling efficient, secure, reliable and seamless electronic information exchange among all authorized maritime stakeholders across available communication systems”, based on the IMO e-navigation strategy
• Maritime Identity Registry (MIR), or the Identity Registry (from D3.7 Technical Specification)
    ◦ The Identity Registry has the objective to enable an authentication of all maritime stakeholders in the context of the Maritime Connectivity Platform and thus increasing the security and reliability of communication. This goal is archived by providing a trustworthy infrastructure for identity authentication of maritime entities like human actors, services and devices.
• Maritime Service Registry (MSR), or the Service Registry (from D3.7 Technical Specification)
    ◦ The Service Registry is one of the Maritime Connectivity Platform core components (MC³) and is supposed to serve as a central reference point to provide and find services and thus to improve the visibility and accessibility of available information and services in the maritime domain. It’s best compared with a yellow pages phone book.
• Maritime Messaging Service (MMS) (from D3.7 Technical Specification)
    ◦ a shore-based messaging service for the provision of flexible communication between ship and shore by using multiple available communication links and for delivering geo-location based messages (geocasting)
• Almanac
    ◦ The Almanac is an offline version of parts of the Service and Identity Registry, to be used if no stable internet connection is available for lookup in the online versions of SR and IR and thus to always allow access to the most relevant information during a journey.
• Maritime Connectivity Platform Demonstrator Component (MCDC) (from D3.7 Technical Specification)
    ◦ The Maritime Connectivity Platform Demonstrator Component serves as a reference implementation on how to use the other Maritime Connectivity Platform core components and can further be used by application developer (for example provider of ship equipment) to ease the usage of MCP functionality. For this purpose, the MCDC realizes some convenience functions, and takes the Network Roaming Device into account to ensure a maximum of connectivity.
• MCP instance provider (from MCP instance providers document)
    ◦ An MCP instance provider is an organization which runs an MCP instance which 1) operates of at least two (staging and production) MCP environments and the production one satisfying the operational requirements, 2) consists of MCP components complying with a specific subset of CWE (Appendix 1) at the source code level, 3) can be fixed by skilled engineer within the downtime criteria, 4) passed the MCC test cases, 5) maintains identities through the MCC procedure for identity management, 6) describes the configuration of instance, environment, component as a profile format, 7) and is validated by MCC.
• Key actor (from MCP Identity Platform document https://developers.maritimeconnectivity.net/identity/index.html)
    ◦ Maritime entities which needs to be authenticate for access right, is not both public and security related, and interact with the identity registry.
• Organization (from D3.7 Technical Specification)
    ◦ In the Maritime Connectivity Platform an organization is an entity, such as an institution, company or an association that has a collective goal and is linked to an external environment. Examples, include international organizations such as IMO, IALA, and IHO. National authorities such as US Coastguard, Swedish Maritime Administration. Local authorities such as VTS-Oeresund, Port of Rotterdam, Hong Kong SAR. Or commercial companies such as Transas or Maris.
• User (from D3.7 Technical Specification)
    ◦ Users mainly refers to human users. Human users differ from other actors in that they typically use a username/password to login which implies a different interaction pattern with the identity registry then say communication between vessels.
• Device (from D3.7 Technical Specification)
    ◦ Devices can be any number of entities that is not covered by the other entity types. It could for example be a lighthouse, an ECDIS or a server that needs to be able to authenticate itself. For example an ECDIS system.
• Service (from D3.7 Technical Specification)
    ◦ Services refers to digital services, as described above. For example, a weather service that is available to other services for machine to machine communication. Services needs to be registered in such a way that it can successfully authenticate users.
• Vessel (from D3.7 Technical Specification)
    ◦ Vessels describes any floating object used for the carriage of people or goods. The main need for registering vessels in the Maritime Connectivity Platform is so that digital authentication certificates can be issued for them. Thereby enabling secure communication between vessels as well as digitally signing of documents. Users might also use these authentication certificates for other purposes. The important thing is that the functionality is there. As part of the authentication certificate of a vessel its name, MMSI number, IMO number, call sign and possible other attributes is included in the header of the authentication certificate.
• Maritime Resource Name (from IALA webpage https://www.iala-aism.org/technical/data-modelling/mrn/)
    ◦ Maritime Resource Name (MRN) is a naming scheme that can uniquely identify any maritime resource on a global scale. By maritime resource, it means anything that has an identity of some kind. This could be organizations, employees, a person, a physical or a virtual object, for instance an electronic document, a buoy, a ship, a mariner, a nautical chart or an electronic service (e.g., “today’s weather report for the Oresund Strait”). Not all resources are “retrievable” in an electronic sense; For example, human beings, corporations, and buoys. However, they can still be considered a resource.
• Authentication (from white paper of Identity Management and Cyber Security)
    ◦ The process of verifying the identity claimed by an entity based on its credentials.
• Authorization (from white paper of Identity Management and Cyber Security)
    ◦ The process of establishing a specific entitlement that is consistent with authorization policies.
• Authorization policies (from white paper of Identity Management and Cyber Security)
    ◦ Declarations that define entitlements of a security principal and any constraints related to that entitlement.
• Entitlements (from white paper of Identity Management and Cyber Security)
    ◦ The actions an entity in a network is allowed to perform and the resources to which it is allowed access.
• Federated identity (from white paper of Identity Management and Cyber Security)
    ◦ Is the means of linking a person's electronic identity and attributes, stored across multiple distinct identity management systems
• Identity (from white paper of Identity Management and Cyber Security)
    ◦ The set of attributes that uniquely identifies a security principal. A security principal can have many different accounts that it uses to access various applications in the network. These accounts can be identified by these applications using different attributes of this entity. For example, a user can be known in the e-mail service by an e-mail ID, whereas that same user can be known in the human resource application by an employee number. The global set of such attributes constitutes the identity of the entity.
• Identity administration (from white paper of Identity Management and Cyber Security)
    ◦ The act of managing information associated with the identity of a security principal. The information can be used by the identity management infrastructure itself to determine administrative privileges.
• Identity management policies (from white paper of Identity Management and Cyber Security)
    ◦ Policies affecting the management of identities which includes naming policies and security policies.
• Realm (from white paper of Identity Management and Cyber Security)
    ◦ A collection of identities and associated policies which is typically used when enterprises want to isolate user populations and enforce different identity management policies for each population.
• Security principals (from white paper of Identity Management and Cyber Security)
    ◦ The subjects of authorization policies, such as users, user groups, and roles. A security principal can be a human or any application entity with an identity in the network and credentials to assert the identity.
• Identity provider (from Wikipedia)
    ◦ An identity provider (abbreviated IdP or IDP) is a system entity that creates, maintains, and manages identity information for principals while providing authentication services to relying applications within a federation or distributed network. Identity providers offer user authentication as a service. Relying party applications, such as web applications, outsource the user authentication step to a trusted identity provider. Such a relying party application is said to be federated, that is, it consumes federated identity.
• Identity broker (from Red Hat: https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.0/html/server_administration_guide/identity_broker )
    ◦ An Identity Broker is a special type of the identity provider and an intermediary service that connects multiple service providers with different identity providers. As an intermediary service, the identity broker is responsible for creating a trust relationship with an external identity provider in order to use its identities to access internal services exposed by service providers.
• PKI, Public Key Infrastructure (from Wikipedia https://en.wikipedia.org/wiki/Public_key_infrastructure)
    ◦ A public key infrastructure (PKI) is a set of roles, policies, hardware, software and procedures needed to create, manage, distribute, use, store and revoke digital certificates and manage public-key encryption. The purpose of a PKI is to facilitate the secure electronic transfer of information for a range of network activities such as e-commerce, internet banking and confidential email. It is required for activities where simple passwords are an inadequate authentication method and more rigorous proof is required to confirm the identity of the parties involved in the communication and to validate the information being transferred.
• OIDC, Open ID Connect (from Wikipedia https://en.wikipedia.org/wiki/OpenID_Connect)
    ◦ OpenID Connect is a simple identity layer on top of the OAuth 2.0 protocol, which allows computing clients to verify the identity of an end-user based on the authentication performed by an authorization server, as well as to obtain basic profile information about the end-user in an interoperable and REST-like manner. In technical terms, OpenID Connect specifies a RESTful HTTP API, using JSON as a data format.
• MCP instance profile
    ◦ Description of HW/SW configuration of an MCP instance, e.g., one the possible constellations like ‘Running MIR (PKI+OIDC) + MSR + MMS’
• MCP environment profile
    ◦ Description of HW/SW configuration of an MCP environment
• MIR profile
    ◦ Description of HW/SW configuration of an MIR component
• MSR profile
    ◦ Description of HW/SW configuration of an MSR component
• MMS profile
    ◦ Description of HW/SW configuration of an MMS component

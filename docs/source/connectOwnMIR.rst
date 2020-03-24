Running Your Own MIR
====================
If your organizations wishes to register your MIR as an MCP Identity Provider, to enable your uses to authenticate in MCP, please contact Oliver Haagh at oliver@dmc.international in order to set it up. Note that currently you need to expose interfaces that supports either OpenID Connect or SAML2.

Within the scope of the EfficienSea2, STM validation, and SMART navigation projects, organizations can get users registered in a special kind of Identity Providers, supplied by MCP. To join MCP please fill out the form at Apply.

Setting up an OpenID Connect Identity Provider
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
OpenID Connect is supported by the latest ADFS and Keycloak releases. MCP Identity Broker only supports the OpenID Connect Authorization Code Flow when connecting to Identity Providers. This limitation only applies when the Identity Broker connects to Identity Providers, not when Services/Clients connects to the Identity Broker.

As default MCP Identity Broker expect the following attributes to be provided by an OpenID Connect Identity Provider:


If your Identity Provider has the values in different attributes, some mapping can be set up.

The Identity Broker will generate and attach the organizations MRN and the users MRN to the user.

Setting up an OpenID Connect Identity Provider for multiple organizations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
MCP has some special Identity Providers that handles the authentication for multiple organizations. Current examples are "IALA" and "BIMCO ExtraNet". These Identity Providers are responsible for vetting the organizations they provide authentication for, so that it is confirmed that the organization is who they claim to be. New organizations can be added by these Identity Providers. Since MCP currently needs to know about organizations centrally to be able to (among other things) issue certificates, some extra information is needed from these Identity Providers, to be able to create them in the central Identity Registry, if they are not already known.

The extra information must be given as attributes, in addition to the attributes mentioned in Setting up an OpenID Connect Identity Provider:

As default MCP Identity Broker expect the following attributes to be provided by an OpenID Connect Identity Provider:

Note that the MRN must be on the form "urn:mrn:mcl:user:dma@iala:thc" and "urn:mrn:mcl:org:dma@iala" for user and organization respectively. In this case the organization is "dma" whos identity is guaranteed by "iala".

Setting up an SAML2 Identity Provider
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
SAML2 is supported by older ADFS releases.

If your Identity Provider has the values in different attributes, some mapping can be set up.

The Identity Broker will generate and attach the organizations MRN and the users MRN to the user.

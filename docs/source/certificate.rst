Certificate
===============
MCP can issue X.509 certificates for the users which can then be used for authentication. Service providers relying on X.509 certificate authentication must obtain and install MCP root certificate into their webservice.

The standard information present in an X.509 certificate includes:

* Version – which X.509 version applies to the certificate (which indicates what data the certificate must include)

* Serial number – A unique assigned serial number that distinguishes it from other certificates

* Algorithm information – the algorithm used to sign the certificate

* Issuer distinguished name – the name of the entity issuing the certificate (MCP)

* Validity period of the certificate – start/end date and time

* Subject distinguished name – the name of the identity the certificate is issued to

* Subject public key information – the public key associated with the identity

The Subject distinguished name field will consists of the following items:

An example of the fields for a vessel could look like this:

C=DK, O=urn:mrn:mcl:org:dma, OU=vessel, CN=JENS SØRENSEN, UID=urn:mrn:mcl:vessel:dma:jens-soerensen

Finally, In additions to the information stored in the standard X.509 attributes listed above, the X509v3 extension SubjectAlternativeName (SAN) extension is used to store extra information. There already exists some predefined fields for the SAN extension, but they do not match the need we have for maritime related fields. Therefore the “otherName” field is used, which allows for using a Object Identifier (OID) to define custom fields. The OIDs currently used are not registered at ITU, but are randomly generated using a tool provided by ITU (see http://www.itu.int/en/ITU-T/asn1/Pages/UUID/uuids.aspx). See the table below for the fields defined, the OIDs of the fields and which kind of entities that uses the fields.

Revocation
^^^^^^^^^^
A crucial part of any PKI is to support revocation of certificates, so that certificates that belongs to entities who is no longer trusted, affiliation has change, etc., can be mark as not trusted any more. Anyone who wishes to validate a certificate can then check if the certificate has been marked as revoked. The checking of the certificate revocation status can be done in two ways:

* Call the OCSP interface provided by the Identity Registry for each certificate.

* Periodically download a Certificate Revocation File from the Identity Registry and use it check certificates locally.

The endpoints for both the OCSP interface and the Certificate Revocation File are embedded into the certificates issued by MCP Identity Registry, and are currently https://api.maritimecloud.net/x509/api/certificates/crl and https://api.maritimecloud.net/x509/api/certificates/ocsp.

Authentication Flow
^^^^^^^^^^^^^^^^^^^
To illustrate the authentication flow the sequence diagram below is provided.

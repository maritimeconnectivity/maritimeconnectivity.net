MCP Certificate
==========================
MCP can issue X.509 certificates for the users which can then be used for authentication. Service providers relying on X.509 certificate authentication must obtain and install MCP root certificate into their webservice.

The standard information present in an X.509 certificate includes:

* **Version** – which X.509 version applies to the certificate (which indicates what data the certificate must include)

* **Serial number** – A unique assigned serial number that distinguishes it from other certificates

* **Algorithm information** – the algorithm used to sign the certificate

* **Issuer distinguished name** – the name of the entity issuing the certificate (MCP)

* **Validity period of the certificate** – the number of months that the certificate is valid

* **Subject distinguished name** – the name of the identity the certificate is issued to

* **Subject public key information** – the public key associated with the identity

The Subject distinguished name field will consists of the following items:

+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+
| Field                  | User     | Vessel    | Device    | Service           | MMS    | Organization       |
+========================+==========+===========+===========+===================+========+====================+
|CN (CommonName)         |Full name |Vessel name|Device name|Service Domain Name|MMS name|Organization Name   |
+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+
|O (Organization)        |                            Organization MCP MRN                                    |
+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+
|OU (Organizational Unit)|"user"    |"vessel"   |"device"   |"service"          |"mms"   |"organization"      |
+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+
|E (Email)               |User email|                                                    |Organization email  |
+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+
|C (Country)             |                             Organization country code                              |
+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+
|UID                     |                          Entity MCP MRN                       |Organization MCP MRN|
+------------------------+----------+-----------+-----------+-------------------+--------+--------------------+

An example of the fields for a vessel could look like this::

  C=DK, O=urn:mrn:mcp:org:idp1:dma, OU=vessel, CN=JENS SØRENSEN, UID=urn:mrn:mcp:vessel:idp1:dma:jens-soerensen

Finally, In additions to the information stored in the standard X.509 attributes listed above, the X509v3 extension SubjectAlternativeName (SAN) extension is used to store extra information. There already exists some predefined fields for the SAN extension, but they do not match the need we have for maritime related fields. Therefore the “otherName” field is used, which allows for using a Object Identifier (OID) to define custom fields. The OIDs currently used are not registered at ITU, but are randomly generated using a tool provided by ITU (see http://www.itu.int/en/ITU-T/asn1/Pages/UUID/uuids.aspx). See the table below for the fields defined, the OIDs of the fields and which kind of entities that uses the fields.

+-----------------+------------------------------------------------+---------------------------------------+
| Field           | Object Identifier (OID)                        | Related entity types                  |
+=================+================================================+=======================================+
| AIS shiptype    |`2.25.107857171638679641902842130101018412315`  | Vessel, Service                       |
+-----------------+------------------------------------------------+---------------------------------------+
| Port of register|`2.25.285632790821948647314354670918887798603`  | Vessel, Service                       |
+-----------------+------------------------------------------------+---------------------------------------+
| Ship MRN        |`2.25.268095117363717005222833833642941669792`  | Service                               |
+-----------------+------------------------------------------------+---------------------------------------+
| MRN             |`2.25.271477598449775373676560215839310464283`  | Vessel, User, Device, Service, MMS    |
+-----------------+------------------------------------------------+---------------------------------------+
| Permissions     |`2.25.174437629172304915481663724171734402331`  | Vessel, User, Device, Service, MMS    |
+-----------------+------------------------------------------------+---------------------------------------+
| Subsidiary MRN  |`2.25.133833610339604538603087183843785923701`  | Vessel, User, Device, Service, MMS    |
+-----------------+------------------------------------------------+---------------------------------------+
| Home MMS URL    |`2.25.171344478791913547554566856023141401757`  | Vessel, User, Device, Service, MMS    |
+-----------------+------------------------------------------------+---------------------------------------+
| URL             |`2.25.245076023612240385163414144226581328607`  | MMS                                   |
+-----------------+------------------------------------------------+---------------------------------------+

Encoding of string values in certificates must follow the specifications defined in RFC 5280, and where possible it is highly recommended to use UTF-8.

Revocation
^^^^^^^^^^
A crucial part of any PKI is to support revocation of certificates, so that certificates that belongs to entities who is no longer trusted, affiliation has change, etc., can be mark as not trusted any more. Anyone who wishes to validate a certificate can then check if the certificate has been marked as revoked. The checking of the certificate revocation status can be done in two ways:

1. Call the OCSP interface provided by the Identity Registry for each certificate.
2. Periodically download a Certificate Revocation File from the Identity Registry and use it check certificates locally.

The endpoints for both the OCSP interface and the Certificate Revocation File are embedded into the certificates issued by MCP Identity Registry, and are currently https://api.maritimecloud.net/x509/api/certificates/crl and https://api.maritimecloud.net/x509/api/certificates/ocsp.

Setting up PKI
====================
A part of the MIR is based on public key certificates.
For this a custom PKI has been developed to issue and manage certificates for stakeholders.
To set up the PKI you must get the source code for it from
https://github.com/MaritimeConnectivityPlatform/MCP-PKI/archive/v0.10.0-hotfix1.zip
‘git clone https://github.com/MaritimeConnectivityPlatform/MCP-PKI.git’.
Alternatively you can also get the needed executable from
https://github.com/MaritimeConnectivityPlatform/MCP-PKI/releases/download/v0.10.0-hotfix1/mc-pki-0.10.0-jar-with-dependencies.jar.
After you have done this you can build the project from the directory storing the code using the following command:

mvn clean install

After this has finished there should now be a new folder called target.
This folder contains the resulting artifacts of the build process, including the jar file mc-pki-0.10.0-SNAPSHOT-jar-with- dependencies.jar which is the artifact that is going to be used to generate the root certificate authority (CA) and sub-CAs for the PKI.

The next step is to generate the root CA. This can be done using the following command where you should of course replace the different fields with information relevant to your setup. For example here urn:mrn:mcp:ca:maritimeconnectivity will be the MRN for the root CA, where you might want it to be called something else in your setup::

  java -jar mc-pki-0.10.0-SNAPSHOT-jar-with-dependencies.jar \
  --init \
  --root-ca-alias urn:mrn:mcp:ca:maritimeconnectivity \ --truststore-path mcp-truststore.jks \ --truststore-password changeit \
  --root-keystore-path root-ca-keystore.jks \ --root-keystore-password changeit \ --root-key-password changeit \
  --x500-name "C=DK, ST=Denmark, L=Copenhagen, O=MCP Test, OU=MCP Test, CN=MCP Test Root Certificate, E=info@maritimeconnectivity.net" \
  --crl-endpoint "https://api.example.com/x509/api/certificates/crl/urn:mrn:mcp:ca:maritimeconnectivity"

You should now have two different keystore files called mcp-truststore.jks, which contains the root CA certificate, and root-ca-keystore.jks, which contains. The password for both of these is ‘changeit’, but can be set to something else by changing the values of truststore-password and root- keystore-password.
Now you will need to create a certificate revocation list (CRL) for the root CA. This can be done using the following command::

  java -jar mc-pki-0.10.0-SNAPSHOT-jar-with-dependencies.jar \
  --generate-root-crl \
  --root-ca-alias urn:mrn:mcp:ca:maritimeconnectivity \ --root-keystore-path root-ca-keystore.jks \ --root-keystore-password changeit \
  --root-key-password changeit \ --revoked-subca-file revoked-subca.csv \ --root-crl-path root-ca.crl

The file revoked-subca.csv should either be empty or contain the sub CAs that have been revoked separated by commas and should have a format like this
<serial-number>;<revocation-reason>;<revocation-date>
The resulting file root-ca.crl contains the list of sub CAs that have been revoked.

The next step is then to generate the sub CA(s) that is going to be used for issuing client certificates. The command below shows an example of how to do this::

  java -jar mc-pki-0.10.0-SNAPSHOT-jar-with-dependencies.jar \ --create-subca \
  --root-ca-alias urn:mrn:mcp:ca:maritimeconnectivity \ --root-keystore-path root-ca-keystore.jks \ --root-keystore-password changeit \ --root-key-password changeit \
  --truststore-path mc-truststore.jks \
  --truststore-password changeit \
  --subca-keystore subca-keystore.jks \
  --subca-keystore-password changeit \
  --subca-key-password changeit \
  --x500-name "UID=urn:mrn:mcp:ca:mcp-idreg, C=DK, ST=Denmark, L=Copenhagen, O=MCP Test, OU=MCP Test, CN=MCP Test Identity Registry, E=info@maritimeconnectivity.net" \
  --crl-endpoint "https://api.example.com/x509/api/certificates/crl/urn:mrn:mcp:ca:mcp-idreg"

This creates a sub CA that contains the information given in x500-name and signed by the root CA. The sub CA certificate is added to mc-truststore.jks and the keys of the sub CA are stored in subca-
keystore.jks. Note that in crl-endpoint you should change ‘api.example.com’ to whatever domain you are using and the MRN after ‘crl’ should be changed to whatever you wrote in ‘UID’.
All the files generated in this section should be stored for later usage.

Setting up NGINX
====================
Setting up NGINX is not required, but it is highly recommended to use it as a reverse proxy because it makes handling of TLS and client certificate authentication a lot easier.
In the supplied file nginx.conf is an example of how NGINX can be used to proxy incoming requests to the Identity Registry API and Keycloak assuming that they are running on the same machine.
There are some requirements that need to be met to use the configuration.
The first one is that you need to have a domain registered with the sub-domains api, api-x509, maritimeid, maritimeid-x509. These can of course be changed to something else in the configuration is necessary.
The second requirement is that you need to have a TLS certificate for your domain. The path to the certificate should then be defined in the variable ssl_certificate and then the path to the corresponding private key should be defined in the variable ssl_certificate_key.
The third requirement is that the variable ssl_crl should point to an up-to-date file that contains the CRLs of the root CA and the sub CAs concatenated together. How to set this up will be described later in this document.
The fourth requirement is that the variable ssl_client_certificate must point to a file that contains the certificates of the root CA and the sub CAs in PEM format. These can be extracted from the mc- truststore.jks generated in the previous step using a tool like KeyStore Explorer.
NGINX can either be installed and run directly on the machine or in a Docker container. Note that if you choose to run it in a Docker container it is recommended to run it with the option --net=host so it binds directly to the network interface of the host instead of using the default bridge driver.

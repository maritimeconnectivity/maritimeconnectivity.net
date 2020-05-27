Setting up Keycloak
====================
Setting up Keycloak can be done using either a standalone installation of Keycloak or using the prebuilt Docker container.
Using the Docker container is recommended, but if a standalone installation is required a guide on how to use this can be found at https://github.com/ MaritimeConnectivityPlatform/MCPKeycloakSpi.

Using a Docker container
^^^^^^^^^^^^^^^^^^^^^^^^
A prebuilt Docker container for Keycloak with MCP specific functionality can be found at https://cloud.docker.com/u/dmadk/repository/docker/dmadk/keycloak-mysql-mc-ha. At the time of writing the latest tag for this is 0.10.0. The latest tag is built from the latest code from the main git branch and is therefore not guaranteed to be stable.
For creating the Docker container using the 0.10.0 tag you can use the following command:
docker create --name=mir-keycloak --restart=unless-stopped -p 8080:8080 \ -v <directory for configurations>:/mc-eventprovider-conf \
-e MC_IDREG_SERVER_ROOT=https://api-x509.example.com \
-e JGROUPS_DISCOVERY_EXTERNAL_IP=<valid IP address> dmadk/keycloak-mysql-mc-ha:0.10.0
The directory that is mounted to ‘/mc-eventprovider-conf’ in the container must contain the following files:
• mc-truststore.jks
• idbroker-updater.jks
The first one is the one that was generated earlier. The second one is only needed if user federation
is used and will be described later on how to generate.
The URL given as value for the variable MC_IDREG_SERVER_ROOT must be set to the same value as the one set in the NGINX configuration.
If running Keycloak in clustered mode the value of JGROUPS_DISCOVERY_EXTERNAL_IP must be set to an IP address that Keycloak is reachable on. If it is not to be run in clustered mode it can just be set to 127.0.0.1 or another random IP.
As default the database and the user that is to be used for it are set to be keycloak and the password for the database user is set to be password. If you want to use other values than these you can set them as variables in the above command as described at https://hub.docker.com/r/jboss/keycloak.
To start Keycloak you can then use the command
docker start mir-keycloak

Setting up Realms in Keycloak
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
When you have gotten Keycloak up and running you will need to setup the needed Realms. To login to the admin interface of Keycloak go to http://localhost:8080 if you have Keycloak running on localhost or else use the domain set in your NGINX configuration. The first time you login you will need to setup an admin user and password.
After that you will need to import the three *-realm.json files from https://github.com/MaritimeConnectivityPlatform/IdentityRegistry/tree/master/setup.
This can be done in the admin interface of Keycloak by hovering the mouse over the dropdown ‘Select realm’ and then click ‘Add realm’. Here you can then import the *-realm.json files one by one.
Note that the URLs to OIDC clients, identity providers, etc. are set to localhost in the *-realm.json files so these will need to be updated to the correct URLs after the files have been imported.

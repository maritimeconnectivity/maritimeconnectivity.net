.. _mcp-instance-usage:

Using MCP instance
==================
There is two contexts of the usage of MCP instances, MCC MCP testbed and MCP Instance Provider's instance.
Primary purpose of MCC MCP testbed is assessing new release of reference implementation and its impact to existing services.
It is strongly recommended to use MCP Instance Provider's instance if the reader considers to consume or provide MCP services in operational purpose.
Enrolment of the MCC MCP testbed as an organization is free and open while that of MCP Instance Provider's instance depends on the enrolment policy set by each MCP Instance Provider.

.. _mcp-instance-usage-testbed:

Using MCC MCP testbed
---------------------
In order to get an organization in our testbed, its users and any ships the organization might own on to the MCP testbed, the organization needs to perform a signup process.
The process is currently manual. To start the process, please fill out the `registration form <https://management.maritimecloud.net/#/apply>`__.

Once your organization has been approved you will have access to MCP and its services.
You should probably start by looking at the `Management Portal <https://management.maritimecloud.net/>`__.

Issuing a Certificate from MCP Testbed Root Certificate
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
In order to use the certificates issued by the MCP Identity Registry it is needed to add MCP Root Certificates to the relevant trustchain. Here you can download the root certificates for MCP instances:

MCP Production environment root certificates as PEM (one file, primarily for Apache/Nginx), in JKS (for Java) or a zip with the separate files (for windows).
MCP Staging environment root certificates as PEM (one file, primarily for Apache/Nginx), in JKS (for Java) or a zip with the separate files (for windows).
MCP Test environment root certificates as PEM (one file, primarily for Apache/Nginx), in JKS (for Java) or a zip with the separate files (for windows).

Using MCP Instance Provider
---------------------------
To be written.....

* use of identity management or certificate case
* use of service consumer case
* use of service provider case

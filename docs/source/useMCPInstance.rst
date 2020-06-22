.. _mcp-instance-usage:

Using MCP instance
==================
There is two contexts of the usage of MCP instances, MCC MCP testbed and MCP Instance Provider's instance.
Primary purpose of MCC MCP testbed is assessing new release of reference implementation and its impact to existing services.
It is strongly recommended to use MCP Instance Provider's instance if the reader considers to consume or provide MCP services in operational purpose.
Enrollment of the MCC MCP testbed as an organization is free and open while that of MCP Instance Provider's instance depends on the enrollment policy set by each MCP Instance Provider.

.. _mcp-instance-usage-testbed:

Using MCC MCP testbed
---------------------
MCC (or rather partners of the MCC on behalf of the MCC) will operate 3 environments of the MCP.

* Test environment which will be used for testing new versions of the MCP reference software as developed by the MCC (or rather partners of the MCC on behalf of the MCC).
* Staging environment which will be used for testing new release candidates of the MCP reference software.
* Public test environment for use by anyone for general tests/assessment of the MCP and services. This is mainly for promotional purposes.

Only MMC members will be granted access to the test and staging environments, and these will only be used for the purposes designated for them.
The pubic test environment will be, as the name indicates, made available to all (relevant) external stakeholders. Users of the public test environment will go through a very simple validation process.

1. New users apply for access through the management portal of the public test environment by filling out the `registration form <https://management.maritimecloud.net/#/apply>`__.
2. Their organisations will be assessed though their website
3. The users will be validated through email correspondence where they are requested to use an email address belonging to the official internet domain
4. Access to the environments are handled by the MCC secretariat, which may deviate from the above procedure if they deem appropriate

Once your organization has been approved you will have access to services in the public test environment.
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

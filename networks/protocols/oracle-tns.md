# Oracle TNS

The **Oracle Transparent Network Substrate** is a proprietary networking protocol used by Oracle Database to facilitate communication between clients and database servers. It operates at the Application Layer and typically uses TCP port 1521 by default.

TNS is responsible for establishing and managing database connections in an Oracle environment. Its main features are:

* Client-to-database communication over a network
* Session multiplexing and load balancing
* Secure authentication and encryption
* High Availability using failover and clustering

In short, the client-side Oracle Net Services software uses the _tnsnames.ora_ file to resolve service names to network addresses, while the listener process uses the _listener.ora_ file to determine the services it should listen to and the listener's behavior.

A _tnsnames.ora_ file looks similar to this:

{% code overflow="wrap" lineNumbers="true" %}
```bash
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = $IP)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```
{% endcode %}

And a _listener.ora_ file looks similar to this:

{% code overflow="wrap" lineNumbers="true" %}
```bash
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PDB1)
      (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
      (GLOBAL_DBNAME = PDB1)
      (SID_DIRECTORY_LIST =
        (SID_DIRECTORY =
          (DIRECTORY_TYPE = TNS_ADMIN)
          (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
        )
      )
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = $oracleDomain)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ADR_BASE_LISTENER = C:\oracle
```
{% endcode %}

We can interact with this protocol and its related services using the [_Odat_](../tools-and-utilities.md#odat) _tool_

Table 2.3. Configuration File Locations
```
Server mode	Location	Purpose
1) domain.xml	
EAP_HOME/domain/configuration/domain.xml	
This is the main configuration file for a managed domain. 
Only the domain master reads this file. On other domain members, it can be removed.

2) host.xml	
EAP_HOME/domain/configuration/host.xml	
This file includes configuration details 
specific to a physical host in a managed domain, such as network interfaces, socket bindings, 
the name of the host, and other host-specific details. The host.xml file includes all of the 
features of both host-master.xml and host-slave.xml, which are described below. This file is 
not present for standalone servers.

3)host-master.xml	
EAP_HOME/domain/configuration/host-master.xml	
This file includes only the configuration details necessary to run a server as a managed domain 
master server. This file is not present for standalone servers.

4) host-slave.xml	
EAP_HOME/domain/configuration/host-slave.xml	
This file includes only the configuration details necessary to run a server as a managed domain 
slave server. This file is not present for standalone servers.

5) standalone.xml	
EAP_HOME/standalone/configuration/standalone.xml	
This is the default configuration file for a standalone server. It contains all information about 
the standalone server, including subsystems, networking, deployments, socket bindings, and other 
configurable details. This configuration is used automatically when you start your standalone server.

6) standalone-full.xml	
EAP_HOME/standalone/configuration/standalone-full.xml	
This is an example configuration for a standalone server. It includes support for every possible 
subsystem except for those required for high availability. To use it, stop your server and restart 
using the following command: EAP_HOME/bin/standalone.sh -c standalone-full.xml

7)standalone-ha.xml	
EAP_HOME/standalone/configuration/standalone-ha.xml	
This example configuration file enables all of the default subsystems and adds the mod_cluster 
and JGroups subsystems for a standalone server, so that it can participate in a high-availability 
or load-balancing cluster. This file is not applicable for a managed domain. To use this configuration,
stop your server and restart using the following command: EAP_HOME/bin/standalone.sh -c standalone-ha.xml

8) standalone-full-ha.xml	
EAP_HOME/standalone/configuration/standalone-full-ha.xml	
This is an example configuration for a standalone server. It includes support for every possible 
subsystem, including those required for high availability. To use it, stop your server and restart 
using the following command: EAP_HOME/bin/standalone.sh -c standalone-full-ha.xml

```
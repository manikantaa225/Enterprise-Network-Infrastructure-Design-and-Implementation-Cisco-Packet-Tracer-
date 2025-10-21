# Enterprise-Network-Infrastructure-Design-and-Implementation-Cisco-Packet-Tracer-
A complete enterprise network design and implementation using Cisco Packet Tracer. Features include VLANs, OSPF routing, DHCP, PAT, SSH, and port security for a 3-floor, 600-user organization. Ensures scalability, redundancy, and secure communication across all departments.

## Overview    </br>
This project presents the design and implementation of a secure and redundant enterprise network using Cisco Packet Tracer for a trading floor support center with 600 staff members distributed across three floors.
The network follows a hierarchical topology with two routers, two multilayer switches, and multiple access switches, ensuring scalability, redundancy, and efficient traffic management. Each department operates in its own VLAN and subnet derived from the 172.16.1.0/24 base network.
Key configurations include OSPF routing, DHCP services, PAT for Internet access, SSH for secure remote management, and port security for device protection.
The network also integrates wireless access points for mobility and redundant ISP connections for high availability.
Overall, the project demonstrates a realistic enterprise-level infrastructure that delivers reliability, security, and full connectivity across all departments.

##  Network Topology   </br>

The enterprise network is built on a three-tier hierarchical topology to ensure scalability, redundancy, and efficient communication across all departments and floors.   </br>

Core Layer: Two routers connected to dual ISPs provide Internet redundancy and dynamic routing using OSPF.    </br>
Distribution Layer: Two Layer 3 switches perform inter-VLAN routing and connect to both routers and access switches for fault tolerance.   </br>
Access Layer: Departmental access switches connect wired and wireless devices, with VLANs separating network traffic for security and management.    </br>
Each department has a dedicated VLAN and subnet derived from the 172.16.1.0/24 base network.
DHCP provides dynamic IP allocation, while servers use static IPs.
The topology also integrates wireless access points, PAT for Internet access, and port security for device control.
Overall, the topology ensures secure, redundant, and reliable connectivity throughout the organization’s three-floor structure.

<img width="912" height="550" alt="Image" src="https://github.com/user-attachments/assets/0597a978-c6cb-4e55-874a-bf91675bb664" />

## FLOOR-1

Floor 1 – Sales & Human Resources  </br>
</br>
Departments:    </br>
Sales & Marketing        </br>
HR & Logistics      </br>
VLAN Configuration:              </br>
VLAN 10: Sales & Marketing – 172.16.1.0/25      </br>
VLAN 20: HR & Logistics – 172.16.1.128/25    </br>
Devices:   </br>
PCs, Laptops, Printers, and Smartphones connected through Access Switches.      </br>
Each department has its own subnet for traffic isolation and better bandwidth utilization      </br>
Connectivity:           </br>
Both VLANs are connected to Layer 3 Switch 0 (MLS0) for inter-VLAN routing.       </br>
Traffic is routed to the distribution layer and then to edge routers for internet access     </br>
Purpose:              </br>
Sales focuses on client communication and database access.       </br>
HR manages employee records and internal systems with secured access.         </br>
</br>

<img width="513" height="636" alt="Image" src="https://github.com/user-attachments/assets/09e55483-3250-4f0f-8f42-66cc674a8d97" />

## FLOOR-2    </br>
</br>
Floor 2 – Finance & Administration    </br>
Departments:       </br>
Finance & Accounts       </br>
Administration & Public Relations     </br>
VLAN Configuration:                 </br>
VLAN 30: Finance & Accounts – 172.16.2.0/25     </br>
VLAN 40: Admin & PR – 172.16.2.128/25      </br>
Devices:    </br>
Desktop PCs, Laptops, Network Printers, and Wi-Fi access points.    </br>
Connectivity:         </br>
Connected via Layer 3 Switch 1 (MLS1) with OSPF routing to ensure fast and reliable inter-floor communication.      </br>
Redundant links provide high availability and load balancing between floors           </br>
Purpose:              </br>
Finance handles secure transactions and data access.                      </br>
Administration and PR manage organizational coordination and communication.        </br>
 </br>
 <img width="575" height="631" alt="Image" src="https://github.com/user-attachments/assets/04d8ae44-4dad-418c-8e9f-4718e9b7d09d" />

 ## FLOOR-3   </br>
 </br>
Floor 3 – ICT Department & Server Room
 </br>
Departments:     </br>
IT Support       </br>
Server Operations        </br>
VLAN Configuration:       </br>
VLAN 50: IT Department – 172.16.3.0/25     </br>
VLAN 60: Server Room – 172.16.3.128/28      </br>
Devices:      </br>
Includes DHCP, DNS, Web, and File Servers.       </br>
IT department has management PCs, laptops, and monitoring systems.     </br>
Connectivity:     </br>
Redundant connections to both Layer 3 Switches (MLS0 & MLS1) for fault tolerance.      </br>
The server VLAN provides centralized services to all other floors.       </br>
Purpose:
IT department maintains the network, performs troubleshooting, and manages user access.     </br>
Server Room ensures centralized resource sharing, data backup, and service reliability.     </br>

<img width="461" height="583" alt="Image" src="https://github.com/user-attachments/assets/42dc0820-ffbc-4721-b37d-20769504d59b" />

## Configuration   </br>
## Console & Privileged  Configuration
 </br>
 configure in all switches & routers except in ISP routers   </br>
  </br>
Switch> enable      </br>
Switch# configure terminal       </br>
Switch(config)# enable secret cisco123     </br>
Switch(config)# line console 0        </br>
Switch(config-line)# password cisco@123      </br>
Switch(config-line)# login      </br>
Switch(config-line)# exit        </br>
Switch(config)# no ip domain-lookup   </br>
Switch(config)# banner motd  # unauthorised prohibited #      </br>
 </br>
## Vlan & Trunk Configuration   </br>
</br>
Switch(config)# vlan 10     </br>
Switch(config-vlan)# name Sales    </br>
Switch(config)# interface range fa0/1 - 2       </br>
Switch(config-if-range)# switchport mode trunk     </br>
Switch(config-if-range)# exit         </br>
Switch(config)# interface range fa0/3 - 24    </br>
Switch(config-if-range)# switchport mode access      </br>
Switch(config-if-range)# switchport access vlan 10   </br>
</br> 
Switch(config)# vlan 20     </br>
Switch(config-vlan)# name HR      </br>
Switch(config)# interface range fa0/1 - 2       </br>
Switch(config-if-range)# switchport mode trunk     </br>
Switch(config-if-range)# exit         </br>
Switch(config)# interface range fa0/3- 24    </br>
Switch(config-if-range)# switchport mode access      </br>
Switch(config-if-range)# switchport access vlan  20    </br>
Switch(config)# interface range fa0/4 - 24     </br>
Switch(config-if)# switchport port-security         </br>
Switch(config-if)# switchport port-security maximum 1      </br>
Switch(config-if)# switchport port-security mac-address sticky      </br>
Switch(config-if)# switchport port-security violation shutdown       </br>
</br>
Switch(config)# vlan 30      </br>
Switch(config-vlan)# name Finance      </br>
Switch(config)# interface range fa0/1 - 2       </br>
Switch(config-if-range)# switchport mode trunk     </br>
Switch(config-if-range)# exit         </br>
Switch(config)# interface range fa0/3 - 24    </br>
Switch(config-if-range)# switchport mode access      </br>
Switch(config-if-range)# switchport access vlan   30   </br>
</br>
Switch(config)# vlan 40        </br>
Switch(config-vlan)# name Admin      </br>
Switch(config)# interface range fa0/1 - 2       </br>
Switch(config-if-range)# switchport mode trunk     </br>
Switch(config-if-range)# exit         </br>
Switch(config)# interface range fa0/3 - 24    </br>
Switch(config-if-range)# switchport mode access      </br>
Switch(config-if-range)# switchport access vlan     </br>
</br>
Switch(config)# vlan 50          </br>
Switch(config-vlan)# name ICT        </br>
Switch(config)# interface range fa0/1 - 2       </br>
Switch(config-if-range)# switchport mode trunk     </br>
Switch(config-if-range)# exit         </br>
Switch(config)# interface range fa0/3 - 24    </br>
Switch(config-if-range)# switchport mode access      </br>
Switch(config-if-range)# switchport access vlan     </br>
</br>
Switch(config)# vlan 60          </br>
Switch(config-vlan)# name Server       </br>
Switch(config)# interface range fa0/1 - 2       </br>
Switch(config-if-range)# switchport mode trunk     </br>
Switch(config-if-range)# exit         </br>
Switch(config)# interface range fa0/3 - 24    </br>
Switch(config-if-range)# switchport mode access      </br>
Switch(config-if-range)# switchport access vlan     </br>
</br>

IN L3 Switches      </br>
  </br>
 
Switch(config)# interface vlan 10     </br>
Switch(config-if)# ip address 172.16.1.1 255.255.255.128      </br>
Switch(config-if)# ip helper-address 172.16.3.130        </br>
Switch(config)# interface vlan 20        </br>
Switch(config-if)# ip address 172.16.1.129 255.255.255.128      </br>
Switch(config-if)# ip helper-address 172.16.3.130          </br>
Switch(config)# interface vlan 30        </br>
Switch(config-if)# ip address 172.16.2.1 255.255.255.128      </br>
Switch(config-if)# ip helper-address 172.16.3.130           </br>
Switch(config)# interface vlan 40          </br>
Switch(config-if)# ip address 172.16.2.129 255.255.255.128      </br>
Switch(config-if)# ip helper-address 172.16.3.130         </br>
Switch(config)# interface vlan 50         </br>
Switch(config-if)# ip address 172.16.3.1 255.255.255.128       </br>
Switch(config-if)# ip helper-address 172.16.3.130           </br>
Switch(config)# interface vlan 60       </br>
Switch(config-if)# ip address 172.16.3.129 255.255.255.240     </br>
Switch(config-if)# ip helper-address 172.16.3.130          </br>
Switch(config-if)#exit   </br>
Switch(config)#ip-routing   </br> 

## DHCP pool configuration   </br>

<img width="1919" height="963" alt="Image" src="https://github.com/user-attachments/assets/6e771ef5-8dfa-405d-baa7-a42f2bc6ed1e" />

## OSPF configuration  </br>

In Multilayer Switch-1     </br>

Switch(config)# interface GigabitEthernet1/0/1      </br>
 Switch(config-if)#no switchport         </br>  
 Switch(config-if)#ip address 172.16.3.145 255.255.255.252        </br>
Switch(config)#interface GigabitEthernet1/0/2       </br>
 Switch(config-if)#no switchport        </br>
 Switch(config-if)#ip address 172.16.3.149 255.255.255.252      </br>
router ospf 10            </br>
 router-id 1.1.1.1          </br>
 network 172.16.1.0 0.0.0.127 area 0        </br>     
 network 172.16.1.128 0.0.0.127 area 0       </br>
 network 172.16.2.0 0.0.0.127 area 0          </br>
 network 172.16.2.128 0.0.0.127 area 0         </br>
 network 172.16.3.0 0.0.0.127 area 0         </br>
 network 172.16.3.128 0.0.0.15 area 0          </br>
 network 172.16.3.144 0.0.0.3 area 0      </br>  
 network 172.16.3.148 0.0.0.3 area 0          </br>
   </br>
ip route 0.0.0.0 0.0.0.0 GigabitEthernet1/0/1      </br>
ip route 0.0.0.0 0.0.0.0 GigabitEthernet1/0/2 70       </br>
   </br>
# Verification  </br>
<img width="1027" height="894" alt="Image" src="https://github.com/user-attachments/assets/9fdb9730-5663-4a83-ba0b-174c15b05fc9" />
</br>


 </br>  
In Multilayer Switch-2     </br>
  </br>
interface GigabitEthernet1/0/1         </br>
 no switchport        </br>
 ip address 172.16.3.153 255.255.255.252     </br>
interface GigabitEthernet1/0/2      </br>
 no switchport       </br>
 ip address 172.16.3.157 255.255.255.252      </br>
 router ospf 10            </br>
 router-id 2.2.2.2          </br>
 network 172.16.1.0 0.0.0.127 area 0        </br>     
 network 172.16.1.128 0.0.0.127 area 0       </br>
 network 172.16.2.0 0.0.0.127 area 0          </br>
 network 172.16.2.128 0.0.0.127 area 0         </br>
 network 172.16.3.0 0.0.0.127 area 0         </br>
 network 172.16.3.128 0.0.0.15 area 0          </br>
 network 172.16.3.144 0.0.0.3 area 0      </br>  
 network 172.16.3.148 0.0.0.3 area 0          </br>
   </br>
 # Verification   </br>
 <img width="1039" height="900" alt="Image" src="https://github.com/user-attachments/assets/d809e2f3-7c97-4d84-af3c-a29611e7bc34" />
</br>

## Edge router's & Ospf Configuration     </br>
</br>
Edge router-1   </br>
</br>
interface GigabitEthernet0/0    </br>
 ip address 172.16.3.146 255.255.255.252    </br>
 ip nat inside        </br>
interface GigabitEthernet0/1      </br>
 ip address 172.16.3.154 255.255.255.252     </br>
 ip nat inside      </br>

interface Serial0/0/0     </br>
 ip address 195.136.17.1 255.255.255.252      </br>
 ip nat outside     </br>
 clock rate 64000       </br>
interface Serial0/0/1     </br>
 ip address 195.136.17.5 255.255.255.252     </br>
 clock rate 64000    </br>
 </br>
router ospf 10   </br>
 router-id 3.3.3.3      </br>
 log-adjacency-changes      </br>
 network 172.16.3.144 0.0.0.3 area 0    </br>
 network 172.16.3.152 0.0.0.3 area 0     </br>
 network 195.136.17.0 0.0.0.3 area 0    </br>
 network 195.136.17.4 0.0.0.3 area 0     </br>
</br>
access-list 1 permit 172.16.1.0 0.0.0.127       </br>
access-list 1 permit 172.16.1.128 0.0.0.127      </br>
access-list 1 permit 172.16.2.0 0.0.0.127        </br>
access-list 1 permit 172.16.2.128 0.0.0.127     </br>
access-list 1 permit 172.16.3.0 0.0.0.127        </br>
access-list 1 permit 172.16.3.128 0.0.0.15       </br>
ip nat inside source list 1 interface Serial0/0/1 overload   </br>
ip route 0.0.0.0 0.0.0.0 Serial0/0/0      </br>
ip route 0.0.0.0 0.0.0.0 Serial0/0/1 60    </br>
</br>
# Verification

<img width="1048" height="910" alt="Image" src="https://github.com/user-attachments/assets/d582a84f-93fe-4591-a258-6228cff2f8c3" />
<img width="1054" height="317" alt="Image" src="https://github.com/user-attachments/assets/e49183c9-12fe-4910-a8c0-5bda561556b0" />
</br>

</br>
Edge router-2   </br>
</br>
interface GigabitEthernet0/0   </br>
 ip address 172.16.3.158 255.255.255.252    </br>
 ip nat inside             </br>

interface GigabitEthernet0/1          </br>
 ip address 172.16.3.150 255.255.255.252     </br>
 ip nat inside    </br>
 
interface Serial0/0/0    </br>
 ip address 195.136.17.13 255.255.255.252        </br>
 ip nat outside          </br>
 clock rate 64000          </br>
interface Serial0/0/1     </br>
 ip address 195.136.17.9 255.255.255.252      </br>
 ip nat outside          </br>
 clock rate 64000             </br>

 router ospf 10          </br>
 router-id 4.4.4.4            </br>
 network 172.16.3.156 0.0.0.3 area 0          </br>
 network 172.16.3.148 0.0.0.3 area 0            </br> 
 network 195.136.17.12 0.0.0.3 area 0            </br>
 network 195.136.17.8 0.0.0.3 area 0                </br>
access-list 1 permit 172.16.1.0 0.0.0.127     </br>
access-list 1 permit 172.16.1.128 0.0.0.127       </br>
access-list 1 permit 172.16.2.0 0.0.0.127    </br>
access-list 1 permit 172.16.2.128 0.0.0.127   </br>
access-list 1 permit 172.16.3.0 0.0.0.127       </br>
access-list 1 permit 172.16.3.128 0.0.0.15   </br>

ip route 0.0.0.0 0.0.0.0 Serial0/0/1            </br>
ip route 0.0.0.0 0.0.0.0 Serial0/0/0 60         </br>
ip nat inside source list 1 interface Serial0/0/1 overload    </br>

# Verification    </br>

<img width="1028" height="996" alt="Image" src="https://github.com/user-attachments/assets/9db13712-d2a4-423f-8fb8-a250bfd8f8f0" />
<img width="1040" height="350" alt="Image" src="https://github.com/user-attachments/assets/f35d0ee7-208c-469b-9c7a-c5707ed30454" />
</br>

## ISP Configuration     </br>
</br>
ISP-1 configuration </br>
</br>
interface Serial0/0/0               </br>
 ip address 195.136.17.2 255.255.255.252              </br>
 no shut                   </br>
interface Serial0/0/1           </br>
 ip address 195.136.17.10 255.255.255.252       </br>
 no shut                </br>
router ospf 10            </br>
 router-id 5.5.5.5              </br>
 network 195.136.17.0 0.0.0.3 area 0      </br>
 network 195.136.17.8 0.0.0.3 area 0       </br>
</br>
  ISP-2 configuration     </br>
</br>
interface Serial0/0/0        </br>
 ip address 195.136.17.14 255.255.255.252    </br>
 no shut         </br>
interface Serial0/0/1      </br>
 ip address 195.136.17.6 255.255.255.252     </br>
 no shut        </br>
router ospf 10         </br>
 router-id 6.6.6.6      </br
 network 195.136.17.12 0.0.0.3 area 0     </br>
 network 195.136.17.4 0.0.0.3 area 0     </br>


## SSH Configuration & Verificaton

SSH (Secure Shell) is a secure remote management protocol used to access and control network devices such as routers and switches. Unlike Telnet, which transmits data (including passwords) in plain text, SSH encrypts all communication — providing confidentiality and integrity between the administrator and the device.   </br>
To securely manage switches and routers from remote PCs.      </br>
To prevent unauthorized access by using encrypted connections.    </br>
To replace Telnet as the default remote access protocol for better security.   </br>
To ensure only authenticated users (e.g., admin) can configure network devices.   </br>
</br>

Switch> enable     </br>
Switch# configure terminal     </br>
switch(config)# ip domain-name cisco.com    </br>
switch(config)# username cisco password cisco@123   </br>
switch(config)# crypto key generate rsa     </br>
How many bits in the modulus [512]: 1024      </br>
switch(config)# line vty 0 4     </br>
switch(config-line)# transport input ssh   </br>
switch(config-line)# login local        </br>
switch(config-line)# exit              </br>
switch(config)# ip ssh version 2      </br>

# Verification

<img width="1000" height="343" alt="Image" src="https://github.com/user-attachments/assets/8b09d95b-b183-4125-b5a7-02762ea0dda0" />

## End-to-End Connectivity    

End-to-End Connectivity Verification    </br>   
To ensure full network functionality, end-to-end connectivity was tested between different network segments across floors. Using the ping command, devices from one  </br>    department successfully reached devices in another subnet through Layer 3 switches and OSPF routing.     </br>

## Verification Output
The test below shows a successful ping from a PC to the destination IP 172.16.3.145:     </br>

<img width="977" height="317" alt="Image" src="https://github.com/user-attachments/assets/7714e9cd-e058-40e0-a6ea-d68e89effc43" />


## Result 
The connectivity test shows 0% packet loss and minimal latency.    </br> 
This confirms that inter-VLAN routing, OSPF configuration, and IP addressing are functioning correctly.    </br>
All floors and departments can communicate securely through the configured network.    </br>




 









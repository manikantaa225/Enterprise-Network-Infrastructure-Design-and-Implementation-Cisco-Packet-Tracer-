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

## DHCP pool configuration

<img width="1919" height="963" alt="Image" src="https://github.com/user-attachments/assets/6e771ef5-8dfa-405d-baa7-a42f2bc6ed1e" />






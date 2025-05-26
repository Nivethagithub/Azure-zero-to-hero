# Azure Networking

## Virtual Network

A Virtual Network (VNet) in Azure is a logically isolated network that securely connects Azure resources and extends on-premises networks. Key features include:

- **Isolation**: VNets provide isolation at the network level for segmenting resources and controlling traffic.

- **Subnetting**: Divide a VNet into subnets for resource organization and traffic control.

- **Address Space**: VNets have an address space defined using CIDR notation, determining the IP address range.

## Subnets, CIDR

### Subnets

Subnets are subdivisions of a Virtual Network, allowing for better organization and traffic management.

### CIDR (Classless Inter-Domain Routing)

CIDR notation represents IP addresses and their routing prefix, specifying the range of IP addresses for a network.

## Routes and Route Tables

### Routes

Routes dictate how network traffic is directed, specifying the destination and next hop.

### Route Tables

Route Tables are collections of routes associated with subnets, enabling custom routing rules.

A Route Table is a networking component used to determine where network traffic is directed within network. It contains a set of rules (routes) that specify how packets should be forwarded.

## Network Security Groups (NSGs)

NSGs are fundamental for Azure's network security, allowing filtering of inbound and outbound traffic. Key aspects include:

- **Rules**: NSGs define allowed or denied traffic based on source, destination, port, and protocol.

- **Default Rules**: NSGs have default rules for controlling traffic within the Virtual Network and between subnets.

- **Association**: NSGs can be associated with subnets or individual network interfaces.

## Application Security Groups (ASGs)

ASGs group Azure virtual machines based on application requirements, simplifying network security:

- **Simplification**: ASGs allow defining rules based on application roles instead of individual IP addresses.

- **Dynamic Membership**: ASGs support dynamic membership based on tags or other attributes.

- **Rule Association**: Security rules can be associated with ASGs for intuitive and scalable network security management.

## 
| Use NSG when...                         | Use ASG when...                                  |
| --------------------------------------- | ------------------------------------------------ |
| You need to allow/deny traffic.         | You want to group VMs for easier rule targeting. |
| Managing access at subnet or NIC level. | Managing rules for dynamic VM groups.            |


##
| Feature              | **NSG (Network Security Group)**                     | **ASG (Application Security Group)**                               |
| -------------------- | ---------------------------------------------------- | ------------------------------------------------------------------ |
| **Purpose**          | Controls inbound/outbound network traffic via rules. | Groups VMs with similar functions to simplify NSG rule management. |
| **Type**             | Firewall-like rule set.                              | Logical container for grouping VMs.                                |
| **Applies To**       | Subnets or Network Interfaces (NICs).                | Referenced inside NSG rules.                                       |
| **Contains**         | Rules (Source/Destination, Port, Protocol, Action).  | A set of VM NICs grouped together.                                 |
| **Granularity**      | Enforces traffic rules.                              | Used within NSGs to target groups.                                 |
| **Example Usage**    | Allow only port 80 traffic to a subnet.              | Target all web servers grouped in an ASG in an NSG rule.           |
| **Scalability**      | Rules can get complex with many VMs.                 | Simplifies rules by grouping similar VMs.                          |
| **Can Stand Alone?** | Yes, used independently.                             | No, must be used inside NSG rules.                                 |


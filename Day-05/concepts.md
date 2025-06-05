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

##

what is standalone here ?


| Concept                              | Can it be used on its own? | Explanation                                                                                                            |
| ------------------------------------ | -------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **NSG (Network Security Group)**     | ✅ **Yes (Standalone)**     | You can create NSG rules and associate them directly with subnets or NICs. It works independently.                     |
| **ASG (Application Security Group)** | ❌ **No (Not Standalone)**  | An ASG **must** be used **inside an NSG rule**. It cannot control traffic by itself. It only groups VM NICs logically. |


🔸 Example:

* You can create an NSG, add a rule to allow port 80 from any source, and assign it to a subnet — that’s standalone use.
* You cannot create an ASG and expect it to filter traffic. You must reference the ASG in an NSG rule.

#
In Azure, NSG (Network Security Group) and ASG (Application Security Group) are both used for managing network security, but they serve different purposes and work together in many scenarios.

## ✅ Network Security Group (NSG)
Purpose: Controls inbound and outbound network traffic to and from Azure resources at the subnet or NIC (Network Interface Card) level.

**🔑 Key Features:**
1. Works like a firewall.
2. Contains security rules with:
      - Source/Destination (IP, IP range, ASG)
      - Port number
      - Protocol (TCP/UDP/Any)
      - Allow/Deny
3. Can be associated with:
   - A subnet
   - A network interface (NIC) of a VM

**📌 Example Use Case:**
Block all internet traffic to a subnet except for ports 80 and 443.

## ✅ Application Security Group (ASG)
Purpose: A logical grouping of VMs based on application roles, enabling easier network rule management without hardcoding IP addresses.

**🔑 Key Features:**
1. Acts like a label for NICs.
2. Can be used in NSG rules as source or destination.
3. Allows you to group VMs like:
  - web-servers
  - app-servers
  - db-servers
4. Useful in dynamic or large-scale environments.

**📌 Example Use Case:**
Allow traffic from ASG web-servers to ASG app-servers on port 8080 using a single NSG rule.

## 🆚 NSG vs ASG Summary
| Feature              | NSG                                 | ASG                                         |
| -------------------- | ----------------------------------- | ------------------------------------------- |
| Purpose              | Enforces security rules             | Groups VMs for simplified rule creation     |
| Works at             | Subnet or NIC level                 | NIC level only                              |
| Contains rules       | Yes                                 | No (used **in** NSG rules)                  |
| Can be used in rules | Yes (source/destination IP/ASG)     | Only used **as source/destination** in NSG  |
| Example              | Deny all traffic except 22, 80, 443 | Allow `web-servers` to talk to `db-servers` |

**🔗 Relationship:**
* NSG enforces the rules.
* ASG simplifies the targets/sources in those rules.

You typically use both together to create scalable, flexible, and maintainable network security policies.



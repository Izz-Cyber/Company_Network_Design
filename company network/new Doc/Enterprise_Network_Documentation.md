# Enterprise Network Documentation

## 1. Introduction

This network has been designed to represent a comprehensive infrastructure for a large enterprise, taking into account the essential requirements of various departments to ensure efficient and secure operations. This documentation aims to provide a comprehensive overview of the network design, its components, and connection details.

## 2. General Network Structure

The network consists of five floors, each designed to host specific departments and functions, reflecting the organizational distribution of the enterprise:

| Floor | Main Departments / Function |
| :---- | :------------------------ |
| First   | Offices and Customer Service, Warehouses, Cashier, Reception, General Archive, Staff Affairs, Healthcare, Eligibility Office |
| Second  | Offices, Employee Lounge, Commercial Department, IT Department |
| Third  | Administrative Offices, Service Manager, Human Resources, Marketing, Archive |
| Fourth  | Administrative Offices, Manager's Office |
| Fifth  | **First Half:** Monitoring Office (Cameras), Cybersecurity Department. **Second Half:** Server Room (Data Center) |

## 3. Devices and Technologies Used

The network primarily relies on Cisco devices and includes a wide range of equipment to ensure connectivity and required functionalities:

### 3.1. Core Network Devices

| Device             | Description                                                                |
| :----------------- | :------------------------------------------------------------------- |
| Core Switch Layer 3 | Core switches on each floor, plus two main (primary and backup) core switches |
| Switch Layer 2     | Branch switches on floors and in the server room                                |
| Router             | Two main (primary and backup) routers for Internet connectivity                   |
| Access Point (AP)  | Wireless access points to provide Wi-Fi coverage                                |

### 3.2. End Devices and Servers

| Category        | Devices                                                                                                                              |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| User Devices | Personal Computers (PCs), Laptops, Tablets, Smartphones, IP Phones |
| Printers     | Wired and wireless printers                                                                                                                |
| Surveillance     | Surveillance Cameras, Monitors (TVs)                                                                                            |
| Servers      | Web and Email server (WEB-Email-server), DNS server, DHCP server, unnamed server (future)                                          |
| Other         | Cooling fans in server rooms, Coffee Machines                                                                      |

## 4. Connection and Interconnectivity Design

### 4.1. Core Switches

*   A Core Switch Layer 3 is present on each floor (Layer1, Layer2, Layer3, Layer4, Security Section(Layer5), CenterRoom(Layer5)).
*   All floor core switches are connected to two main Core Switch Layer 3 devices: `MainSwitch` (primary) and `AlternativePath1` (backup) to ensure high availability and fault tolerance.
*   EtherChannel technology is used between some core switches to increase bandwidth and flexibility.

### 4.2. Routers

*   There are two main routers: `internet1` (primary) and `internet2` (backup).
*   Both `MainSwitch` and `AlternativePath1` are connected to `internet1` and `internet2`.
*   EtherChannel technology is used between the main core switches and routers to increase bandwidth and flexibility.

### 4.3. Data Center

*   Contains two Layer 2 switches:
    *   `DMZ(CenterRoom(Layer5))`: Dedicated to the DMZ zone, directly connected to `internet1` and `internet2`.
    *   `CenterRoom(Layer5)`: Dedicated to the remaining servers (DNS, DHCP, Server 3), connected to the main core switches `MainSwitch` and `AlternativePath1`.
*   A Web and Email server (WEB-Email-server) is located in the DMZ zone.

### 4.4. Wireless Network

*   Wireless connectivity is provided via Access Points (APs) distributed across different floors.
*   APs are connected directly to Layer 2 switches or Core Switches.

### 4.5. Cameras

*   All cameras in the network (wired and wireless) are connected to a dedicated VLAN for surveillance.
*   Cameras are connected to specific ports on Layer 2 switches or Core Switches.

## 5. Floor and Device Details

### 5.1. First Floor (Layer1)

*   **Core Switch:** Core Switch Layer 3 named `Layer1`.
*   **Branch Switches:** Two Layer 2 Switches named `S1.1` and `S1.2`.
*   **Access Points:** `AP S1.1-1.1` (connected to `S1.1`) and `AP S1.2-2.1` (connected to `S1.2`).
*   **Departments and Devices:**
    *   **Warehouse Office:** PC, IP Phone, Printer (connected to `S1.1`).
    *   **Cashier Office (Fund):** PC, IP Phone, Printer (connected to `S1.2`).
    *   **Reception and Customer Service:** 5 PCs, 5 IP Phones, Printer, Tablet (connected to `S1.2`).
    *   **Shared Offices (one hall):** General Archive, The Staff Affairs, Healthcare, Eligibility Office. PCs, IP Phones, two shared printers (connected to `S1.1`).
*   **Cameras:** A surveillance camera connected to `S1.2` on port `Fa0/10`, named `C Layer1(S1.2-2.1)`.
*   **Branch Switches to Core Switch Connection:** `S1.1` and `S1.2` connect to `Layer1` via ports `Fa0/1` and `Fa0/2` respectively, and port `Fa0/24` on the branch switches.
*   **APs to Switches Connection:** APs connect to branch switches on port `Fa0/16`.

### 5.2. Second Floor (Layer2)

*   **Core Switch:** Core Switch Layer 3 named `Layer2`.
*   **Branch Switches:** None.
*   **Access Points:** `AP Layer2-2.1` (connected to `Layer2` on port `Fa0/16`) and `AP-Lounge(Layer2-2.2)` (connected to `Layer2` on port `Fa0/17`).
*   **Departments and Devices:**
    *   **Commercial Department Office:** 3 PCs, 3 IP Phones, Printer (wireless).
    *   **IT Office:** 2 PCs (one with IP Phone), Printer, Laptop, Tablet.
    *   **Employee Lounge:** Coffee machine (wireless), laptops, smartphones, and tablets connect wirelessly.
*   **Cameras:** A surveillance camera in the lounge named `C Layer2(Lounger2.2-2.1)`, connected wirelessly to `AP-Lounge(Layer2-2.2)`.
*   **Devices to Core Switch Connection:** Devices connect directly to `Layer2` starting from port `Fa0/1`.

### 5.3. Third Floor (Layer3)

*   **Core Switch:** Core Switch Layer 3 named `Layer3`.
*   **Branch Switches:** None.
*   **Access Points:** `AP Layer3-3.1` (connected to `Layer3` on port `Fa0/16`).
*   **Departments and Devices:**
    *   **Service Manager Office:** PC, IP Phone, Printer (wireless).
    *   **Human Resources (HR) Department:** 2 PCs, 2 IP Phones, Printer.
    *   **Marketing Department:** PC, IP Phone, 2 Laptops (wireless), Tablet.
    *   **Archive Department:** 2 PCs (one with IP Phone), Printer (wireless), Smartphone.
*   **Cameras:** A camera named `C Layer3(AP3.1-1.1)` connected directly to `AP Layer3-3.1`.
*   **Devices to Core Switch Connection:** Devices connect directly to `Layer3` starting from port `Fa0/1`.

### 5.4. Fourth Floor (Layer4)

*   **Core Switch:** Core Switch Layer 3 named `Layer4`.
*   **Branch Switches:** Three Layer 2 Switches named `S4.1`, `S4.2`, and `S4.3`.
    *   Branch switches connect to `Layer4` via port `Fa0/1` on `Layer4` to port `Fa0/24` on the branch switches.
*   **Access Points:**
    *   `AP S4.1-1.1` (connected to `S4.1` on port `Fa0/16`).
    *   `AP S4.2-2.1` (connected to `S4.2` on port `Fa0/16`).
    *   `AP S4.3-3.1` (connected to `S4.3` on port `Fa0/16`).
*   **Departments and Devices:**
    *   **Branch Switch `S4.1`:**
        *   **Manager's Office Manager:** PC, IP Phone, Printer (wireless).
        *   **Meeting Room:** TV, Tablet (connect wirelessly to `AP S4.1-1.1`).
        *   **Manager Office:** PC, IP Phone, Laptop (wireless), Smartphone.
        *   **Manager's Secretary:** PC, IP Phone, Printer (wireless) (on the same VLAN as Manager Office).
        *   **Public Relations Office:** 3 PCs, 3 IP Phones, shared Printer.
    *   **Branch Switch `S4.2`:**
        *   **Deputy Office:** PC, IP Phone, Smartphone.
        *   **Deputy's Secretary:** PC, IP Phone, Printer (wireless) (on the same VLAN as Deputy Office).
        *   **Director General of Finance and Accounts:**
            *   Director: PC, IP Phone.
            *   Accounts Officer: PC, IP Phone.
            *   Checks and Bank Officer: PC, IP Phone.
            *   Auditor: PC, IP Phone.
            *   Two wireless printers.
    *   **Branch Switch `S4.3`:**
        *   **Oversight Office:** 2 PCs, 2 IP Phones, Printer (wireless).
        *   **Technical Department Manager Office:** PC, IP Phone, Printer (wireless), Tablet.
        *   **Statistics Office:** PC, IP Phone, Printer (wireless).
*   **Cameras:** A basic camera connected to `S4.3` via cable `Fa0/10`, named `C Layer4(S4.3-3.1)`.
*   **End Device Connection:** All end devices connect to branch switches starting from port `Fa0/1`.

### 5.5. Fifth Floor (First Half - Security and Monitoring Department)

*   **Core Switch:** Core Switch Layer 3 named `Security Section(Layer5)`.
*   **Branch Switches:** Two Layer 2 Switches named `S5.1` (for monitoring) and `S5.2` (for cybersecurity).
*   **Access Points:** `AP S5.2-2.1w` (connected to `S5.2` on port `Fa0/16`).
*   **Departments and Devices:**
    *   **Monitoring Department:** PC, IP Phone, Printer (wired). Connected to `S5.1`.
    *   **Cybersecurity Department:** PC, IP Phone, PC (without IP Phone), 2 Laptops (wired), Printer (wireless), 2 TVs (wireless), Tablet. Connected to `S5.2`.
*   **Cameras:** A camera named `C CY` connected to `S5.2` on port `Fa0/10`. In addition to 15 cameras distributed throughout the company (one camera per floor, two in the server room, one in the cybersecurity department, one external camera, one at the main entrance, one at the back entrance, two in the parking lot, one in the warehouse, one on the fifth floor).
*   **Branch Switches to Core Switch Connection:** `S5.1` and `S5.2` connect to `Security Section(Layer5)` via ports `Fa0/1` and `Fa0/2` respectively, and port `Fa0/24` on the branch switches.

### 5.6. Fifth Floor (Second Half - Data Center)

*   **Core Switch:** Core Switch Layer 3 named `CenterRoom(Layer5)`.
*   **Branch Switches:** Two Layer 2 Switches named `DMZ(CenterRoom(Layer5))` and `CenterRoom(Layer5)`.
*   **Routers:** `internet1` and `internet2`.
*   **Devices and Servers:**
    *   **`DMZ(CenterRoom(Layer5))`:** Connects to `internet1` (port `Gig0/1` to `Gig0/1/3`) and `internet2` (port `Gig0/2` to `Gig0/1/3`). Connected to `WEB-Email-server` (port `Fa0/1`) and `DMZ FAN` (port `Fa0/15`).
    *   **`CenterRoom(Layer5)`:** Connects to `MainSwitch` (port `Gig0/1` to `Gig1/0/15`) and `AlternativePath1` (port `Gig0/2` to `Gig1/0/15`). Connected to `DNS` (port `Fa0/1`), `DHCP` (port `Fa0/2`), `Server 3` (port `Fa0/3`), and `CenterRoom(Layer5) FAN` (port `Fa0/15`).
*   **Cameras:** Two wired cameras named `C CenterRoom1` (port `Fa0/10`) and `C CenterRoom2` (port `Fa0/11`).

## 6. Main Core Switches and Routers Interconnectivity

### 6.1. Floor Core Switches to MainSwitch and AlternativePath1 Connection

| Floor Core Switch | Connection to MainSwitch (Floor Core Switch Port -> MainSwitch Port) | Connection to AlternativePath1 (Floor Core Switch Port -> AlternativePath1 Port) |
| :----------------- | :---------------------------------------------------------------- | :--------------------------------------------------------------------------- |
| Layer1             | `Gig0/1` -> `Gig1/0/11`                                           | `Gig0/2` -> `Gig1/0/11`                                                      |
| Layer2             | `Gig0/1` -> `Gig1/0/12`                                           | `Gig0/2` -> `Gig1/0/12`                                                      |
| Layer3             | `Gig0/1` -> `Gig1/0/13`                                           | `Gig0/2` -> `Gig1/0/15`                                                      |
| Layer4             | `Gig0/1` -> `Gig1/0/14`                                           | `Gig0/2` -> `Gig1/0/14`                                                      |
| Security Section(Layer5) | `Gig0/1` -> `Gig1/0/16`                                           | `Gig0/2` -> `Gig1/0/16`                                                      |
| CenterRoom(Layer5) | `Gig0/1` -> `Gig1/0/15`                                           | `Gig0/2` -> `Gig1/0/15`                                                      |

### 6.2. MainSwitch and AlternativePath1 to Routers Connection

*   **MainSwitch:**
    *   `Gig1/0/1` -> `internet1` (`Gig0/0/0`)
    *   `Gig1/0/2` -> `internet1` (`Gig0/0/1`)
    *   `Gig1/0/3` -> `internet2` (`Gig0/0/0`)
    *   `Gig1/0/4` -> `internet2` (`Gig0/0/1`)
    *   (EtherChannel used between MainSwitch and routers)
*   **AlternativePath1:**
    *   `Gig1/0/1` -> `internet1` (`Gig0/1/0`)
    *   `Gig1/0/2` -> `internet1` (`Gig0/1/1`)
    *   `Gig1/0/3` -> `internet2` (`Gig0/1/0`)
    *   `Gig1/0/4` -> `internet2` (`Gig0/1/1`)

## 7. Proposed VLAN and IP Address Segmentation

To ensure security, efficiency, and ease of management, the network will be segmented into logical VLANs, with appropriate IP ranges allocated to each. The `192.168.0.0/16` network will be used as an example for the overall enterprise IP range.

| VLAN ID | VLAN Name             | Description                                                                | Proposed IP Range (Example) |
| :------ | :-------------------- | :------------------------------------------------------------------- | :------------------ |
| 10      | Administration        | Administrative offices (Third and Fourth Floors, Manager's Office, Public Relations, Deputy Office, Director General of Finance and Accounts, Oversight, Statistics) | `192.168.10.0/24`   |
| 20      | Customer Service      | Reception and Customer Service (First Floor)                               | `192.168.20.0/24`   |
| 30      | Warehouse & Cashier   | Warehouse office, Cashier office (First Floor)                             | `192.168.30.0/24`   |
| 40      | Shared Offices        | General Archive, Staff Affairs, Healthcare, Eligibility Office (First Floor) | `192.168.40.0/24`   |
| 50      | Commercial Department | Commercial Department (Second Floor)                                     | `192.168.50.0/24`   |
| 60      | IT Department         | Information Technology Department (Second Floor)                               | `192.168.60.0/24`   |
| 70      | Human Resources       | Service Manager, Human Resources (Third Floor)                         | `192.168.70.0/24`   |
| 80      | Marketing             | Marketing Department (Third Floor)                                          | `192.168.80.0/24`   |
| 90      | Surveillance          | All cameras in the network and monitoring office (Fifth Floor)             | `192.168.90.0/24`   |
| 100     | Cybersecurity         | Cybersecurity Department (Fifth Floor)                                  | `192.168.100.0/24`  |
| 110     | Internal Servers      | DNS, DHCP, Server 3 (Server Room)                             | `192.168.110.0/24`  |
| 120     | DMZ                   | Web and Email server (Server Room)                         | `192.168.120.0/24`  |
| 130     | Wireless Network      | All wireless devices connected to APs (can be further segmented later)          | `192.168.130.0/24`  |
| 140     | IP Phones             | All IP Phones in the network                                              | `192.168.140.0/24`  |

**Notes on VLAN Segmentation:**

*   **Cameras:** All cameras will be on a single VLAN (`VLAN 90`) for easy management and centralized monitoring.
*   **Servers:** DMZ servers will be separated from internal servers in different VLANs for increased security.
*   **Wireless Network:** Initially, all wireless devices can be placed on a single VLAN (`VLAN 130`). It can later be segmented into sub-VLANs based on departments or user types if necessary.
*   **IP Phones:** A separate VLAN (`VLAN 140`) can be dedicated to IP Phones to ensure Quality of Service (QoS).
*   **Cybersecurity:** The Cybersecurity Department (`VLAN 100`) will have access and monitoring privileges over all other VLANs to enable them to perform their security tasks effectively.

## 8. Honeypot Server Addition Plan

To enhance network security and detect intrusion attempts, a Honeypot Server will be added.

*   **Proposed Location:** The Honeypot server can be placed in `VLAN 100` (Cybersecurity), `VLAN 110` (Internal Servers), or even `VLAN 120` (DMZ) depending on the objective of the Honeypot.
    *   **If the goal is to detect internal attacks:** It is preferable to place it in `VLAN 110` or `VLAN 100`.
    *   **If the goal is to detect external attacks:** It is preferable to place it in `VLAN 120` (DMZ).
*   **Initial Recommendation:** It is recommended to place it in `VLAN 100` (Cybersecurity) to be under the direct supervision of the Cybersecurity Department, with access only by them, allowing them to effectively analyze threats without exposing real systems to risk.

## 9. Standards

To ensure network quality and stability, the following standards must be adhered to:

*   **Cisco Standards:** Utilize Cisco best practices and recommendations for device configuration.
*   **IEEE Standards:** Adhere to IEEE standards for Ethernet and wireless networks (e.g., 802.3 and 802.11).
*   **Security Standards:** Implement strict security policies, including access control, encryption, and intrusion detection/prevention systems.
*   **Naming Conventions:** Adhere to naming conventions for devices, ports, and VLANs for ease of management and maintenance.
*   **Documentation:** Regularly update this documentation to reflect any changes to the network.

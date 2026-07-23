# Azure Virtual Networks Lab — Contoso Multi-Region Setup

A hands-on Azure Networking lab where I designed and deployed a multi-region virtual network topology for a fictional company, **"Contoso"** — covering resource groups, VNets, subnets, and a gateway subnet, across 3 Azure regions.

---

##  Overview

This project simulates a real enterprise scenario: a company with core IT services, a manufacturing site, and a research division, each needing isolated but interoperable networks in Azure.

I built:

- **1 Resource Group** to organize all resources
- **3 Virtual Networks** in 3 different regions (US, Europe, Asia)
- **8 Subnets total**, including a dedicated `GatewaySubnet` for future VPN/ExpressRoute connectivity
- Verified all deployments directly in the Azure Portal

---

#  Architecture

```text
ContosoResourceGroup (East US)
│
├── CoreServicesVnet (East US) — 10.20.0.0/16
│   ├── GatewaySubnet            10.20.0.0/27
│   ├── SharedServicesSubnet     10.20.10.0/24
│   ├── DatabaseSubnet           10.20.20.0/24
│   └── PublicWebServiceSubnet   10.20.30.0/24
│
├── ManufacturingVnet (West Europe) — 10.30.0.0/16
│   ├── ManufacturingSystemSubnet  10.30.10.0/24
│   ├── SensorSubnet1              10.30.20.0/24
│   ├── SensorSubnet2              10.30.21.0/24
│   └── SensorSubnet3              10.30.22.0/24
│
└── ResearchVnet (Southeast Asia) — 10.40.0.0/16
    └── ResearchSystemSubnet       10.40.0.0/24
```

---

#  Why this design

- **Non-overlapping address spaces** — each VNet uses a distinct `/16` block (`10.20`, `10.30`, `10.40`) so they can be peered later without IP conflicts.

- **Room to grow** — subnets don't consume the full VNet address space; extra room is reserved for future subnets.

- **GatewaySubnet** — reserved in `CoreServicesVnet` to support a future VPN Gateway or ExpressRoute connection back to on-premises.

- **Region placement** — VNets are placed close to where they're actually used (core IT in the US, manufacturing plant in Europe, research team in Asia), reducing latency.

---

#  Steps performed

1. Created the `ContosoResourceGroup` resource group in East US.
2. Created `CoreServicesVnet` (`10.20.0.0/16`) with 4 subnets, including a reserved `GatewaySubnet`.
3. Created `ManufacturingVnet` (`10.30.0.0/16`) in West Europe with 4 subnets for manufacturing systems and 3 sensor networks.
4. Created `ResearchVnet` (`10.40.0.0/16`) in Southeast Asia with 1 subnet for research systems.
5. Verified all VNets and subnets via **All resources** and each VNet's **Subnets** blade.

---

# 📸 Screenshots

<img width="921" height="396" alt="image" src="https://github.com/user-attachments/assets/8e28614e-0171-4737-ad75-dcb818bad6d4" />
creation a virtual network 
<img width="571" height="364" alt="image" src="https://github.com/user-attachments/assets/1dfe2bbc-04b1-444a-8173-d5f99507df22" />
<img width="729" height="403" alt="image" src="https://github.com/user-attachments/assets/5c41f58d-ee63-4755-b83e-df7d833256b3" />

<img width="678" height="431" alt="image" src="https://github.com/user-attachments/assets/6347ff18-f564-4132-b5e5-90eae30d47d8" />

<img width="826" height="183" alt="image" src="https://github.com/user-attachments/assets/3fa30d49-3a87-4cfe-9ad3-ce59bccae137" />






#  Key takeaways

- Azure Virtual Network is the fundamental building block for private networking in Azure — it lets resources communicate securely with each other, the internet, and on-prem networks.

- Subnets segment a VNet's address space; planning ahead (not using the whole range immediately) avoids costly re-addressing later.

- A `GatewaySubnet` is a reserved, purpose-built subnet needed before you can attach a VPN Gateway or ExpressRoute circuit.

---

#  Possible next steps

- Set up VNet peering between `CoreServicesVnet` and the other two VNets.
- Attach a VPN Gateway to `GatewaySubnet` for a simulated hybrid connection.
- Add Network Security Groups (NSGs) to each subnet to enforce traffic rules.

---

#  Tools used

- Azure Portal
- Azure Virtual Networks & Subnets

---

> This project was completed as part of hands-on Azure networking practice, building toward a Cloud/DevOps portfolio.

# azure-networking-lab
# Azure Networking Lab (CLI-Based Infrastructure Project)

## Overview
This project demonstrates the design and implementation of a virtual network in Microsoft Azure using both the Azure Portal and Azure CLI. The focus is on cloud networking fundamentals, subnet design, and network security configuration.

Due to Azure subscription policy restrictions, compute resources (virtual machines) could not be deployed. However, the full networking and security architecture was successfully implemented and validated.

---

## Architecture

- Virtual Network: `cloud-engineer-vnet`
- Address Space: `10.0.0.0/16`
- Subnet: `web-subnet (10.0.1.0/24)`
- Region: East US 2

---

## Components Implemented

### 1. Virtual Network (VNet)
- Created a private network in Azure
- Defined IP address space for future workloads

### 2. Subnets
- Created `web-subnet`
- Segmented network for workload separation

### 3. Network Security Group (NSG)
- Created via Azure CLI
- Configured inbound rule:
  - Allow SSH (TCP 22)
- Attached to subnet for traffic control

---

## Azure CLI Commands Used

```bash
az login
az network vnet list -o table
az network vnet subnet list -g rg-azure-enterprise-lab -o table

az network nsg create \
  --resource-group rg-azure-enterprise-lab \
  --name web-subnet-nsg \
  --location eastus2

az network nsg rule create \
  --resource-group rg-azure-enterprise-lab \
  --nsg-name web-subnet-nsg \
  --name allow-ssh \
  --priority 1000 \
  --direction Inbound \
  --access Allow \
  --protocol Tcp \
  --destination-port-ranges 22 \
  --source-address-prefixes "*"

# Microsoft Azure Implementation Sample

This repository contains a basic implementation sample for Microsoft Azure. The sample includes the creation of a Virtual Network (VNet), a Virtual Machine (VM), and a Storage Account using Azure CLI.

## Prerequisites

1. **Azure Account:** You need access to a Microsoft Azure account.
2. **Azure CLI:** Install and configure the Azure Command Line Interface. Instructions can be found [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).

## Steps to Run

### 1. Create a Resource Group:

```bash
az group create --name MyResourceGroup --location eastus
```
### 2. Create a Virtual Network:

```bash
az network vnet create --resource-group MyResourceGroup --name MyVNet --address-prefixes 10.0.0.0/16 --subnet-name MySubnet --subnet-prefix 10.0.0.0/24
```
### 3. Create a Network Security Group:

```bash
az network nsg create --resource-group MyResourceGroup --name MyNSG
```
### 4. Create a Virtual Machine:

```bash
az vm create --resource-group MyResourceGroup --name MyVM --image UbuntuLTS --admin-username azureuser --admin-password "<your-password>" --nsg MyNSG --subnet MySubnet --public-ip-address ""
```
### 5. Create a storage Account:

```bash
az storage account create --resource-group MyResourceGroup --name mystorageaccount --location eastus --sku Standard_LRS
```
### 6. Navigate to the Storage Account:

```bash
az storage account show-connection-string --resource-group MyResourceGroup --name mystorageaccount --query "connectionString" --output tsv
```
### 7. Upload a File:

```bash
az storage blob upload --account-name mystorageaccount --account-key <your-storage-account-key> --container-name <your-container-name> --name <your-blob-name> --type block --content-type "application/octet-stream" --content-encoding "gzip" --type block --content <path-to-local-file>
```
## Additional Inforamtion

```vbnet
Make sure to replace placeholders with actual values, and be cautious with handling access keys.
Note that using Azure Key Vault or Shared Access Signatures (SAS) for more secure access is recommended in production scenarios.
```

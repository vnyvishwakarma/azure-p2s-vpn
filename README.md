# Create P2S VPN Connection on Azure

## Introduction

This guide outlines the steps to create a Point-to-Site (P2S) VPN connection between an "on-premises" user virtual machine and a virtual network in Azure. This setup is intended to enable secure access to Azure resources from a remote location, utilizing an Azure VPN gateway.

### Prerequisites

- Access to an Azure account and the Azure portal.
- A user VM to serve as the "on-premises" client.
- PowerShell access on the user VM.
- Internet connectivity for downloading necessary tools and accessing the Azure portal.

## Steps Overview

1. **Preparation**: Log into Azure Portal.
2. **Connect to User VM**: Access the user VM using Remote Desktop.
3. **Generate Certificates**: Create both a self-signed root certificate and a client certificate.
4. **Export the Public Key**: Export the public key from the root certificate.
5. **Configure the VPN Gateway**: Insert the public certificate data into the Azure VPN Gateway configuration.
6. **Install the VPN Client**: Download and install the VPN client on the user VM.
7. **Test Connectivity**: Ensure the VPN connection is established and functioning.

## Detailed Instructions

### 1. Preparation

- Ensure you are logged into the Azure portal using an incognito or private browser window to avoid session conflicts with your personal account.
- **Note**: The creation of the VPN gateway may take between 30-45 minutes.

### 2. Connect to User VM

- Utilize Remote Desktop to connect to your user VM using the provided public IP address and credentials.

### 3. Generate Certificates

#### Generate the Self-Signed Root Certificate

- Open PowerShell on the user VM.
- Run the following command to generate a self-signed root certificate:

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign

  
```powershell
New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")





### 4. Export the Public Key

- Access the Certificate Manager to export the public key of the root certificate and copy its data.

### 5. Configure VPN Gateway

- Navigate to the virtual network gateway's Point-to-site configuration in the Azure portal.
- Enter the root certificate name and paste the copied public key data.
- Save your changes.

### 6. Install VPN Client

- Download the VPN client from within the Azure portal.
- Proceed to install the VPN client on the user VM.

### 7. Test Connectivity

- Establish a connection to the VPN and test it by pinging the server VM's private IP address.

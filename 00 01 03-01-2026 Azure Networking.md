# 🌐 Azure Networking Notes (VNet, Subnet, IP Addressing & Practice)

---

## 1️⃣ Resource Group (RG)

* **Resource Group** is a logical container in Azure.
* It holds related resources like:

  * VNet
  * Subnets
  * Virtual Machines
  * Public IPs, NICs, NSGs, etc.

📌 Example

```text
Resource Group: myRG
```

---

## 2️⃣ Virtual Network (VNet)

* A **VNet** is a private network in Azure (similar to VPC in AWS).
* Uses **CIDR notation** for IP addressing.
* Supports:

  * Subnets
  * Private communication
  * Internet access (via Public IP / NAT)

📌 Example

```text
VNet Name: cloud-network
Address Space: 10.0.0.0/16
```

---

## 3️⃣ IP Addressing & CIDR Calculations

### 🔢 CIDR Basics

| CIDR | Total IPs | Formula   |
| ---- | --------- | --------- |
| /16  | 65,536    | 2^(32−16) |
| /24  | 256       | 2^(32−24) |

---

### 🔹 10.0.0.0/16 Explained

* **Total IPs**

  ```
  2^(32−16) = 2^16 = 65,536 IPs
  ```

* **Azure Reserved IPs (per subnet)** → **5 IPs blocked**

  * Network address
  * Default gateway
  * Azure DNS (x2)
  * Broadcast (conceptual)

👉 **Usable IPs per subnet**

```
65,536 − 5 = 65,531
```

---

### 🔹 /24 Subnet Example

```
2^(32−24) = 2^8 = 256 IPs
256 − 5 (Azure reserved) = 251 usable IPs
```

---

## 4️⃣ Subnets (Part of VNet)

* A **Subnet** divides a VNet into smaller networks.
* Each subnet must have **non-overlapping CIDR ranges**.

📌 Example Subnets:

```text
Subnet-A → 10.0.1.0/24
Subnet-B → 10.0.2.0/24
Subnet-C → 10.0.3.0/24
```

---

## 🔐 Azure Reserved IPs in a Subnet

For **10.0.0.0/24**:

| IP Address    | Status          |
| ------------- | --------------- |
| 10.0.0.0      | Network address |
| 10.0.0.1      | Azure Gateway   |
| 10.0.0.2      | Azure DNS       |
| 10.0.0.3      | Azure DNS       |
| 10.0.0.255    | Reserved        |
| **10.0.0.4+** | ✅ Usable        |

---

## 5️⃣ Public IP vs Private IP

| Type           | Purpose                          |
| -------------- | -------------------------------- |
| **Private IP** | Internal VNet communication      |
| **Public IP**  | Internet access (SSH, RDP, HTTP) |

📌 Example

```text
VM Private IP: 10.0.1.4
VM Public IP: 20.244.8.228
```

---

![Image](https://azure-training.com/wp-content/uploads/2019/01/vnetoverview.png)

![Image](https://learn.microsoft.com/en-us/azure/virtual-network/media/subnet-extension/subnet-extension.png)

![Image](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/media/default-outbound-access/explicit-outbound-options.png)

![Image](https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/_images/hub-spoke.png)

---

## 6️⃣ VNet & Subnet Practice (Lab Flow)

### 🧪 Hands-on Steps

```text
1. Create Resource Group
2. Create VNet
3. Create Subnet A, B, C
4. Create VM1 in Subnet A
5. Create VM2 in Subnet B
6. SSH from local → VM1
7. SSH from VM1 → VM2 (private IP)
```

---

## 7️⃣ SSH Access (Linux VM)

### 🔹 From Local Machine → VM1 (Public IP)

```bash
cd Downloads
chmod 400 vm1_key.pem
ssh -i vm1_key.pem azureuser@20.244.8.228
```

---

### 🔹 From VM1 → VM2 (Private IP)

```bash
touch vm2_key.pem
nano vm2_key.pem
cat vm2_key.pem
chmod 400 vm2_key.pem

ssh -i vm2_key.pem azureuser@10.0.1.4
```

📌 **Key Concept**

> VMs in the **same VNet**, even in **different subnets**, can communicate using **private IPs** by default.

---

## 8️⃣ VNet Peering

* Connects **two VNets privately**
* Traffic stays on Microsoft backbone
* No VPN / Gateway required

### 🔹 Supported Scenarios

| Scenario                          | Supported |
| --------------------------------- | --------- |
| Same subscription                 | ✅         |
| Different subscription            | ✅         |
| Same region                       | ✅         |
| Different region (Global Peering) | ✅         |

---

### 🔹 Roles in Peering

| Role          | Description       |
| ------------- | ----------------- |
| **Requester** | Initiates peering |
| **Accepter**  | Approves peering  |

---

### 🚫 CIDR Overlap Not Allowed

❌ Invalid:

```
VNet1 → 10.0.0.0/16
VNet2 → 10.0.0.0/16
```

✅ Valid:

```
VNet1 → 10.0.0.0/16
VNet2 → 172.31.0.0/16
```

---

## 9️⃣ Azure CLI Installation & Login

### 🔹 Install PowerShell (Windows)

🔗
[https://learn.microsoft.com/en-gb/powershell/scripting/install/install-powershell-on-windows?view=powershell-7.5](https://learn.microsoft.com/en-gb/powershell/scripting/install/install-powershell-on-windows?view=powershell-7.5)

📌 Restart terminal after installation

---

### 🔹 Verify Azure CLI

```bash
az --version
```

---

### 🔹 Login to Azure

```bash
az login
```

👉 Browser opens for authentication

```bash
az login --tenant tenant-id
az login --tenant bc281606-c655-4c05-90f2-49309a59c59f
```

📌 Select subscription when prompted.

---

## 🔟 Resource Group Commands

```bash
az group create --name myResourceGroup --location eastus
```

```bash
az group delete --name myResourceGroup
```

---

## 1️⃣1️⃣ Developer Tools Setup

* **GitHub** → create account (`firstlast`)
* **VS Code Extensions**

  * Microsoft Azure
  * Git & GitHub tools

---

## ✅ Key Takeaways (Exam + Interview)

* `/16 = 65,536 IPs`
* Azure blocks **5 IPs per subnet**
* VMs in same VNet communicate privately
* VNet peering requires **non-overlapping CIDRs**
* Public IP required only for **external access**

---


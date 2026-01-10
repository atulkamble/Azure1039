# 🚀 Terraform & Git – Complete Setup and Usage Guide (Azure)

---

## 🔹 What is Terraform?

**Terraform** is an **Infrastructure as Code (IaC)** tool developed by **HashiCorp**.

### 📌 Infrastructure as Code (IaC)

IaC means:

* Infrastructure is written as **code**
* Version controlled
* Repeatable & automated
* Cloud-agnostic (Azure, AWS, GCP)

---

## 🔹 Terraform Types

* **HashiCorp Terraform** – Open-source IaC tool
* **Azure Terraform** – Terraform used to provision Azure resources

---

## 🔹 Terraform Installation

### 🪟 Windows (PowerShell – Run as Administrator)

Install **Chocolatey** first:

```
https://chocolatey.org/install
```

Install Terraform:

```powershell
choco install terraform
```

Verify:

```powershell
terraform --version
```

---

### 🍎 macOS (Homebrew)

```bash
brew install terraform
terraform --version
```

---

### 🌐 Official Terraform Download

```
https://developer.hashicorp.com/terraform/install
```

---

## 🔹 Terraform Core Files & Commands

### 📁 main.tf

Main Terraform configuration file

### ⚙️ Common Terraform Commands

```bash
terraform init -upgrade
terraform plan
terraform apply -auto-approve
terraform destroy
```

---

## 🔹 Git & GitHub Overview

### 📌 Git

* Distributed **Version Control System**
* Tracks **code changes**
* Maintains **versions**

### 📌 GitHub

* Cloud platform to host Git repositories
* Collaboration & CI/CD support

---

## 🔹 Git Installation

Download Git:

```
https://git-scm.com/install/
```

Verify:

```bash
git --version
```

---

## 🔹 GitHub Setup

Sign up:

```
https://github.com/
```

### Default Branch

```
main
```

---

## 🔹 Terraform + Git (Azure Project – Example 1)

### Clone Repository

```bash
git clone https://github.com/atulkamble/terraform-azure-2026
cd terraform-azure-2026
```

### Run Terraform

```bash
terraform init -upgrade
terraform plan
terraform apply -auto-approve
```

---

## 🔹 Terraform Azure VNet Peering Project (PowerShell)

### Clone Repository

```powershell
git clone https://github.com/atulkamble/azure-vnet-peering.git
cd azure-vnet-peering
```

### Open in VS Code

```powershell
code .
```

---

### 🔧 Configuration Step

➡️ Update **subscription-id** in:

```
provider.tf
```

---

### 🚀 Deploy Infrastructure

```bash
terraform init -upgrade
terraform plan
terraform apply -auto-approve
```

---

### 🧹 Destroy Infrastructure

```bash
terraform destroy
```

---

## ✅ Summary

* Terraform = IaC tool
* Git = Version control
* GitHub = Code hosting
* Azure + Terraform = Automated cloud infrastructure
* PowerShell / Bash supported
* Production-ready workflow

---

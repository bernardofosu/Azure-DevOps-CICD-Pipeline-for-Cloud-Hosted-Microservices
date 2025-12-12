# 🧪 Terraform One‑Command Dev + Prod (Learning Mode)

> ⚠️ **This approach is for LEARNING / LABS only**
> ❌ **NOT recommended for real production systems**

---

## 🧠 Idea: Create DEV and PROD Together

In this setup:

👉 One Terraform folder
👉 One `terraform apply` command
👉 DEV and PROD are created **at the same time**

This is useful when:

- You are learning Terraform
- You want to understand modules
- You want quick results

---

## 🧱 Project Structure (Simple – Learning)

```
aks-terraform-learning/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── provider.tf
├── versions.tf
└── terraform.tfvars
```

---

## 🧩 main.tf (DEV + PROD Together)

```hcl
# DEV AKS
module "aks_dev" {
  source = "./modules/aks"

  cluster_name        = "nakodtech-dev-cluster"
  resource_group_name = "nakodtech-dev-rg"
  location            = var.location
  dns_prefix          = "nakodtech-dev"

  kubernetes_version  = var.kubernetes_version
  node_vm_size        = var.dev_node_vm_size
  node_count          = var.dev_node_count

  service_principal_app_id     = var.service_principal_app_id
  service_principal_client_secret = var.service_principal_client_secret
}

# PROD AKS
module "aks_prod" {
  source = "./modules/aks"

  cluster_name        = "nakodtech-prod-cluster"
  resource_group_name = "nakodtech-prod-rg"
  location            = var.location
  dns_prefix          = "nakodtech-prod"

  kubernetes_version  = var.kubernetes_version
  node_vm_size        = var.prod_node_vm_size
  node_count          = var.prod_node_count

  service_principal_app_id     = var.service_principal_app_id
  service_principal_client_secret = var.service_principal_client_secret
}
```

---

## 🧮 variables.tf

```hcl
variable "location" { default = "West Europe" }
variable "kubernetes_version" { default = "1.32.9" }

variable "dev_node_vm_size"  { default = "Standard_D2s_v6" }
variable "dev_node_count"   { default = 2 }

variable "prod_node_vm_size" { default = "Standard_D4s_v6" }
variable "prod_node_count"  { default = 3 }

variable "service_principal_app_id" {}
variable "service_principal_client_secret" { sensitive = true }
```

---

## ▶️ One Command Deployment

```bash
terraform init
terraform apply
```

✅ DEV AKS created
✅ PROD AKS created
✅ One execution

---

## 👍 Why This Is GOOD for Learning

✅ Easy to understand
✅ See DEV vs PROD differences clearly
✅ Learn modules quickly
✅ Fast feedback

---

## ❌ Downsides (VERY IMPORTANT)

### 🚨 1. Single State File (BIGGEST PROBLEM)

```
terraform.tfstate
```

Contains:

- DEV resources
- PROD resources

👉 One mistake affects **both**

---

### 💥 2. Dangerous Destroy

```bash
terraform destroy
```

❌ Deletes DEV **and** PROD together

---

### 🔐 3. No Access Control

- Cannot restrict who touches PROD
- Junior engineer can break PROD

---

### 🔄 4. No Promotion Flow

❌ No DEV → PROD approval
❌ No testing gate
❌ No CI/CD stages

---

### 🧯 5. Large Blast Radius

Any change:

- affects whole infrastructure
- harder to rollback

---

## 🏁 Verdict (Very Honest)

| Use Case           | Verdict  |
| ------------------ | -------- |
| Learning Terraform | ✅ OK    |
| Demos / Labs       | ✅ OK    |
| CI/CD pipelines    | ❌ BAD   |
| Real Production    | ❌ NEVER |

---

## 🧠 Golden Rule to Remember

> **One Terraform state = one environment**

Break this rule → problems later.

---

## 🚀 Next Step (When You’re Ready)

👉 Split into:

```
environments/dev
environments/prod
```

👉 Same module
👉 Separate state
👉 Real DevOps practice

---

🎓 Learn it this way first — then move to best practice.

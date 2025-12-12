
# 🟦 How to Create an Azure DevOps Organization & Start a YAML Pipeline

---

## 🟩 1️⃣ Create or Use an Existing Azure DevOps Organization

### ✔️ Step 1: Sign In
Go to:  
🔗 **https://dev.azure.com**  
Sign in with your Microsoft account.

### ✔️ Step 2: Create New Organization (if you don’t have one)
1. Click **New organization**
2. Select a **region** closest to you
3. Pick a name (example: `nakodtech`)
4. Click **Continue**

### ✔️ If You Already Have an Organization
Just select it — no need to create a new one.

---

## 🟩 2️⃣ Create a New Project

Inside your organization:
1. Click **New Project**
2. Enter:
   - **Project name:** e.g., `bankapp`
   - **Visibility:** Private
3. Click **Create**

This project will contain your repos, pipelines, and artifacts.

---

## 🟩 3️⃣ Go to Pipelines → Create New Pipeline

1. On the left sidebar, click **Pipelines**
2. Click **New Pipeline**
3. Choose where your code is stored

---

## 🟩 4️⃣ Select Your Code Repository

You will see options:
- Azure Repos Git
- GitHub
- Bitbucket
- Other Git

### ✔ Most common:
Select **GitHub** → Authorize Azure DevOps → Choose your repo (e.g., `bankapp2`)

---

## 🟩 5️⃣ Choose YAML Configuration → Start with Starter Pipeline

Azure DevOps will offer templates.

Choose:

### ✔ **Starter Pipeline** (recommended)

This gives you:

```yaml
# Starter pipeline
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- script: echo Hello World
```

Replace this later with your real YAML pipeline.

---

## 🟩 6️⃣ Save & Run Pipeline

1. Click **Save and run**
2. Azure DevOps will:
   - Commit the YAML file (`azure-pipelines.yml`) to your repo
   - Automatically queue and run the pipeline
   - Show build logs

---

# 🟧 FINAL SUMMARY

| Step | What You Do |
|------|-------------|
| 1️⃣ | Sign into Azure DevOps |
| 2️⃣ | Create or choose an Organization |
| 3️⃣ | Create a Project |
| 4️⃣ | Go to Pipelines → New Pipeline |
| 5️⃣ | Choose Repository |
| 6️⃣ | Select **Starter YAML** |
| 7️⃣ | Save and Run |

---

🚀 **You now have a working Azure DevOps YAML pipeline setup!**


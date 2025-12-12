# 🤖 Setting Up a Self-Hosted Azure DevOps Agent (Step-by-Step)

## 🟦 1. Create a Personal Access Token (PAT)

You need a PAT so the agent can authenticate with Azure DevOps.

- Go to **User Settings → Personal Access Tokens** 🔑
- Create a token with **Agent Pools (Read & Manage)** and **Deployment Groups (optional)** permissions
- Copy the PAT (you won’t see it again!)

---

## 🟩 2. Create an Agent Pool called **nakodtech**

- Navigate to **Organization Settings → Agent Pools** 🏛️
- Click **New Agent Pool**
- Name it **nakodtech**
- Save ✔️

This pool will now exist at the **organization level** and can be shared with any project.

---

## 🟧 3. Link the Pool to Your Project

Go to:

- **Project Settings → Agent Pools → Add pool** ➕
- Choose **Existing**
- Select **nakodtech**
- Check **Grant access permission to all pipelines**

Now your project can use the pool 🚀.

---

## 🟥 4. Install and Configure the Self-Hosted Agent

Run these commands on your Linux machine:

### 📥 Download the agent

```bash
wget https://download.agent.dev.azure.com/agent/4.264.2/vsts-agent-linux-x64-4.264.2.tar.gz
```

### 📦 Extract the agent

```bash
mkdir myagent && cd myagent
tar zxvf ~/Downloads/vsts-agent-linux-x64-4.264.2.tar.gz
```

### 🛠️ Configure the agent

```bash
./config.sh
```

You will be asked for:

- **Server URL:** `https://dev.azure.com/ofosubernard2026` 🌍
- **Auth type:** Press Enter for PAT 🔑
- **Personal Access Token:** Paste the PAT
- **Agent Pool:** `nakodtech` 🏊
- **Agent Name:** Any name (e.g., `Agent-1`)
- **Work Folder:** Press Enter for `_work`

You should see:

```
Successfully added the agent 🎉
Testing agent connection...
```

---

## ▶️ 5. Start the Agent

Run the agent interactively:

```bash
./run.sh
```

Or install it as a **system service** for automatic startup 🔄.

---

## 💡 Summary

| Step | Action                               |
| ---- | ------------------------------------ |
| 1️⃣   | Create PAT 🔑                        |
| 2️⃣   | Create org-level pool `nakodtech` 🏛️ |
| 3️⃣   | Link pool to your project 🔗         |
| 4️⃣   | Download & configure agent 🤖        |
| 5️⃣   | Run agent and begin using it 🚀      |

---

If you'd like, I can add diagrams, workflow charts, or convert everything into a printable PDF! 📄✨

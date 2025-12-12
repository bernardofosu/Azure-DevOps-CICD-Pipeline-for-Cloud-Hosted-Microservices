
# 🤖 Azure DevOps Agents as Objects — With Properties & Demands

This document explains how Azure DevOps treats self‑hosted agents internally, and how pipelines select specific agents using **demands**.

---

# 🟦 Azure DevOps Agents = Objects With Properties

When you install a self‑hosted Azure DevOps agent, it becomes an **object** stored inside an **Agent Pool**.

Each agent has its own properties, such as:

- `agent.name`  
- `agent.os`  
- `agent.version`  
- `agent.machineName`  
- `agent.capabilities.*`

These properties can be used to **filter and choose** which agent runs a job.

---

# 🟩 Example: Agent Object Internally

When you register an agent named **Agent-1**, Azure DevOps stores something equivalent to:

```json
{
  "agent.name": "Agent-1",
  "agent.os": "Windows_NT",
  "agent.version": "3.232",
  "agent.machineName": "DESKTOP-01"
}
```

This makes it possible to target the exact agent you want.

---

# 🟦 Selecting an Agent Using `demands`

You can filter agents by name or any capability:

```yaml
pool:
  name: nakodtech
  demands:
    - agent.name -equals Agent-1
```

This means:

> “From pool **nakodtech**, use the agent whose name property is **Agent-1**.”

---

# 🟧 Multiple Agents Example

### Pool: `nakodtech`

| Agent Name | OS      | Purpose |
|------------|---------|---------|
| Agent-1    | Windows | Build   |
| Agent-2    | Linux   | Test    |
| Agent-3    | Windows | Deploy  |

### Select Linux agent only:

```yaml
demands:
  - agent.os -equals Linux
```

### Select Agent-2 specifically:

```yaml
demands:
  - agent.name -equals Agent-2
```

---

# ⭐ Comparison With Other CI Systems

### 🟪 GitLab  
Uses **tags**, not agent names:

```yaml
tags:
  - docker
  - self-hosted
```

### 🟧 GitHub Actions  
Uses **runner labels**:

```yaml
runs-on: ["self-hosted", "linux"]
```

### 🟦 Azure DevOps  
Uses **Agent Pool name + Demands**:

```yaml
pool:
  name: MyPool
  demands:
    - agent.name -equals MyAgent
```

---

# 🏆 Summary (Simple & Clear)

> Azure DevOps agents behave like objects with properties.  
> Pipelines can select specific agents by reading those properties using `demands:`.  
> This is different from GitLab (tags) and GitHub Actions (labels), where selection is not tied to agent names.

---

✨ This file is ideal for DevOps documentation, interviews, or portfolios.

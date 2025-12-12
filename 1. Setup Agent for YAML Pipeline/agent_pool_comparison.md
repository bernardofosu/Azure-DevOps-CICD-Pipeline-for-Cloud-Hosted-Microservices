
# 🤖 Agent Pools & Runners Comparison — GitLab vs Azure DevOps vs GitHub Actions

This document explains how each CI/CD platform selects its agents/runners and the key differences in syntax and behavior.

---

# 🟦 Azure DevOps — Agent Pools

### ✔ Uses **Agent Pools**  
Every self‑hosted or Microsoft-hosted agent belongs to a **pool**.

### ✔ YAML requires the *exact* agent pool name  
```yaml
pool:
  name: nakodtech
```

### ⚠ Must match the name under:  
**Project Settings → Agent Pools**

### Example:
If your agent pool is named **nakodtech**, YAML must be:

```yaml
pool:
  name: nakodtech
```

### ❌ If the name doesn’t match → Azure DevOps error:
> Pool not found  
> No agents could be found in pool 'DEVPOOL'

---

# 🟪 GitLab CI/CD — Runners

### ✔ Uses **Runner Tags**, not pool names  
```yaml
tags:
  - docker
  - self-hosted
```

GitLab matches a runner by *tag*, not by runner name.

### ✔ Runners are registered on the server  
You add tags when you configure:

```bash
sudo gitlab-runner register
```

---

# 🟧 GitHub Actions — Self-Hosted Runners

### ✔ Uses **runner labels**, not pool names  
```yaml
runs-on: ["self-hosted", "linux", "x64"]
```

GitHub matches runners by **labels**, e.g.:

- `self-hosted`
- `linux`
- `ubuntu-20.04`
- `x64`

### ✔ Runners appear under:
**Settings → Actions → Runners**

### ✔ No pool system like Azure DevOps.

---

# 🏆 Quick Comparison Table

| Feature | Azure DevOps 🟦 | GitLab 🟪 | GitHub Actions 🟧 |
|--------|------------------|-----------|--------------------|
| Uses agent pools | ✅ Yes | ❌ No | ❌ No |
| Uses tags / labels | ❌ No | ✅ Yes | ✅ Yes |
| YAML keyword | `pool:` | `tags:` | `runs-on:` |
| Must match exact name | ✅ Yes | ❌ Uses tags | ❌ Uses labels |
| Self-hosted setup | Agent installed + pool | Runner installed + token | Runner installed + token |

---

# 🎯 Summary (For Interviews or README)

> **Azure DevOps** requires `pool.name` to match the exact Agent Pool name.  
> **GitLab CI/CD** uses tags to match jobs to runners.  
> **GitHub Actions** uses labels for selecting runners, not pool names.

---

✨ This document is perfect for DevOps portfolios, CVs, and internal documentation.

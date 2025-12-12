# 🟦 Azure DevOps Pipeline Structure (Hierarchy Explained)

Azure DevOps YAML uses this exact structure:

```
stages:
  - stage: <stage_name>
    jobs:
      - job: <job_name>
        steps:
          - script: echo "Hello"
```

## 🔹 1. stages  
The top-level pipeline grouping.

## 🔹 2. stage  
A single stage that groups related jobs.

## 🔹 3. jobs  
A list of jobs inside a stage.

## 🔹 4. job  
Defines one job running on an agent.

## 🔹 5. steps  
Actual tasks or commands executed in the job.

---

# 🟦 Azure DevOps YAML — Which Values Are User-Defined vs System Keywords?

Here is the example:

```yaml
stages:
  - stage: compile
    displayName: "Maven Compile"
    jobs:
      - job: maven_compile
        steps:
          - script: mvn clean install
            displayName: "Run Maven Build"
```

## 🟩 System Keywords (Azure-defined)

These are fixed schema terms that **cannot be renamed**:

- `stages`
- `stage`
- `jobs`
- `job`
- `steps`
- `script`
- `displayName`
- `pool`
- `demands`

Azure DevOps expects these exact keywords.

## 🟦 User-Defined Values (you choose)

These are custom names that **you define**:

- `compile`
- `"Maven Compile"`
- `maven_compile`
- `"Run Maven Build"`

You can change these freely.

## 🟨 Real Executable Code

Only this part is **real shell code** executed on the agent:

```
mvn clean install
```

Azure executes it exactly as if you typed it in a terminal.

---

# 🧠 Summary Table

| Type | Items | Example |
|------|--------|---------|
| **System Keywords** | stages, stage, jobs, job, steps, script | Fixed YAML structure |
| **User Values** | compile, maven_compile, display names | You decide the names |
| **Real Commands** | Shell commands | mvn clean install |

---

# 🎉 Final Notes

Azure DevOps YAML =  
**Structure (fixed keywords)** + **User naming** + **Real shell commands**.


# FinOps Agent — Microsoft Copilot Studio Sample

> A production-ready **FinOps Advisor agent** built with Microsoft Copilot Studio. Helps organizations understand, manage, and optimize Microsoft cloud spending across Azure, Microsoft 365, Copilot, AI Foundry, and Fabric — grounded in official Microsoft Learn documentation.

<p align="center">
  <img src="FinOps Agent/icon.png" alt="FinOps Agent Icon" width="120" />
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/renatoromao/">
    <img src="https://img.shields.io/badge/LinkedIn-Follow%20Renato%20Romão-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
  &nbsp;
  <img src="https://img.shields.io/badge/Platform-Microsoft%20Copilot%20Studio-742774?style=for-the-badge&logo=microsoftcopilot&logoColor=white" alt="Copilot Studio" />
  &nbsp;
  <img src="https://img.shields.io/badge/Model-Claude%20Sonnet%204.6-FF6B00?style=for-the-badge&logo=anthropic&logoColor=white" alt="Model" />
</p>

<img width="1462" height="775" alt="image" src="https://github.com/user-attachments/assets/47249da6-dab2-40b3-9cd9-68e63f0c999d" />

<img width="1454" height="769" alt="image" src="https://github.com/user-attachments/assets/fe1d5d3b-6556-4c55-9b15-9fef2f422228" />

---

## What This Agent Does

The **FinOps Agent** applies [FinOps Foundation](https://www.finops.org/) principles to Microsoft cloud services, giving your team instant, grounded guidance on:

| Domain | Coverage |
|---|---|
| **Azure Cost Management** | Budgets, alerts, reservations, savings plans, right-sizing |
| **Microsoft 365** | E3/E5 licensing, license optimization, usage analytics |
| **Microsoft Copilot** | M365 Copilot licensing, Copilot Studio consumption billing, ROI |
| **Microsoft Foundry** | Token-based pricing, model deployment costs, AI workload optimization |
| **Microsoft Fabric** | Capacity units, workload cost management, reserved capacity |
| **FinOps Best Practices** | Chargeback/showback, tagging, budgeting, forecasting, cost allocation |

All answers are **grounded in official Microsoft Learn documentation** through semantic search — no hallucinations, no guesswork.

---

## Agent Architecture

```
FinOps Agent/
├── agent.mcs.yml           # Core agent config, instructions & AI settings
├── settings.mcs.yml        # Access control, auth, generative AI features
├── icon.png                # Agent icon
├── knowledge/              # 6 Microsoft Learn knowledge sources
│   ├── azure-cost-management-billing.knowledge.mcs.yml
│   ├── finops-with-azure.knowledge.mcs.yml
│   ├── azure-ai-foundry.knowledge.mcs.yml
│   ├── copilot-for-microsoft-365.knowledge.mcs.yml
│   ├── microsoft-365-licensing-pricing.knowledge.mcs.yml
│   └── microsoft-fabric-pricing-capacity.knowledge.mcs.yml
└── topics/                 # 13 conversation topics
    ├── ConversationStart.mcs.yml
    ├── Search.mcs.yml      # Conversational boosting / main knowledge search
    ├── Greeting.mcs.yml
    ├── Fallback.mcs.yml
    ├── Escalate.mcs.yml
    └── ...
```

---

## Prerequisites

Before you deploy, make sure you have:

- [ ] A **Microsoft 365 tenant** with Copilot Studio license
- [ ] **Copilot Studio** access ([aka.ms/copilotstudio](https://aka.ms/copilotstudio))
- [ ] The **Copilot Studio VS Code extension** installed ([install here](https://marketplace.visualstudio.com/items?itemName=ms-CopilotStudio.vscode-copilotstudio))
- [ ] **VS Code** (latest stable version)
- [ ] **Git** installed locally

---

## Deploy in 7 Steps

### Step 1 — Clone This Repository

```bash
git clone https://github.com/renatoromao/copilotstudio-samples-finops.git
cd copilotstudio-samples-finops
```

### Step 2 — Open in VS Code

```bash
code .
```

### Step 3 — Create a New Agent in Copilot Studio

1. Go to [Copilot Studio](https://aka.ms/copilotstudio) and sign in.
2. Click **Create** → **New agent**.
3. Give it a name (e.g. _My FinOps Agent1_) and complete the setup wizard.
4. Once created, note the agent name — you'll use it in the next step.

### Step 4 — Clone Your Agent Locally via the VS Code Extension

1. In VS Code, open the **Copilot Studio** panel from the Activity Bar (left sidebar).
2. Click **Sign in** and authenticate with your Microsoft 365 account.
3. Select the **Environment** where you created the agent.
4. Find your agent in the list and click **Clone** (or **Open locally**) to pull it into a local folder on your machine.

### Step 5 — Copy the FinOps Agent Files into Your Local Agent Folder

From this repository, copy the following files and folders into your locally cloned agent folder, **replacing** any existing files with the same name:

```
FinOps Agent/
├── agent.mcs.yml        ← copy and replace
├── knowledge/           ← copy entire folder and replace
└── topics/              ← copy entire folder and replace
```

> Make any customizations you need at this point — edit `agent.mcs.yml` to adjust instructions, add/remove knowledge sources in `knowledge/`, or modify topics in `topics/`.

### Step 6 — Apply Changes via the Extension

1. Back in VS Code, open the **Copilot Studio** panel.
2. Click **Apply Changes** (or **Publish**) to push your local changes back to Copilot Studio.
3. Wait for the extension to confirm the changes were applied successfully.

### Step 7 — Test in Copilot Studio

1. Open [Copilot Studio](https://aka.ms/copilotstudio) and navigate to your agent.
2. Click **Test** in the top-right corner to open the test chat panel.
3. Start a conversation and validate the agent's responses.

---

## Try It Out

Once deployed, test it with prompts like:

- _"What is the best Azure savings plan for a predictable workload?"_
- _"How do I set up a budget alert in Azure Cost Management?"_
- _"What's the difference between Microsoft 365 E3 and E5 from a cost perspective?"_
- _"How is Microsoft Copilot Studio billed?"_
- _"How do I optimize Microsoft Fabric capacity costs?"_

---

## Knowledge Sources

The agent automatically searches these official Microsoft Learn docs:

| Source | URL |
|---|---|
| FinOps with Azure | https://learn.microsoft.com/azure/cost-management-billing/finops/ |
| Azure Cost Management + Billing | https://learn.microsoft.com/azure/cost-management-billing/ |
| Microsoft Fabric | https://learn.microsoft.com/fabric/ |
| Microsoft Foundry | https://learn.microsoft.com/azure/ai-foundry/ |
| Microsoft 365 | https://learn.microsoft.com/microsoft-365/ |
| Copilot for Microsoft 365 | https://learn.microsoft.com/copilot/microsoft-365/ |

---

## Customization Tips

| What to Change | Where |
|---|---|
| Agent instructions / persona | `agent.mcs.yml` → `instructions` |
| Knowledge sources | `knowledge/` — add or edit `.knowledge.mcs.yml` files |
| Conversation topics | `topics/` — add or edit `.mcs.yml` files |
| Auth & access control | `settings.mcs.yml` |
| Agent icon | Replace `icon.png` (512×512 PNG recommended) |

---

## Part of the Copilot Studio Samples Collection

This repo is part of a growing collection of **Microsoft Copilot Studio sample agents** — each in its own repository, ready to clone and deploy.

> **More samples coming soon.** Follow along to be notified when new agents drop.

---

## About the Author

Built by **Renato Romão** — 6x Microsoft MVP (Copilot Studio & Microsoft Foundry).

<p align="center">
  <a href="https://www.linkedin.com/in/renatoromao/">
    <img src="https://img.shields.io/badge/%F0%9F%91%A4%20Follow%20Renato%20Rom%C3%A3o%20on%20LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="Follow on LinkedIn" />
  </a>
</p>

---

## License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">
  Made with ❤️ for the Microsoft community
</p>


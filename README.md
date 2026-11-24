DukaanVoice

Your shop. Your language. Your AI operator, with you in control.

DukaanVoice is a voice-first AI assistant for kirana shops. It helps shopkeepers check inventory, view sales, prepare invoices, and update stock using Hindi, Hinglish, or English.

Instead of navigating multiple screens, shopkeepers can speak naturally. The AI uses Model Context Protocol (MCP) tools to access shop operations, while every important change goes through a preview and explicit approval.

«[!IMPORTANT]
This project is a prototype built with synthetic demo data. It is not a production billing, accounting, or payment system.»

---

✨ What it does

- 🎙️ Voice and text input in Hindi, Hinglish, and English
- 📦 Inventory lookup with stock and low-stock information
- 📊 Daily sales summary
- 🧾 Invoice drafting with server-calculated totals
- 🔄 Stock adjustment with preview and approval
- 🔐 Human approval before every write operation
- 🧾 Action receipts and audit history
- 👥 Owner and staff permission checks
- 🔁 Demo reset with seeded data

---

💡 How it works

flowchart LR
    A[Shopkeeper] --> B[Voice or Text]
    B --> C[Next.js Interface]
    C --> D[Agent API]
    D --> E[MCP Server]
    E --> F[Business Service]
    F --> G[Draft + Hash]
    G --> H[Approval]
    H --> I[Commit Action]
    I --> J[Database + Audit Receipt]

The model plans and communicates. The server validates and executes.

The AI never writes directly to the database.

---

🛠️ Tech Stack

Layer| Technology
Frontend| Next.js, TypeScript, Tailwind CSS
Voice Input| Browser Web Speech API
Voice Output| ElevenLabs TTS
AI Agent| Node.js, provider adapter, tool calling
MCP Server| Official TypeScript MCP SDK
Validation| Zod
Business Logic| Separate service layer
Database| SQLite with seeded demo data
Cloud| AWS Lambda, API Gateway
Frontend Hosting| Vercel
Testing| Vitest

<details>
<summary><strong>Why MCP?</strong></summary>MCP provides a standard, discoverable tool interface between the AI agent and shop operations.

The same tools can be reused by compatible AI clients without tying the business logic to a single interface.

The MCP server also keeps validation and safety rules outside the model.

</details>---

🔌 MCP Tools

DukaanVoice uses a small set of focused tools:

Tool| Purpose
"get_inventory"| Check available stock
"get_sales_summary"| Retrieve today's sales
"find_customer"| Find and disambiguate customers
"create_invoice_draft"| Prepare an invoice
"propose_stock_adjustment"| Preview a stock change
"commit_action"| Execute an approved action
"get_action_history"| View action receipts

<details>
<summary><strong>How a write operation is protected</strong></summary>1. The agent proposes an action.
2. The server creates a draft with the exact parameters.
3. A hash binds the draft to its contents.
4. The shopkeeper reviews and approves it.
5. The server validates the approval token.
6. Role checks and idempotency checks run.
7. The action is committed.
8. An audit receipt is generated.

If the draft changes after approval, the approval becomes invalid.

</details>---

🧱 Project Structure

DukaanVoice/
├── frontend/          # Next.js application
├── agent/             # AI agent and provider adapter
├── mcp-server/        # MCP tools and schemas
├── business-service/  # Business rules and write controls
├── data/              # Seeded demo data
├── tests/             # Critical safety tests
├── docs/              # Architecture and project notes
└── README.md

The structure above represents the intended separation of components; adjust it to match the final repository.

---

🚀 Getting Started

Prerequisites

- Node.js
- npm
- A modern browser with microphone support
- API credentials for the services enabled in your environment

Installation

git clone https://github.com/YOUR_USERNAME/DukaanVoice.git
cd DukaanVoice
npm install

Create your environment file:

cp .env.example .env

Add the required credentials locally. Never commit API keys or secrets.

Start the development server:

npm run dev

Run the tests:

npm test

«[!NOTE]
These commands assume the corresponding npm scripts are configured in the repository. Update them if the project uses separate frontend, agent, or MCP server packages.»

---

🛡️ Safety by Design

DukaanVoice is built around a simple rule:

Reads can happen immediately. Writes require explicit approval.

- No direct database access from the model
- Server-side stock and invoice calculations
- Draft-bound approval tokens
- Idempotency keys to prevent duplicate records
- Role-based permissions
- Clear error and cancellation paths
- Audit logs for completed actions
- No false success messages

---

🧪 Prototype Validation

Our demo focuses on proving the workflow reliably.

- [ ] Inventory lookup returns the correct seeded quantity
- [ ] Stock changes remain drafts until approval
- [ ] Unapproved writes are rejected
- [ ] Modified drafts invalidate approval
- [ ] Duplicate requests do not create duplicate records
- [ ] Ambiguous customer requests ask for clarification
- [ ] Failed operations show a clear error
- [ ] Successful writes generate audit receipts

---

🎯 Scope

Current prototype focus

Inventory, sales summaries, stock adjustments, invoice drafts, voice interaction, and safe action execution.

Not included

- Payments or bank access
- GST filing
- Real supplier messaging
- Real customer data
- Autonomous background transactions
- Full production POS replacement
- Support for every Indian language

---

🗺️ Roadmap

- [ ] Complete the core MCP read and write tools
- [ ] Finish the approval and audit workflow
- [ ] Add Hindi and Hinglish voice interaction
- [ ] Integrate ElevenLabs confirmations
- [ ] Complete safety and idempotency tests
- [ ] Deploy the demo with local fallback
- [ ] Validate the workflow with kirana shopkeepers
- [ ] Explore POS integrations and additional languages

---

🤝 Contributing

This project is being developed as part of wHACKiest 2026 — Track 01: Make MCP Matter.

Contributions, feedback, and ideas around MCP-based shop automation are welcome.

---

📌 Project Principle

DukaanVoice does not ask a shopkeeper to become a software expert.

It brings software closer to how the shopkeeper already works—and keeps the shopkeeper in control at every meaningful step.

---

Built by Team Pajamapops

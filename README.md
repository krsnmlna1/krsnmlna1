# Hi, I'm Krisna Maulana Rahman 👋

### Smart Contract Security Researcher | AI-Directed Builder

Auditing smart contracts through live contest platforms (Sherlock), with every finding backed by a working proof-of-concept. Alongside that, I direct AI-built tools end-to-end — specifying requirements and iterating with AI on the implementation, not hand-writing the code myself. Based in Indonesia 🇮🇩, open to remote work.

---

## 🔍 What I Do

**Smart Contract Auditing** — reviewing Solidity codebases through live audit contests, tracing fund flows and verifying every finding with a Foundry proof-of-concept before calling it a bug.

**AI-Directed Builds** — specifying requirements and directing AI on implementation for trading systems, on-chain dashboards, and automation tools.

---

## 🛡️ Security Audits

### NavBrick Finding — Sherlock Audit Contest (Tare)
Identified an int128 ledger-overflow vulnerability in a lending protocol's core valuation function, permanently freezing deposits and redemptions for all vault shareholders once triggered. Verified with a 5-test Foundry suite (5/5 passing). Submitted as a full Sherlock-format report — judging pending.

### Cap Labs Retrospective Audit
**[reproduce-practice](https://github.com/krsnmlna1/reproduce-practice)**

Independent retrospective audit of a fractional-reserve vault: balance verification relied on internal bookkeeping instead of actual on-chain token balance, letting the first redeemer succeed while blocking every subsequent one. Confirmed with a passing Foundry PoC and verified as a non-duplicate against the protocol's original disclosed findings.

**Stack:** Solidity · Foundry (forge/cast/anvil) · manual code review

---

## 🤖 AI-Directed Builds

### [Sentinel Trade Bot](https://github.com/krsnmlna1/sentinel-dashboard)
**AI-Directed Telegram Trading Bot**

Specified requirements and directed AI-driven implementation end-to-end, from concept to deployment.
- Liquidity-sniping and copy-trading command set, using Alchemy WebSocket for chain data
- AI-driven token analysis via Groq (Llama 3.1 70B)

**Tech:** TypeScript · Node.js · PostgreSQL · Prisma · Ethers.js · Telegram Bot API · Groq AI

### Sentinel Command Center
**AI-Directed On-Chain Intelligence Dashboard**

Specified and directed AI-built dashboard for on-chain monitoring — mempool activity and wallet-behavior analysis.
- Mempool monitoring via Alchemy WebSocket
- LLM-based wallet-activity classification experiments (OpenAI/DeepSeek)

**Tech:** Next.js · TypeScript · Ethers.js · OpenAI/DeepSeek APIs · Alchemy WSS · Recharts

---

## 🛠 Tech Stack

**Security & Auditing:** Solidity · Foundry (forge/cast/anvil/chisel) · Slither · manual code review · PoC development
**Blockchain:** Ethers.js · Web3.js · Hardhat · Alchemy · Uniswap V2/V3
**AI Direction:** Groq API · OpenAI API · DeepSeek · Claude API · LangChain
**Frontend:** Next.js · React · TypeScript · Tailwind CSS
**Backend:** Node.js · Express.js · Python · PostgreSQL · Prisma
**DevOps:** Docker · Git · Linux · WSL2

---

## 📫 Connect

- **Portfolio:** [krsnmlna.dev](https://krsnmlna.dev)
- **LinkedIn:** [Krisna Maulana](https://linkedin.com/in/krsnmlna)
- **Twitter/X:** [@krsnmlna_1](https://x.com/krsnmlna_1)
- **Sherlock:** [krsnmlna](https://audits.sherlock.xyz/watson/krsnmlna)
- **Email:** hi@krsnmlna.dev

---

*Open to smart contract audit opportunities and AI-directed build contracts.*

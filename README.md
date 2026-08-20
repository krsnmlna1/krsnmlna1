# Hi, I'm Krisna Maulana Rahman 👋

### Smart Contract Security Researcher

Building a public audit track record through contest platforms — Sherlock primarily, with Cantina in view — plus independent retrospectives against already-resolved scopes, worked blind before opening the published results. Every finding is backed by a proof-of-concept that has been run against the *patched* contract and shown to flip. Solidity/EVM and Cairo/Starknet. Based in Indonesia 🇮🇩, open to remote work.

**Writeups and PoCs:** [github.com/krsnmlna1/audit-portfolio](https://github.com/krsnmlna1/audit-portfolio)

---

## 🛡️ Security Work

### Tare — Sherlock Audit Contest *(judging pending)*
Private-credit / RWA lending on Avalanche C-Chain. A servicer can post ledger entries — every one of them obeying the rules the function actually enforces, because no magnitude cap exists — that drive the `int128` negation in `Loans.getLoanValues` to overflow. `updateNav` then reverts, and because `removeLoansFromNav`, `setLoans`, and `setCalculator` are all gated behind `_requireIdleNav()`, every vault lever locks at once: deposit and redemption approvals freeze for all shareholders.

Not a permanent brick — a balancing ledger entry clears it — but nothing caps or rate-limits re-triggering it immediately afterward, so the realistic impact is a repeatable freeze rather than a one-shot one. Verified with a 5-test Foundry suite (5/5 passing), submitted in Sherlock's report format.

### Opus / Shrine — Code4rena Retrospective *(Cairo, Starknet)*
**[→ writeup + PoC](https://github.com/krsnmlna1/audit-portfolio/tree/main/2024-01-opus)**

Blind retrospective against a resolved $100k scope, in a language I hadn't written before. Found a read-before-write ordering bug in `withdraw_helper`: it reads a trove's yang balance, calls `charge()` — which silently writes an updated balance to that same storage slot when a pending exceptional redistribution exists — then overwrites it with the value computed from the stale read. A 1-wei withdrawal destroys a redistribution increment larger than the entire position, and the same call advances the redistribution cursor, so it can never be re-pulled.

Converged on the same root cause and the same fix as C4 [#184](https://github.com/code-423n4/2024-01-opus-findings/issues/184) (judged satisfactory, duplicate of primary #206) — which the judge *upgraded* to High Risk from the QA/Gas tier its own submitter had filed it under.

**Stack:** Cairo · Scarb 2.4.0 · Starknet Foundry (`snforge`) 0.13.1, pinned via `asdf`

### Cap Labs — Sherlock Retrospective
**[→ writeup + PoC](https://github.com/krsnmlna1/audit-portfolio/tree/main/2025-07-cap)**

`Vault._verifyBalance()` checks bookkeeping (`totalSupplies - totalBorrows`) instead of the actual token balance. When the underlying yVault takes a loss, the bookkeeping figure never reflects it — the first redeemer drains real assets and everyone after them hits an insufficient-balance revert. PoC passing, confirmed non-duplicate against the contest's own published finding #409.

### AuditAgent vs. Claude Code — AI Audit Tooling Benchmark
**[→ full comparison](https://github.com/krsnmlna1/audit-portfolio/blob/main/ai-tool-comparison.md)**

Ran Nethermind's AuditAgent and a local Claude Code pass over that same Cap Labs scope, both benchmarked against my own confirmed finding. **Neither rediscovered it.** One candidate finding from the Claude Code pass looked solid — test green, PoC passing — until I found the assertion was catching the wrong revert, and traced a way a liquidator could self-heal the condition atomically for the cost of dust. Full cost/time breakdown, scope-confound caveats, and methodology notes are public.

### Damn Vulnerable DeFi v4.1.0
**[→ solutions](https://github.com/krsnmlna1/audit-portfolio/tree/main/dvd)** — 3 of 18, each with a root-cause writeup and a working exploit. A training set, listed as one: the vulnerabilities are given, so the exercise is explaining the mechanism precisely and building the exploit, not discovering that something is wrong.

---

## 🔬 How I Verify

Idea generation is cheap now — static analyzer, LLM, or a hunch while reading code. The part that doesn't automate is verification.

**The rule I hold myself to: a PoC isn't confirmed until it's been run against the patched contract and flipped.** A positive control proves the setup actually reaches the vulnerable state; a negative control proves nothing else moved. On Opus that meant 387 tests passing, exactly the 2 bug tests flipping, and nothing else in the suite budging.

I learned it by failing it. The first PoC I wrote for Opus reported a `FAIL` that proved nothing — the identical failure occurred against a *fixed* contract too. "It fails" isn't a result. "It fails here, passes there, and nothing else moved" is.

For recon I work archetype-first: map the folder structure to functional roles — vault, oracle, lending, fee, access — then prioritize whatever doesn't have a standard analogue.

---

## 🛠 Tech Stack

**Security & Auditing:** Solidity · Foundry (forge/cast/anvil/chisel) · Cairo · Starknet Foundry (`snforge`) · Scarb · Slither · manual code review · PoC development
**Chains:** EVM (Ethereum, Avalanche C-Chain, Base) · Starknet
**Blockchain:** Ethers.js · Hardhat · Alchemy · Uniswap V2/V3
**AI Tooling:** Claude API · OpenAI API · Groq · DeepSeek · LangChain
**Backend / DevOps:** Node.js · TypeScript · Python · PostgreSQL · Prisma · Docker · Git · Linux · WSL2

---

## 🤖 Before This — AI-Directed Builds

Not the pitch anymore, but it's where the AI-as-substrate habit came from: I specified requirements and directed AI on implementation end-to-end, rather than hand-writing the code.

- **[Sentinel Trade Bot](https://github.com/krsnmlna1/sentinel-dashboard)** — Telegram trading bot: liquidity-sniping and copy-trading commands over Alchemy WebSocket, with token analysis via Groq (Llama 3.1 70B). *TypeScript · Node.js · PostgreSQL · Prisma · Ethers.js*
- **Sentinel Command Center** — on-chain intelligence dashboard: mempool monitoring and LLM-based wallet-activity classification experiments. *Next.js · TypeScript · Ethers.js · Alchemy WSS · Recharts*
- **[solidity-ai-auditor](https://github.com/krsnmlna1/solidity-ai-auditor)** — early static-analysis + LLM audit prototype, which is what pulled me toward the security side in the first place.

---

## 📫 Connect

- **Portfolio:** [krsnmlna.dev](https://krsnmlna.dev)
- **LinkedIn:** [Krisna Maulana](https://linkedin.com/in/krsnmlna)
- **Twitter/X:** [@krsnmlna_1](https://x.com/krsnmlna_1)
- **Sherlock:** [krsnmlna](https://audits.sherlock.xyz/watson/krsnmlna)
- **Email:** hi@krsnmlna.dev

---

*Open to smart contract audit roles and contract work.*

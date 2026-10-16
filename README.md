# Hi, I'm Krisna Maulana Rahman 👋

### Backend & Automation Developer · Smart Contract Security Researcher

Information Technology undergraduate at Telkom University Surabaya. I build backend services and automation tooling in Python, and I direct AI coding tools on larger builds, which are labelled as AI-directed below. The stack I list as my own is the part I learned and can defend line by line: Python, FastAPI, PostgreSQL, SQL, and pytest. My background is smart contract security research, where a claim only counts once a test proves it. Based in Indonesia 🇮🇩, open to remote work.

---

## 🧰 Backend Work

### jobradar: job ingest API and collector
**[→ repo](https://github.com/krsnmlna1/jobradar)**

An HTTP ingest service on FastAPI and PostgreSQL 18, using psycopg 3 over an async connection pool with raw SQL rather than an ORM, so every endpoint maps to a statement that can be read directly.

- Ingestion is idempotent through a `UNIQUE (source, ext_id)` constraint with `ON CONFLICT DO NOTHING ... RETURNING id`; an empty result is the signal that separates a duplicate from a new insert.
- The health check performs a real database round trip instead of reporting healthy unconditionally.
- A collector pulls remote listings from a job board's search API in a single request and retries with exponential backoff on connection errors. It runs daily on a systemd timer.
- Tests run under pytest against a real PostgreSQL database rather than mocks, because the behaviour under test is the interaction with the database. The README ends with what is not covered yet.

**Stack:** Python · FastAPI · PostgreSQL 18 · psycopg 3 · raw SQL · pytest · uv · systemd

---

## 🛡️ Security Work

Writeups and PoCs: [github.com/krsnmlna1/audit-portfolio](https://github.com/krsnmlna1/audit-portfolio)

### Opus / Shrine: Code4rena retrospective *(Cairo, Starknet)*
**[→ writeup + PoC](https://github.com/krsnmlna1/audit-portfolio/tree/main/2024-01-opus)**

Blind retrospective against a resolved $100k scope, in a language I hadn't written before. Found a read-before-write ordering bug in `withdraw_helper`: it reads a trove's yang balance, then calls `charge()`, which silently writes an updated balance to that same storage slot when a pending exceptional redistribution exists, and finally overwrites it with the value computed from the stale read. A 1-wei withdrawal destroys a redistribution increment larger than the entire position, and the same call advances the redistribution cursor, so it can never be re-pulled.

Converged on the same root cause and the same fix as C4 [#184](https://github.com/code-423n4/2024-01-opus-findings/issues/184) (judged satisfactory, duplicate of primary #206), which the judge *upgraded* to High Risk from the QA/Gas tier its own submitter had filed it under.

**Stack:** Cairo · Scarb 2.4.0 · Starknet Foundry (`snforge`) 0.13.1, pinned via `asdf`

### Cap Labs: Sherlock retrospective
**[→ writeup + PoC](https://github.com/krsnmlna1/audit-portfolio/tree/main/2025-07-cap)**

`Vault._verifyBalance()` checks bookkeeping (`totalSupplies - totalBorrows`) instead of the actual token balance. When the underlying yVault takes a loss, the bookkeeping figure never reflects it, so the first redeemer drains real assets and everyone after them hits an insufficient-balance revert. PoC passing, confirmed non-duplicate against the contest's own published finding #409.

### AuditAgent vs. Claude Code: AI audit tooling benchmark
**[→ full comparison](https://github.com/krsnmlna1/audit-portfolio/blob/main/ai-tool-comparison.md)**

Ran Nethermind's AuditAgent and a local Claude Code pass over that same Cap Labs scope, both benchmarked against my own confirmed finding. **Neither rediscovered it.** One candidate finding from the Claude Code pass looked solid, with the test green and the PoC passing, until I found the assertion was catching the wrong revert and traced a way a liquidator could self-heal the condition atomically for the cost of dust. Full cost and time breakdown, scope-confound caveats, and methodology notes are public.

### Damn Vulnerable DeFi v4.1.0
**[→ solutions](https://github.com/krsnmlna1/audit-portfolio/tree/main/dvd)**

3 of 18, each with a root-cause writeup and a working exploit. Listed as a training set: the vulnerabilities are given, so the exercise is explaining the mechanism precisely and building the exploit, not discovering that something is wrong.

---

## 🔬 How I Verify

Idea generation is cheap now, whether it comes from a static analyzer, an LLM, or a hunch while reading code. The part that doesn't automate is verification.

**The rule I hold myself to: a test isn't confirmed until it has been run against the fixed version and flipped.** A positive control proves the setup actually reaches the broken state; a negative control proves nothing else moved. On Opus that meant 387 tests passing, exactly the 2 bug tests flipping, and nothing else in the suite budging.

I learned it by failing it. The first PoC I wrote for Opus reported a `FAIL` that proved nothing, because the identical failure occurred against a *fixed* contract too. "It fails" isn't a result. "It fails here, passes there, and nothing else moved" is.

The same habit applies to infrastructure. When I wanted to know whether my jobradar timer needed `Persistent=true`, I read the systemd documentation and then tested it: one timer through a suspend, then two timers side by side through a real shutdown. The setting stayed because the shutdown test showed what it does.

---

## 🛠 Tech Stack

**Backend & Testing:** Python · FastAPI · PostgreSQL · SQL · psycopg 3 · pytest · REST APIs · uv · Git · Linux · systemd
**Security & Auditing:** Solidity · Foundry (forge/cast/anvil/chisel) · Cairo · Starknet Foundry (`snforge`) · Scarb · Slither · manual code review · PoC development
**Chains:** EVM (Ethereum, Avalanche C-Chain, Base) · Starknet
**AI-directed builds:** Claude Code for implementation under my direction; TypeScript, Node.js, Prisma, Docker, and the Claude, OpenAI and Groq APIs appear in those builds, written by AI tooling rather than claimed as my own stack

---

## 🤖 AI-Directed Builds

I specify requirements and direct AI on implementation end to end rather than hand-writing the code. That is also where the habit of treating AI output as a claim to verify, not an answer to accept, came from.

- **[Sentinel Trade Bot](https://github.com/krsnmlna1/sentinel-dashboard)**: Telegram trading bot with liquidity-sniping and copy-trading commands over Alchemy WebSocket, and token analysis via Groq (Llama 3.1 70B). *TypeScript · Node.js · PostgreSQL · Prisma · Ethers.js*
- **Sentinel Command Center**: on-chain intelligence dashboard with mempool monitoring and LLM-based wallet-activity classification experiments. *Next.js · TypeScript · Ethers.js · Alchemy WSS · Recharts*
- **[solidity-ai-auditor](https://github.com/krsnmlna1/solidity-ai-auditor)**: early static-analysis + LLM audit prototype, which is what pulled me toward the security side in the first place.

---

## 📫 Connect

- **LinkedIn:** [Krisna Maulana](https://linkedin.com/in/krsnmlna)
- **Twitter/X:** [@krsnmlna_1](https://x.com/krsnmlna_1)
- **Sherlock:** [krsnmlna](https://audits.sherlock.xyz/watson/krsnmlna)

---

*Open to backend, automation, and QA automation roles at internship or entry level, to smart contract audit work, and to AI-directed build contracts.*

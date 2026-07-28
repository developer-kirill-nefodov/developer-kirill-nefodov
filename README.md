# Kirill Nefodov

[![Portfolio](https://img.shields.io/badge/Portfolio-1F6FEB?style=flat-square&logo=googlechrome&logoColor=white)](https://developer-kirill-nefodov.github.io/personal-portfolio/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kirill-nefodov-954747214/)
[![Email](https://img.shields.io/badge/Email-24292F?style=flat-square&logo=gmail&logoColor=white)](mailto:kirillnef58@gmail.com)
![Location](https://img.shields.io/badge/Romania%20(EU)%20%C2%B7%20Remote-24292F?style=flat-square)

I build AI pipelines over medical and regulated data — and the machinery that makes their output trustworthy.

Five years of commercial full-stack work, the last two on a patient-facing health platform: lab documents, EHR records from multiple US vendors and wearable telemetry reconciled into one patient timeline. Three input classes that arrive in different shapes, disagree with each other, use different identity keys and units, and can deliver the same record twice. Most of the engineering is in ingestion and reconciliation — and in what happens when a model, a vendor or a queue misbehaves.

## Focus

- **AI pipelines over regulated data** — validation of model output, quarantine paths, audit trails, human decision points
- **Integration-heavy backends** — EHR and third-party APIs, idempotent sync, conflict resolution, background jobs and queues
- **Production ownership** — from requirements through deployment to debugging live systems on real data

## How I work — five mechanisms from production

These are engineering decisions, not feature lists. Client work is under NDA, so no names, domains or business rules — only the approach.

**Bounded retries, and an explicit "giving up"**
One in-process queue routes each patient to the right importer by which external identity is present, processes a fixed batch concurrently, and drops a task after five failed attempts with an explicit log line rather than retrying forever. The queue is rebuilt from persisted in-progress records on boot, so a restart resumes instead of silently losing work. No external broker.

**Model output is an integration problem, not a prompt problem**
One wrapper handles chat and completion endpoints, function calling and image inputs; retries twice; strips code fences before parsing; and returns null instead of throwing when the payload isn't JSON. Every call's cost is computed from returned token usage against a per-model price table, and the inference provider is swappable per model without touching call sites.

**Never drop a value you don't understand**
Values the reference model doesn't recognise are quarantined with the date of the source document — not the date of the batch — enriched in the background, and surfaced for a human to approve or reject. An import never fails because of an unknown key.

**Identity before merge**
Sources that each claim their own key are resolved to one canonical identity, units are normalised, and only then does an idempotent merge write into the patient timeline. Re-delivering the same record changes nothing.

**Encrypt at the field, decrypt what you use**
Patient identifiers and names are stored encrypted with a salt held on the user record. Every queue task decrypts exactly the fields it needs and nothing else.

## Why this is worth naming now

From **2 August 2026** the EU AI Act requires high-risk systems — most clinical AI among them — to provide human oversight, accuracy and robustness, technical documentation, traceability and post-market monitoring. Around a quarter of hospitals report being ready. The properties above weren't built to satisfy a regulation; they were built because pipelines over medical data break without them. They happen to be the same list.

## Selected work

**Health data platform** · NDA client · 2024 – present
Multi-source ingestion and reconciliation into a patient health timeline, with the mechanisms described above. Core ingestion and reconciliation layer built together with one other engineer.
`Node.js (ESM)` `uWebSockets.js` `MongoDB` `React` `Recoil` `OpenAI-compatible APIs` `cloud document intelligence` `SSE`

**B2B commerce platform** · NDA client · 2022 – 2026
Multi-country B2B commerce system: pricing logic, ordering flows, supplier integration over synchronous XML exchange, admin workflows, and three and a half years of production maintenance on a live system.
`React` `Node.js` `MongoDB` `uWebSockets.js` `EDI/XML` `FTP` `SMTP`

**[QuantPilot](https://github.com/developer-kirill-nefodov/quant-pilot-ai)** · personal · open
Local research platform for crypto-futures strategies. Backtester and paper executor are the same engine; every result must survive out-of-sample, cross-coin and cross-year checks. 804 tests and 25 documented negative results.
Machine learning did not carry an edge here, and the repository says so with the numbers: four independent forms were tried and all failed the same way — a win/loss classifier at mean AUC 0.5902 against a 0.60 gate, order-flow features moving AUC inside the noise band, ML volatility sizing changing Sharpe by +0.004 across 5,264 trades, and an ML regime classifier that lost to the rule-based one. A stricter probe with a shuffled-label control confirmed it. The models came out rather than shipped, and the closed directions stayed documented.

**[Nfter](https://github.com/developer-kirill-nefodov/nfter)** · personal · open
Full-stack TypeScript Web3 dApp on Sepolia: account auth, SIWE wallet linking, in-contract generative ERC-721 NFTs, tips, an approval-based marketplace, referrals, and verifiable on-chain state. 171 tests.

**[Crypto Pulse Dashboard](https://github.com/developer-kirill-nefodov/crypto-pulse-dashboard)** · personal · open
Vue 3 dashboard streaming 400+ Binance USDT pairs over WebSocket, with candlestick and line charts and historical pagination.

Earlier commercial work: a Next.js / GraphQL / DatoCMS platform generating 500+ pages from reusable content blocks, a Shopify storefront application, and internal reporting tooling.

More detail — including architecture diagrams for the NDA projects — is in my portfolio.

## Stack

![Node.js](https://img.shields.io/badge/Node.js-24292F?style=flat-square&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-24292F?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-24292F?style=flat-square&logo=react&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-24292F?style=flat-square&logo=mongodb&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-24292F?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-24292F?style=flat-square&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-24292F?style=flat-square&logo=docker&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-24292F?style=flat-square&logo=openai&logoColor=white)

Also: Fastify, Express, uWebSockets.js, in-process queues, WebSocket and SSE, Web Workers, GraphQL, Next.js, Vue 3.

## Links

- [Portfolio](https://developer-kirill-nefodov.github.io/personal-portfolio/)
- [LinkedIn](https://www.linkedin.com/in/kirill-nefodov-954747214/)
- Email: `kirillnef58@gmail.com`

Open to remote roles as an AI, Full-Stack or Backend Engineer.

```markdown
# nedu-rails

Passkey-first stablecoin rails for rural economies (pilot: Nedumudy, Kerala)

Subtitle: Passkey-first stablecoin rails for rural economies (pilot: Nedumudy, Kerala)

GOAL
Build an end-to-end system that lets villagers pay local shops using a fiat-pegged community stablecoin, with passkey login and a transparent community treasury.

This repository is a monorepo scaffold (MVP) including:
- Solidity smart contracts (Foundry)
- Next.js web dapp with passkey-first auth (WebAuthn) + gasless UX
- Node relayer (ERC-2771 minimal forwarder)
- TypeScript SDK for dapp integration
- CI (lint/test/typecheck), docs, and demo scripts

Quick links:
- /contracts — Foundry smart contracts and tests
- /apps/web — Next.js dapp
- /apps/relayer — Node/Express gasless relayer
- /packages/sdk — TypeScript SDK & deployed address mapping
- /docs — architecture, threat model, accessibility, roadmap

High-level MVP scope
- ERC20 stablecoin Nedu Rupee (NEDU) — 6 decimals, pausable, role-based (MINTER, BURNER, PAUSER), fee-in-bps for Treasury
- CommunityTreasury.sol — receives fee income and supports multisig-controlled disbursements with public events
- MerchantRegistry.sol — register and approve merchants
- CommunityMultisig.sol — simple N-of-M multisig (Gnosis Safe compatibility is future work)
- Forwarder (MinimalForwarder) — on-chain primitive for ERC-2771 gasless
- ReserveOracle.sol — mock attested reserve to display coverage ratio
- Web: passkey-first login (WebAuthn) for application session; gasless transactions routed through relayer

Quickstart (local dev/demo)
1) Prereqs
   - Node >=18, pnpm, Foundry (forge)
   - Optional: Docker for running anvil (or use anvil from Foundry)

2) Clone & bootstrap
   - git clone <repo-url>
   - cd nedu-rails
   - pnpm install (root workspace installs for apps and packages)

3) Start a local chain
   - forge anvil (or `pnpm --filter contracts start` if you add a script)
   - Deploy contracts via Foundry script:
     - cd contracts
     - forge script script/Deploy.s.sol --broadcast --rpc-url http://localhost:8545 -vv

   The deploy script will output addresses and write them to /packages/sdk/addresses.json for dapp & relayer.

4) Start relayer
   - cd apps/relayer
   - cp .env.example .env and set RPC_URL, FORWARDER_ADDRESS, RELAYER_PRIVATE_KEY
   - pnpm start

5) Start dapp
   - cd apps/web
   - cp .env.example .env and set RPC_URL, CHAIN_ID, FORWARDER_ADDRESS, TOKEN_ADDRESS, ...
   - pnpm dev
   - Open http://localhost:3000 — register a demo passkey, try Send, Pay Merchant, Top-up (mock)

Demo flows (for README demos)
1) Admin mints NEDU to “Village Reserve” EOA and a few demo users.
2) Register 3 demo merchants via web /seed script.
3) User pays merchant; fee goes to Treasury; Dashboard shows updated Treasury and Coverage Ratio.
4) Multisig disburses funds to “School Roof Repair” with reference; appears on /community timeline.

Acceptance criteria
- Contracts deploy & pass tests.
- Web app shows balances, coverage ratio, merchants; can send payments via relayer in dev.
- README lets a newcomer run the demo in ~30 minutes.

Files in this scaffold include comments and TODOs. Please open issues for missing features, enhancements, or UI polish. See /GOOD_FIRST_ISSUES.md for recommended starter tasks.
```

```markdown
Architecture Overview

Contracts:
- NeduToken (ERC20 + Pausable + AccessControl) -> collects fee on transfers and forwards to CommunityTreasury
- CommunityTreasury -> receives fees, emits events for transparency, supports multisig disbursements
- MerchantRegistry -> on-chain merchant verification
- CommunityMultisig -> lightweight N-of-M multisig for admin actions
- ReserveOracle -> attested_reserve, settable by multisig

Off-chain:
- Relayer: accepts signed meta-transactions, submits to forwarder
- Web: passkey-first session authentication; gasless transactions through relayer

Data flow:
User (web session) -> constructs meta-tx -> relayer -> forwarder -> NeduToken transfer -> fee to CommunityTreasury -> events recorded

Security & threats:
See /docs/threat-model.md
```

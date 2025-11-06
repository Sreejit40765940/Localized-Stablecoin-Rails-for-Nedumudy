```markdown
Threat model (MVP)

Major risks:
- Fee skimming by malicious contract/address: mitigated by AccessControl, event logs, and allowing fee-exempt toggles only by multisig.
- Registry spoofing: merchant records are on-chain and only admin can approve; UI shows registry-sourced names and hashes.
- Relayer abuse: relayer allowlist & rate-limiting; forwarder verifies meta-tx signatures.
- Oracle manipulation: ReserveOracle is settable only by multisig for MVP and clearly labeled as mock.

Further mitigations for production:
- External audits, timelocks for big multisig spends, more stringent oracle attestations, use Gnosis Safe or multisig service.
```

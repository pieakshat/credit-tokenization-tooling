# 11 Testing and security

Property suites and verification tooling for vault and token code.

---

### a16z erc4626-tests

- **Link:** https://github.com/a16z/erc4626-tests
- **Summary:** Foundry property-based tests for ERC-4626 conformance, usable for fuzzing or symbolic execution. Properties cover round-trip behavior (no free profit from deposit and withdraw), balance and allowance updates, preview over- and under-estimation, caller-independent conversions, and non-reverting view functions. Implementation-specific behavior such as yield generation is not tested.
- **Type:** test suite
- **Layer:** testing
- **Chains:** EVM
- **License:** AGPL-3.0
- **Last checked:** 2026-11-12
- **Use when:** a synchronous ERC-4626 vault needs a conformance check.
- **Notes:** AGPL-3.0 terms apply to code that incorporates the suite. Last updated in July 2025.

---

### crytic/properties (ERC-4626)

- **Link:** https://github.com/crytic/properties/tree/main/contracts/ERC4626
- **Summary:** Echidna property tests for ERC-4626 vaults, grouped as must-not-revert, functional accounting, redeem-using-approval, sender-independent, rounding and security properties. A vault can optionally expose internal test methods through `IERC4626Internal` to enable properties that cannot be tested externally.
- **Type:** test suite
- **Layer:** testing
- **Chains:** EVM
- **License:** AGPL-3.0
- **Last checked:** 2026-11-12
- **Use when:** a vault is fuzzed with Echidna and standard invariants are wanted without writing them.
- **Notes:** AGPL-3.0 terms apply, as above.

---

### Recon erc7540-reusable-properties

- **Link:** https://github.com/Recon-Fuzz/erc7540-reusable-properties
- **Summary:** Seven reusable invariants for ERC-7540 vaults (7540-1 to 7540-7), written in collaboration with Centrifuge. They cover the share and asset price relationship, `max*` functions never reverting, over-claiming reverting, `requestRedeem` reverting on insufficient balance, and `preview*` always reverting. Installed as a Foundry dependency and inherited from an `ERC7540Properties` contract.
- **Type:** test suite
- **Layer:** testing, vault
- **Chains:** EVM
- **License:** none stated in the repository
- **Last checked:** 2026-11-12
- **Use when:** fuzzing the request and claim state machine of an ERC-7540 vault.
- **Notes:** Without a license, default copyright applies. Permission from the authors is needed before reuse.

---

### Certora Prover

- **Link:** https://github.com/Certora/CertoraProver
- **Summary:** A formal verification tool that checks user-written rules against smart contract bytecode. The repository documents building the tool locally; hosted use is documented at docs.certora.com.
- **Type:** framework
- **Layer:** testing
- **Chains:** EVM
- **License:** GPL-3.0
- **Last checked:** 2026-11-12
- **Use when:** key accounting properties, such as shares never exceeding backing assets, need to be proven and not only fuzzed.
- **Notes:** A proof covers only the rules written. Specifications from production protocols can be read in the `certora/` directories of [Morpho Vault V2](https://github.com/morpho-org/vault-v2/tree/main/certora) and [Centrifuge](https://github.com/centrifuge/protocol-certora).

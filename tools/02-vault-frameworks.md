# 02 Vault frameworks

Code for the deposit and redemption layer. Standards are listed in [01](01-token-standards.md).

Several entries below are GPL or custom-licensed. Reading the code for design reference is unrestricted; reusing it depends on the license, which each entry links.

---

### OpenZeppelin ERC4626

- **Link:** https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/extensions/ERC4626.sol
- **Summary:** Base implementation of ERC-4626 with a configurable decimals offset that mitigates share-price inflation attacks. The documentation covers that attack and common customizations such as fees.
- **Type:** contracts
- **Layer:** vault
- **Chains:** EVM
- **License:** MIT
- **Audit:** reports for the library are published in the repository: https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/audits
- **Last checked:** 2026-11-12
- **Use when:** a synchronous vault is needed on a library with published audits.
- **Notes:** Synchronous only. Asynchronous flows (ERC-7540) are not included.

---

### ERC-7540 Reference Implementations

- **Link:** https://github.com/ERC4626-Alliance/ERC-7540-Reference
- **Summary:** Four example vaults for ERC-7540: controlled async deposit, controlled async redeem, fully async (both), and timelocked async redeem with a three-day delay and an exchange rate fixed at request time.
- **Type:** contracts
- **Layer:** vault, redemption
- **Chains:** EVM
- **License:** MIT
- **Last checked:** 2026-11-12
- **Use when:** studying the request lifecycle, or as a starting point for an asynchronous vault.
- **Notes:** The repository states the code is unaudited. Last updated in August 2024.

---

### Centrifuge Vault Development Kit

- **Link:** https://github.com/centrifuge/protocol/tree/vdk/src/vaults (branch `vdk`)
- **Summary:** One configurable vault contract with an instant lane (ERC-4626) and an asynchronous lane (ERC-7540), plus ERC-7575 multi-asset shares. Product behavior comes from plugin contracts fixed at deployment: request policy, instant policy, liquidity route, oracle and settlement observer. The same bytecode is intended to cover tokenized treasuries, private credit, fund of funds and tranched credit.
- **Type:** framework
- **Layer:** vault, redemption, token
- **Chains:** EVM, with a hub-and-spoke design for cross-chain pools
- **License:** [Business Source License 1.1](https://github.com/centrifuge/protocol/blob/vdk/LICENSE) with a change license of GPL-3.0-or-later. Non-production use is permitted; production use requires the Additional Use Grant published at license.centrifuge.io, or a commercial license.
- **Last checked:** 2026-11-12
- **Use when:** studying a complete design for credit and fund products. The `ARCHITECTURE.md` and `SPECIFICATION.md` in the vaults directory describe the guarantees and non-guarantees, with the tests behind each.
- **Notes:** Development branch; the structure may change. Configuration is fixed at construction and no upgrade path exists, so a change ships as a new vault. Production reuse is restricted by the license.

---

### Morpho Vault V2

- **Link:** https://github.com/morpho-org/vault-v2
- **Summary:** Non-custodial, immutable vaults that allocate deposits into underlying markets through adapters. Roles (owner, curator, allocators) manage allocation within id-based absolute and relative caps, and curator configuration changes are timelockable.
- **Type:** contracts
- **Layer:** vault
- **Chains:** EVM
- **License:** GPL-2.0, with a separate [`LICENSE-MIT`](https://github.com/morpho-org/vault-v2/blob/main/LICENSE-MIT) file in the repository
- **Audit:** reports are published in the repository: https://github.com/morpho-org/vault-v2/tree/main/audits
- **Last checked:** 2026-11-12
- **Use when:** studying curated allocation with caps and timelocks, or planning integration with Morpho markets (see [13](13-defi-composability.md)).
- **Notes:** A lending-allocation vault, not an RWA issuance framework. The repository includes Certora specifications.

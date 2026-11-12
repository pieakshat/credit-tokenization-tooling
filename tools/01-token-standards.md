# 01 Token standards

Specifications that share and tranche tokens implement. Tooling in later categories builds on one or more of these. Specification text on EIP pages is licensed CC0.

---

### ERC-3643: T-REX, Token for Regulated EXchanges

- **Link:** https://eips.ethereum.org/EIPS/eip-3643
- **Summary:** A permissioned token standard in which every transfer is validated against an onchain identity registry and a compliance contract. It defines interfaces for the token, identity registry, identity registry storage, compliance, trusted issuers registry and claim topics registry.
- **Type:** spec
- **Layer:** token, compliance
- **Chains:** EVM
- **License:** CC0
- **Status:** Final
- **Last checked:** 2026-11-12
- **Use when:** investors must be verified and transfers restricted by investor type or jurisdiction.
- **Notes:** The standard presumes an onchain identity and claims model. The KYC provider and legal structure need to be compatible with it. A reference implementation is listed in [03](03-compliance-and-identity.md).

---

### ERC-4626: Tokenized Vaults

- **Link:** https://eips.ethereum.org/EIPS/eip-4626
- **Summary:** A standard API for vaults that issue shares representing a claim on a single underlying ERC-20 asset, with deposit, mint, withdraw and redeem functions.
- **Type:** spec
- **Layer:** vault
- **Chains:** EVM
- **License:** CC0
- **Status:** Final
- **Last checked:** 2026-11-12
- **Use when:** deposits and redemptions settle within a single transaction, for example a fund that keeps an instant-liquidity buffer.
- **Notes:** Redemptions that depend on loan repayments cannot settle within a single transaction; ERC-7540 covers that case. Vaults are exposed to share-price manipulation, so conformance and invariant testing are covered in [11](11-testing-and-security.md).

---

### ERC-7540: Asynchronous ERC-4626 Tokenized Vaults

- **Link:** https://eips.ethereum.org/EIPS/eip-7540
- **Summary:** Extends ERC-4626 with request-based deposit and redemption. A request is submitted, later becomes claimable, and is then executed through the existing ERC-4626 functions. Implementations may make deposits, redemptions or both asynchronous.
- **Type:** spec
- **Layer:** vault, redemption
- **Chains:** EVM
- **License:** CC0
- **Status:** Final
- **Last checked:** 2026-11-12
- **Use when:** settlement depends on loan repayments, NAV publication or manager approval, as in private credit pools that fund redemptions from repayments.
- **Notes:** The request lifecycle is a state machine whose transitions need dedicated testing. Property suites for it are listed in [11](11-testing-and-security.md).

---

### ERC-7575: Multi-Asset ERC-4626 Vaults

- **Link:** https://eips.ethereum.org/EIPS/eip-7575
- **Summary:** Allows several vaults or entry points to share one share token by externalizing the share token from the vault. It adds a `share` method on the vault, a vault lookup on the share token, and mandatory ERC-165 support.
- **Type:** spec
- **Layer:** vault, token
- **Chains:** EVM
- **License:** CC0
- **Status:** Final
- **Last checked:** 2026-11-12
- **Use when:** investors subscribe in more than one currency or stablecoin into the same fund share class.
- **Notes:** NAV and accounting must stay consistent across every vault that feeds the shared token.

---

### ERC-7887: Cancelation for ERC-7540 Tokenized Vaults

- **Link:** https://eips.ethereum.org/EIPS/eip-7887
- **Summary:** Extends ERC-7540 with asynchronous cancelation of pending deposit and redeem requests, including a way to view the cancelation status and claim the returned assets or shares.
- **Type:** spec
- **Layer:** vault, redemption
- **Chains:** EVM
- **License:** CC0
- **Status:** Draft
- **Last checked:** 2026-11-12
- **Use when:** investors need to withdraw an unsettled request before the next settlement window.
- **Notes:** Draft status; the interface may change.

---

### ERC-8161: Transferable Tokenized Vault Requests

- **Link:** https://eips.ethereum.org/EIPS/eip-8161
- **Summary:** Extends ERC-7540 with optional transfer of pending deposit and redeem requests from one controller to another. Two separate interfaces are defined, and implementations may support either or both.
- **Type:** spec
- **Layer:** vault, redemption
- **Chains:** EVM
- **License:** CC0
- **Status:** Final
- **Last checked:** 2026-11-12
- **Use when:** unsettled positions need to move between wallets, for example on wallet migration.
- **Notes:** Transfers of requests interact with transfer restrictions. A request must not reach an address that would be barred from holding the shares.

---

### ERC-7741: Authorize Operator

- **Link:** https://eips.ethereum.org/EIPS/eip-7741
- **Summary:** Defines EIP-712 signed messages for granting and revoking operator permissions on contracts that implement an operator model, enabling meta-transactions and atomic interactions.
- **Type:** spec
- **Layer:** vault
- **Chains:** EVM
- **License:** CC0
- **Status:** Draft
- **Last checked:** 2026-11-12
- **Use when:** a custodian, router or manager acts for an investor without a separate approval transaction.
- **Notes:** Draft status. The scope of actions an operator may perform is set by the implementing contract.

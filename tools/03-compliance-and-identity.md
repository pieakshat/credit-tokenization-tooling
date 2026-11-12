# 03 Compliance and identity

Tooling that decides who may hold, receive and redeem a token: identity registries, compliance rules, freezes and forced transfers.

---

### ERC-3643 reference implementation (T-REX)

- **Link:** https://github.com/ERC-3643/ERC-3643
- **Summary:** Solidity contracts implementing the ERC-3643 standard: security token, identity registry, trusted issuers registry, claim topics registry and compliance contract, built around ONCHAINID identities. The `contracts/` directory is organized into `token`, `registry`, `compliance`, `roles`, `factory` and `proxy`.
- **Type:** contracts
- **Layer:** compliance, token
- **Chains:** EVM
- **License:** GPL-3.0
- **Last checked:** 2026-11-12
- **Use when:** an implementation of the ERC-3643 standard is needed, or compatibility with it is required.
- **Notes:** GPL-3.0 is a copyleft license. Derived code generally has to be released under the same terms, which constrains projects using other licenses. Hardhat project, published on npm as `@erc3643org/erc-3643`.

---

### Centrifuge transfer hooks

- **Link:** https://github.com/centrifuge/protocol/tree/vdk/src/token/hooks (branch `vdk`)
- **Summary:** Per-share-token hooks that restrict transfers and vault actions. `ShareTokenHook` keeps a memberlist with a valid-until timestamp and a freeze flag for each account, and ships four presets: `FreezeOnly`, `RedemptionRestrictions`, `FullRestrictions` and `FreelyTransferable`. Each preset sets which of five roles (entry, transfer, exit, burn, payout) require membership.
- **Type:** contracts
- **Layer:** compliance, token
- **Chains:** EVM
- **License:** [Business Source License 1.1](https://github.com/centrifuge/protocol/blob/vdk/LICENSE) with a change license of GPL-3.0-or-later; production use is subject to the Additional Use Grant at license.centrifuge.io
- **Last checked:** 2026-11-12
- **Use when:** studying transfer restrictions expressed as swappable policies, with separate rules for entering, holding and exiting a pool.
- **Notes:** Development branch. The hooks are designed to work with the Centrifuge vault and share token and are not a standalone library.

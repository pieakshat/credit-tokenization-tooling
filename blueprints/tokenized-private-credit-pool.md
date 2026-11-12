# Blueprint: tokenized private credit pool

**Status:** draft. Only tools with an entry in [`tools/`](../tools/) are recommended. Layers without a cataloged tool are marked as not yet cataloged.

## Scenario

An issuer lends to businesses off-chain through an SPV. Verified investors subscribe to the pool with stablecoins and receive shares. Redemptions are paid from loan repayments on a schedule and not on demand.

## Choices by layer

| Layer | Choice | Rationale | Catalog |
|---|---|---|---|
| Share token | ERC-20 with transfer restrictions, following the ERC-3643 model or policy-based hooks | Only verified investors may hold shares | [01](../tools/01-token-standards.md), [03](../tools/03-compliance-and-identity.md) |
| Deposit and redemption | ERC-7540 asynchronous vault | Redemptions depend on repayments and NAV publication, so they cannot settle in one transaction | [01](../tools/01-token-standards.md), [02](../tools/02-vault-frameworks.md) |
| Request cancelation and transfer | ERC-7887 (Draft) and ERC-8161, optional | Allows an unsettled request to be canceled or moved to another wallet | [01](../tools/01-token-standards.md) |
| Compliance | Identity registry or role-based hooks | Defines who may hold, receive and redeem | [03](../tools/03-compliance-and-identity.md) |
| Pool accounting | Not yet cataloged | Interest accrual, defaults and fees | [04](../tools/04-pool-accounting-and-waterfalls.md) |
| NAV | Not yet cataloged | Requires a trusted publisher and freshness limits | [05](../tools/05-nav-and-oracles.md) |
| Redemption design | Not yet cataloged; the Centrifuge Vault Development Kit shows one approach | Epochs, notice periods and gates | [06](../tools/06-redemptions-and-liquidity.md), [02](../tools/02-vault-frameworks.md) |
| Testing | ERC-4626 and ERC-7540 property suites, plus formal verification of core accounting | The request and claim state machine needs dedicated invariant testing | [11](../tools/11-testing-and-security.md) |

## Design decisions

1. **Synchronous, asynchronous or both.** Products whose redemptions are funded by loan repayments need asynchronous redemption. Some add an instant lane backed by a cash buffer, as the Centrifuge Vault Development Kit does.
2. **NAV publication.** The publisher, and the controls that prevent a stale or incorrect value, are the principal trust assumption of the design.
3. **Issuer powers.** Freezes, forced transfers and pausing should be defined explicitly and visible onchain.
4. **Licensing.** Reference codebases are GPL, AGPL or custom-licensed (see [02](../tools/02-vault-frameworks.md), [03](../tools/03-compliance-and-identity.md) and [11](../tools/11-testing-and-security.md)). Whether code is reused or only studied needs to be decided before implementation begins.
5. **Upgrade policy.** Immutable contracts with new deployments for changes, or upgradeable contracts behind timelocks.

# Spend permissions

Delegation with Light Token works similar to SPL. When you approve a delegate, you authorize a specific account to transfer tokens on your behalf:

- **Owner retains custody**: You still own the tokens and can transfer or revoke at any time. Delegation is non-custodial.
- **Capped spending**: The delegate can spend tokens up to the limit, but cannot access or drain the account beyond the approved amount.
- **Single delegate per account**: Each token account can only have one active delegate. The owner can revoke at any time.
- **New approval replaces old**: Approving a new delegate automatically revokes the previous one.

## Use cases

| Use case | How delegation helps |
|:---------|:--------------------|
| **Subscriptions** | Approve a monthly cap. The service provider transfers the fee each period. |
| **Recurring payments** | Approve a spending limit. The payment processor draws funds as needed. |
| **Managed spending** | A parent or admin approves a cap for a sub-account. |
| **Agent wallets** | An AI agent operates within a delegated spending limit. |

## Approve a delegate

Grant a delegate permission to spend up to a capped amount:

```typescript
import { approveInterface } from "@lightprotocol/compressed-token/unified";

const tx = await approveInterface(
  rpc,
  payer,
  senderAta,
  mint,
  delegate.publicKey,     // who gets permission
  500_000,                // amount cap
  owner                   // token owner (signs)
);

console.log("Approved:", tx);
```

## Check delegation status

```typescript
import { getAtaInterface } from "@lightprotocol/compressed-token";

const account = await getAtaInterface(rpc, senderAta, owner.publicKey, mint);

console.log("Delegate:", account.parsed.delegate?.toBase58() ?? "none");
console.log("Delegated amount:", account.parsed.delegatedAmount.toString());
```

## Revoke a delegate

Remove spending permission:

```typescript
import { revokeInterface } from "@lightprotocol/compressed-token/unified";

const tx = await revokeInterface(rpc, payer, senderAta, mint, owner);

console.log("Revoked:", tx);
```

## Examples

| File | Description | Key function |
|:-----|:------------|:-------------|
| [delegate-approve.ts](https://github.com/Lightprotocol/examples-light-token/blob/main/toolkits/payments/spend-permissions/delegate-approve.ts) | Let a delegate spend tokens on your behalf. | `approveInterface` |
| [delegate-revoke.ts](https://github.com/Lightprotocol/examples-light-token/blob/main/toolkits/payments/spend-permissions/delegate-revoke.ts) | Revoke delegate access. | `revokeInterface` |
| [delegate-check.ts](https://github.com/Lightprotocol/examples-light-token/blob/main/toolkits/payments/spend-permissions/delegate-check.ts) | Check current delegation status and remaining allowance. | `getAtaInterface` |
| [delegate-full-flow.ts](https://github.com/Lightprotocol/examples-light-token/blob/main/toolkits/payments/spend-permissions/delegate-full-flow.ts) | Approve, check, and revoke in one script. | `approveInterface`, `revokeInterface`, `getAtaInterface` |

## Source

- [Spend permissions docs](https://zkcompression.com/light-token/payments/spend-permissions)
- [GitHub examples](https://github.com/Lightprotocol/examples-light-token/tree/main/toolkits/payments/spend-permissions)

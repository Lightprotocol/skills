# Verify address

Check whether a recipient has an associated token account before sending.

```typescript
import {
  getAssociatedTokenAddressInterface,
  getAtaInterface,
} from "@lightprotocol/compressed-token";

const ata = getAssociatedTokenAddressInterface(mint, recipient);

try {
  const account = await getAtaInterface(rpc, ata, recipient, mint);
  console.log("Account exists, balance:", account.parsed.amount);
} catch {
  console.log("Account does not exist yet — will be created on first transfer");
}
```

## Examples

| File | Description | Key function |
|:-----|:------------|:-------------|
| [verify-address.ts](https://github.com/Lightprotocol/examples-light-token/blob/main/toolkits/payments/verify/verify-address.ts) | Check if ATA exists for a recipient. | `getAtaInterface` |

## Source

- [Verify payments docs](https://zkcompression.com/light-token/payments/accept-payments/verify-payments)
- [GitHub example](https://github.com/Lightprotocol/examples-light-token/blob/main/toolkits/payments/verify/verify-address.ts)

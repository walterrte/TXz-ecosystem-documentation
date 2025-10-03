# Integration Guides

## Adding TXZ to Your DApp

**Step 1: Install Dependencies**

```bash
npm install @solana/web3.js @solana/spl-token
```

**Step 2: Import TXZ Token**

```javascript
import { PublicKey } from '@solana/web3.js';
import { TOKEN_PROGRAM_ID } from '@solana/spl-token';

const TXZ_MINT = new PublicKey('TXZ_TOKEN_ADDRESS_HERE');
```

**Step 3: Check User Balance**

```javascript
async function getTXZBalance(walletAddress) {
  const tokenAccounts = await connection.getParsedTokenAccountsByOwner(
    new PublicKey(walletAddress),
    { mint: TXZ_MINT }
  );

  if (tokenAccounts.value.length === 0) return 0;

  const balance = tokenAccounts.value[0].account.data.parsed.info.tokenAmount.uiAmount;
  return balance;
}
```

**Step 4: Apply Discount Logic**

```javascript
const MIN_TXZ_FOR_DISCOUNT = 10000;

async function calculateFee(amount, walletAddress) {
  const txzBalance = await getTXZBalance(walletAddress);

  const baseFee = amount * 0.05; // 5%
  const discountedFee = amount * 0.03; // 3%

  return txzBalance >= MIN_TXZ_FOR_DISCOUNT ? discountedFee : baseFee;
}
```

## Adding TXZ to Wallets

**Token Metadata:**
```json
{
  "name": "TXZ Token",
  "symbol": "TXZ",
  "decimals": 9,
  "logo": "https://txz-dev.fun/assets/logo.png",
  "mint": "TXZ_TOKEN_ADDRESS_HERE"
}
```

**Phantom Wallet:** Automatically detects SPL tokens
**Solflare:** Add custom token with mint address
**Backpack:** Import using token address

---

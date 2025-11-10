# Wallet Integration (RainbowKit + wagmi)

### Wallet Integration (RainbowKit + wagmi)

Wrap your app:

```jsx
import { WalletProvider } from 'rootstockwinks';

export default function App({ Component, pageProps }) {
  return (
    <WalletProvider>
      <Component {...pageProps} />
    </WalletProvider>
  );
}
```

Use the connection UI:

```jsx
import { WalletConnection } from 'rootstockwinks';

function MyComponent() {
  return <WalletConnection showBalance showNetwork />;
}
```

Advanced hook:

```jsx
import { useWalletIntegration } from 'rootstockwinks';

const {
  walletState,
  connectWallet,
  disconnectWallet,
  switchToRootstockMainnet,
  switchToRootstockTestnet,
  requestTransactionSignature,
  requestMessageSignature,
  requestPersonalSignature,
  requestTypedDataSignature,
  sendTransaction,
} = useWalletIntegration();
```

* `sendTransaction(to, value)` now powers the example app’s “Send tRBTC” flow and sends native tRBTC on Rootstock Testnet.

Send native tRBTC:

```ts
const result = await sendTransaction('0xRecipient', '0.05');
if (result.success) {
  console.log('tx hash', result.txHash);
} else {
  console.error(result.error);
}
```

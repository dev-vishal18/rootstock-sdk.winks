# Signature Manager

### Signature Manager&#x20;

```ts
import { SignatureManager, Eip1193Provider } from 'rootstockwinks';

const sm = new SignatureManager(new Eip1193Provider(window.ethereum));

await sm.requestTransactionSignature({ to: '0x...', value: 0n });
await sm.requestMessageSignature('Hello Rootstock');
await sm.requestPersonalSignature('Personal message');
await sm.requestTypedDataSignature({ domain, types, value });
```

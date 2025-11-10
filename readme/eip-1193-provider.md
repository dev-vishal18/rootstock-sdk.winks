# EIP-1193 Provider

### EIP-1193 Provider Adapter

```ts
import { Eip1193Provider } from 'rootstockwinks';

const eip = new Eip1193Provider(window.ethereum);
await eip.request({ method: 'eth_requestAccounts' });
```

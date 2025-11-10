# RPC Management

### RPC Manager

```ts
import { RpcManager } from 'rootstockwinks';

const rpc = new RpcManager();
const provider = rpc.createProvider('mainnet'); // or 'testnet'
const bestUrl = rpc.getBestRpcUrl('mainnet');
// Health snapshot
const health = rpc.getHealth('mainnet');
```

* Periodic health checks (eth\_blockNumber) with timeouts
* Chooses lowest-latency healthy endpoint; fails over automatically

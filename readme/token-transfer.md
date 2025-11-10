# Token Transfer

### Enhanced Token Transfer Hook

```tsx
import { useEnhancedTokenTransfer } from 'rootstockwinks';

const {
  transferERC20,
  transferNFT,
  approveToken,
  getTokenBalance,
  getNFTOwner,
  getTokenAllowance,
  ensureRootstockNetwork,
  address,
  isConnected,
} = useEnhancedTokenTransfer();
```

* Use this hook for ERC-20/ERC-721/ERC-1155 contracts. For native tRBTC, prefer `useWalletIntegration().sendTransaction`.

### Simple Token/NFT Functions

```ts
import {
  transferERC20,
  approveToken,
  getTokenBalance,
  getTokenAllowance,
  getNFTOwner,
  transferNFT,
} from 'rootstockwinks';
import { ethers } from 'ethers';

const provider = new ethers.BrowserProvider(window.ethereum);
const signer = await provider.getSigner();

await transferERC20('0xToken', '0xRecipient', '1.0', signer);
await approveToken('0xToken', '0xSpender', '100.0', signer);
const bal = await getTokenBalance('0xToken', '0xAccount', provider);
const allowance = await getTokenAllowance('0xToken', '0xOwner', '0xSpender', provider);
const owner = await getNFTOwner('0xNft', '123', provider);
await transferNFT('0xNft', '0xFrom', '0xTo', '123', signer);
```

# Winks SDK (rootstock)

A React/Next.js SDK for building on Rootstock with wallet integration, token/NFT utilities, signature management, and RPC Management

## Features

* 🚀 Easy Integration: drop-in `Winks` wrapper for Next.js
* 🔑 API-keyed metadata management (server included)
* 📱 Social meta: Open Graph, Twitter Cards
* 🎯 Full SEO meta coverage
* 💰 Token utilities: ERC-20 transfer/approve/balance/allowance
* 🎨 NFT utilities: ERC-721 owner, ERC-721/1155 transfers, ERC-1155 balance
* 🔗 Rootstock ready (Testnet 31) — SDK defaults to Testnet in the example app
* 🌐 Wallet integration via RainbowKit + WalletConnect (styles auto-injected)
* ✍️ Signature management (tx/message/personal/typed data)
* 🔄 Network switching helpers
* 🧭 RPC Management with health checks and latency-based selection
* 🧩 EIP-1193 Provider adapter
* 🧯 Signature queueing to avoid overlapping prompts
* 🛠️ Dual builds (Rollup + Vite) outputting CJS + ESM
* ✅ Testing setup (Jest unit, Playwright E2E)

## Installation

```bash
npm install rootstockwinks
```

## Quick Start (Next.js)

```jsx
// pages/_app.js or app/layout.js
import { Winks } from 'rootstockwinks';

export default function App({ Component, pageProps }) {
  return (
    <Winks apikey="YOUR_API_KEY">
      <Component {...pageProps} />
    </Winks>
  );
}
```

Create an API key:

```bash
# Create API Key
curl -X POST http://winksserver.winks.fun/api/keys \
  -H "Content-Type: application/json" \
  -d '{"name": "My Website"}'

# Set metadata
curl -X POST http://winksserver.winks.fun/api/meta/YOUR_API_KEY \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_API_KEY" \
  -d '{
    "title": "My Awesome Website",
    "description": "The best website ever created",
    "ogTitle": "My Awesome Website",
    "ogDescription": "The best website ever created",
    "ogImage": "https://example.com/og-image.jpg",
    "ogUrl": "https://example.com",
    "twitterCard": "summary_large_image",
    "twitterTitle": "My Awesome Website",
    "twitterDescription": "The best website ever created",
    "twitterImage": "https://example.com/twitter-image.jpg",
    "canonical": "https://example.com",
    "robots": "index, follow",
    "viewport": "width=device-width, initial-scale=1",
    "charset": "utf-8",
    "author": "Your Name"
  }'
```

### WalletConnect project ID (RainbowKit)

RainbowKit requires a WalletConnect project ID. Set it in your app (for the example app, create `example/.env.local`):

```bash
NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID=YOUR_PROJECT_ID
```

### Winks Component

Props:

* `apikey: string` required
* `children: ReactNode` required
* `fallback?: MetaData` (used if server fetch fails)

`MetaData` shape:

```ts
interface MetaData {
  title?: string;
  description?: string;
  keywords?: string;
  ogTitle?: string;
  ogDescription?: string;
  ogImage?: string;
  ogUrl?: string;
  twitterCard?: string;
  twitterTitle?: string;
  twitterDescription?: string;
  twitterImage?: string;
  canonical?: string;
  robots?: string;
  viewport?: string;
  charset?: string;
  author?: string;
}
```



### Network Configuration

* Rootstock Mainnet: Chain ID 30, RPC `https://public-node.rsk.co`, Explorer `https://explorer.rootstock.io`, Currency RBTC
* Rootstock Testnet: Chain ID 31, RPC `https://public-node.testnet.rsk.co`, Explorer `https://explorer.testnet.rootstock.io`, Currency tRBTC

## Server API&#x20;

* `GET /health`
* `POST /api/keys` → `{ id, key, name, createdAt, isActive }`
* `GET /api/keys` (auth)
* `DELETE /api/keys/:key` (auth)
* `GET /api/meta/:apiKey` → returns `MetaData`
* `POST /api/meta/:apiKey` (auth) `{ metadata: MetaData }`
* `PUT /api/meta/:apiKey` (auth) `{ metadata: MetaData }`
* `DELETE /api/meta/:apiKey` (auth)

Auth header: `X-API-Key: {apiKey}`

## Development

### Build

```bash
npm run build           # TypeScript + Rollup (CJS + ESM)
npm run build:vite      # Vite library build (optional)
```

### Testing

```bash
npm test                # Jest unit tests
npx playwright install chromium
npm run test:e2e        # Playwright (ensure example app is running or use a prod build)
```

## License

MIT

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add some amazing feature'`
4. Push: `git push origin feature/amazing-feature`
5. Open a Pull Request

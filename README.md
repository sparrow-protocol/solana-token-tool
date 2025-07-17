## 🕊️ Sparrow Protocol Token Toolkit

A CLI + utility suite to mint, register, and interact with **SPL Token-2022 tokens** and NFTs—built for Solana developers. Supports metadata uploads to IPFS, Jupiter token registration (API + manual fallback), Token-2022 minting, Solana Blinks, and AI agent endpoints.

> Used to mint, upload, and register `TSPRW` tokens and NFTs for the Sparrow Protocol.

---

### 🚀 Features

* ✅ **Token-2022** minting with transfer-fee and close-authority support
* 🖼️ Uploads NFT metadata and logos to **IPFS**
* 🌍 Registers tokens on **Jupiter Aggregator** (API or GitHub PR format)
* 🤖 Adds **AI agent endpoints** for smart LLM integration
* ⚡ Generates Solana **Blink** links via Solana Actions
* 🔐 CLI wrapper for easy scripting & automation

---

## 📦 Installation

```bash
git clone https://github.com/sparrow-protocol/token-toolkit
cd token-toolkit
npm install
```

Requires:

* `ts-node`, `tsx`, or build via `tsc`
* Solana CLI (`solana-keygen`, `solana config`)

---

## 🛠️ How It Works

Sparrow's toolkit wraps common on-chain workflows into a TypeScript CLI:

### 1. 🪙 Minting Token-2022 NFTs

Creates a new mint with 0 decimals, sends to an associated token account, and uploads metadata to IPFS.

### 2. 🖼️ IPFS Upload

Uploads a logo or metadata JSON to a remote IPFS node (e.g., Infura, Pinata), returns a permanent CID-based URI.

### 3. 🧾 Jupiter Token Registration

Attempts to register the token with Jupiter via API. If the endpoint is unavailable, it generates a `jupiter-token.json` file ready for a PR to [jup-ag/token-list](https://github.com/jup-ag/token-list).

### 4. 🤖 AI Agent Endpoint

Exposes a `/api/ai` endpoint compatible with Solana Actions or custom LLM agents. Supports TSPRW ownership checks, token transfers, and more.

### 5. 🔗 Blink Link Generation

With `solana-actions`, generate links like:

```
https://solana.com/blink?url=https://your-app.vercel.app/api/transfer&icon=https://ipfs.io/ipfs/<CID>&title=Transfer+NFT
```

---

## 🧪 Example Usage

### ✅ Upload NFT Metadata

```bash
tsx bin/sparrow.ts upload-metadata \
  --file metadata/tsprw.json \
  --keypair keypair/authority.json
```

### ✅ Mint a TSPRW NFT

```bash
tsx bin/sparrow.ts mint-nft \
  --keypair keypair/authority.json \
  --metadata metadata/tsprw.json \
  --mint-keypair keypair/mint.json \
  --network devnet
```

### ✅ Register on Jupiter (manual fallback)

```bash
tsx bin/sparrow.ts register-jupiter \
  --mint <MINT_ADDRESS> \
  --symbol TSPRW-NFT \
  --name "Sparrow NFT" \
  --decimals 0 \
  --logo-uri https://ipfs.io/ipfs/<CID> \
  --is-nft \
  --tags "nft,solana"
```

If the API fails, check `jupiter-token.json` and submit a PR to:
👉 [https://github.com/jup-ag/token-list](https://github.com/jup-ag/token-list)

---

## 📁 Project Structure

```bash
.
├── bin/
│   └── sparrow.ts          # CLI entry point
├── utils/
│   ├── mintToken.ts        # Token-2022 mint logic
│   ├── uploadIPFS.ts       # Uploads metadata/images to IPFS
│   ├── registerOnJupiter.ts# Token registration with Jupiter
├── metadata/
│   └── tsprw.json          # NFT metadata file
├── keypair/
│   └── authority.json      # Keypair for mint authority
├── api/
│   ├── transfer.ts         # Transfer handler (Blink-compatible)
│   └── ai.ts               # AI-agent endpoint
├── .env                    # Environment variables
└── README.md
```

---

## ⚙️ .env Configuration

```bash
MINT_ADDRESS=YourTokenMintAddress
AUTHORITY_SECRET_KEY=[1,23,...]
KEYPAIR_PATH=keypair/authority.json
NETWORK=devnet
IMAGE_URI=https://ipfs.io/ipfs/<CID>
```

---

## 🔐 Security Notes

* Never commit your `keypair/*.json` or `.env` file to version control
* Add `.gitignore`:

```bash
keypair/
.env
```

---

## 💡 Contributing

PRs welcome! Submit ideas, bugfixes, or improvements.

* Want to add Token-2022 confidential transfers?
* Looking to support Metaplex NFT standards fully?
* Need DAO governance support via SPL Governance?

Open an issue or start a discussion.

---

## 📣 License

MIT © Sparrow Protocol — fly safe 🕊️

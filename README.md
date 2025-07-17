## 🕊️ Sparrow Protocol Token Toolkit

A CLI + utility suite to mint, register, and interact with **SPL Token-2022 tokens** and NFTs—built for Solana developers. Supports metadata uploads to IPFS, Jupiter token registration (API + manual fallback), Token-2022 minting, Solana Blinks, and AI agent endpoints.

> Used to mint, upload, and register `SPRW` tokens and NFTs for the Sparrow Protocol.

---

### 🚀 Features

* ✅ **Token-2022** minting with transfer-fee and close-authority support
* 🖼️ Uploads NFT and SPL token metadata + logos to **IPFS/Arweave**
* 🌍 Registers tokens on **Jupiter Aggregator** (API or GitHub PR format)
* 🤖 Adds **AI agent endpoints** for smart LLM integration (Dialect, Solana Actions)
* ⚡ Generates Solana **Blink** links for token interactions
* 🔐 CLI wrapper for easy scripting & automation

#### 🧪 In Progress / Coming Soon

* 🔒 Token-2022 **Confidential Transfers**
* 🎨 Metaplex-compliant NFT metadata
* 🗳 DAO Voting integration with **SPL Governance**
* 🧠 Advanced AI agent support (e.g., Dialect, LLMs)

---

## 📦 Installation

```bash
git clone https://github.com/sparrow-protocol/token-toolkit
cd token-toolkit
pnpm install
```

Requires:

* `ts-node`, `tsx`, or build via `tsc`
* Solana CLI (`solana-keygen`, `solana config`)

---

## 🛠️ How It Works

Sparrow's toolkit wraps common on-chain workflows into a TypeScript CLI:

### 1. 🪙 Minting Token-2022 SPL Tokens or NFTs

Creates a new mint (fungible or non-fungible) with optional metadata and authority config.

### 2. 🖼️ IPFS/Arweave Upload

Uploads a logo or metadata JSON to a remote node (Infura, Pinata, or Arweave), returns a permanent CID/transaction URI.

### 3. 🧾 Jupiter Token Registration

Attempts to register the token with Jupiter via API. If the endpoint is unavailable, generates a `jupiter-token.json` file for a manual PR.

### 4. 🤖 AI Agent Endpoint

Exposes a `/api/ai` endpoint compatible with Solana Actions or custom LLMs. Supports token ownership queries, transfers, and AI-agent intent resolution.

### 5. 🔗 Blink Link Generation

With `solana-actions`, generate links like:

```
https://solana.com/blink?url=https://blinks.sparrowprotocol.com/api/transfer&icon=https://arweave.net/<CID>&title=Transfer+SPRW
```

---

## 🧪 Example Usage

### ✅ Upload Token Metadata

```bash
tsx bin/sparrow.ts upload-metadata \
  --file metadata/sprw.json \
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

### ✅ Register an SPL Token (e.g. SPRW)

```bash
tsx bin/sparrow.ts register-jupiter \
  --mint <MINT_ADDRESS> \
  --symbol SPRW \
  --name "Sparrow" \
  --decimals 6 \
  --logo-uri https://arweave.net/<CID> \
  --tags "governance,staking,defi,solana"
```

### ✅ Register an NFT

```bash
tsx bin/sparrow.ts register-jupiter \
  --mint <MINT_ADDRESS> \
  --symbol SPRW-NFT \
  --name "Sparrow NFT" \
  --decimals 0 \
  --logo-uri https://ipfs.io/ipfs/<CID> \
  --is-nft \
  --tags "nft,solana"
```

---

## 📁 Project Structure

```bash
.
├── bin/
│   └── sparrow.ts          # CLI entry point
├── utils/
│   ├── mintToken.ts        # Token-2022 mint logic
│   ├── uploadIPFS.ts       # Uploads metadata/images
│   ├── registerOnJupiter.ts# Token registration logic
├── metadata/
│   └── sprw.json           # SPL token metadata file
├── keypair/
│   └── authority.json      # Mint authority wallet
├── api/
│   ├── transfer.ts         # Transfer (Blink-compatible)
│   └── ai.ts               # AI-agent route
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
IMAGE_URI=https://arweave.net/<CID>
```

---

## 🔐 Security Notes

* Never commit your `keypair/*.json` or `.env` to git
* Add `.gitignore`:

```bash
keypair/
.env
```

---

## 💡 Contributing

PRs welcome! Submit ideas, fixes, or enhancements.

Looking for help on:

* 🔒 Token-2022 confidential transfer support
* 🎨 Metaplex NFT metadata builder
* 🗳 SPL Governance integration
* 🧠 AI-agent intent-to-action bridge (Dialect or LLMs)

---

## 📣 License

MIT © Sparrow Protocol — fly safe 🕊️

## 🕊️ Sparrow Protocol Token Toolkit

A CLI + utility suite to mint, register, and interact with **SPL Token-2022 tokens** and NFTs—built for Solana developers. Supports metadata uploads to IPFS, Jupiter token registration (API + manual fallback), Token-2022 minting, Solana Blinks, and AI agent endpoints.

> Used to mint, upload, and register `TSPRW` tokens and NFTs for the Sparrow Protocol.

---

### 🚀 Features

* ✅ **Token-2022** minting (NFTs and SPL tokens)
* 🖼️ Uploads metadata and logos to **IPFS**
* 🌍 Registers tokens on **Jupiter Aggregator** (API or GitHub PR fallback)
* 🤖 Adds **AI agent endpoints** for smart LLM interaction
* ⚡ Generates **Solana Blink** links via Solana Actions
* 🔐 CLI wrapper for scripting and automation

---

## 📦 Installation

```bash
git clone https://github.com/sparrow-protocol/token-toolkit
cd token-toolkit
npm install
````

Requires:

* Node.js with `ts-node` or `tsx`
* Solana CLI (`solana-keygen`, `solana config set`)

---

## 🛠️ How It Works

Sparrow's toolkit wraps common on-chain workflows into a TypeScript CLI:

### 1. 🪙 Mint Token-2022

Create an SPL token (e.g., 6–9 decimals) or NFT (0 decimals), send it to an associated token account, and attach metadata via IPFS.

### 2. 🖼️ IPFS Upload

Upload logos or metadata JSON to Infura, Pinata, or another IPFS node—returns a CID-based permanent URL.

### 3. 🧾 Jupiter Token Registration

Registers tokens with Jupiter Aggregator:

* Uses API when available
* Falls back to JSON file for manual PR to [jup-ag/token-list](https://github.com/jup-ag/token-list)

### 4. 🤖 AI Agent Endpoint

Provides `/api/ai` for agents to query token ownership, trigger transfers, and generate action links.

### 5. 🔗 Blink Link Generator

Generate transaction links for wallets or actions like:

```
https://solana.com/blink?url=https://your-vercel-app.vercel.app/api/transfer&icon=https://ipfs.io/ipfs/<CID>&title=Transfer+TSPRW
```

---

## 🧪 Example Usage

### ✅ Upload Metadata to IPFS

```bash
tsx bin/sparrow.ts upload-metadata \
  --file metadata/tsprw.json \
  --keypair keypair/authority.json
```

### ✅ Mint a TSPRW NFT (0 decimals)

```bash
tsx bin/sparrow.ts mint-nft \
  --keypair keypair/authority.json \
  --metadata metadata/tsprw.json \
  --mint-keypair keypair/mint.json \
  --network devnet
```

### ✅ Register NFT on Jupiter (fallback)

```bash
tsx bin/sparrow.ts register-jupiter \
  --mint <NFT_MINT_ADDRESS> \
  --symbol TSPRW-NFT \
  --name "Sparrow NFT" \
  --decimals 0 \
  --logo-uri https://ipfs.io/ipfs/<CID> \
  --is-nft \
  --tags "nft,solana"
```

### ✅ Register SPL Token on Jupiter (e.g., 6 decimals)

```bash
tsx bin/sparrow.ts register-jupiter \
  --mint <SPL_TOKEN_MINT> \
  --symbol TSPRW \
  --name "Sparrow Token" \
  --decimals 6 \
  --logo-uri https://ipfs.io/ipfs/<CID> \
  --tags "utility,solana"
```

If the Jupiter API fails, check the generated `jupiter-token.json` and submit a PR here:
👉 [https://github.com/jup-ag/token-list](https://github.com/jup-ag/token-list)

---

## 📁 Project Structure

```
.
├── bin/
│   └── sparrow.ts              # CLI entry point
├── utils/
│   ├── mintToken.ts            # Token-2022 mint logic
│   ├── uploadIPFS.ts           # Uploads metadata/images to IPFS
│   └── registerOnJupiter.ts    # Jupiter registration logic
├── metadata/
│   └── tsprw.json              # NFT/SPL metadata
├── keypair/
│   └── authority.json          # Authority keypair
├── api/
│   ├── transfer.ts             # Blink-compatible token transfer handler
│   └── ai.ts                   # AI-agent endpoint for token queries
├── .env                        # Local environment config
└── README.md
```

---

## ⚙️ .env Configuration

```bash
MINT_ADDRESS=YourTokenMintAddress
AUTHORITY_SECRET_KEY=[1,2,3,...]
KEYPAIR_PATH=keypair/authority.json
NETWORK=devnet
IMAGE_URI=https://ipfs.io/ipfs/<CID>
```

---

## 🔐 Security Notes

* **Do not commit** your `.env` or `keypair/*.json` to git!
* Add to `.gitignore`:

```
keypair/
.env
```

---

## 💡 Contributing

PRs welcome! Features you could contribute:

* 🔒 Token-2022 Confidential Transfers
* 🎨 Metaplex-compliant NFT metadata
* 🗳 DAO Voting integration with SPL Governance
* 🧠 Advanced AI agent support (Dialect, LLMs)

Open an issue or start a discussion anytime.

---

## 📣 License

MIT © Sparrow Protocol — fly safe 🕊️

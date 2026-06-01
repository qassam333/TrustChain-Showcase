# TrustChain

<p align="center">
  <img src="./assets/logo.png" alt="TrustChain Logo" width="200" />
</p>

> **Decentralized Academic Certificate Verification System**

TrustChain is a blockchain-based platform that allows universities to issue tamper-proof academic certificates on the Polygon blockchain, enabling instant and public verification by employers, students, and other institutions.

This repository is a **showcase** of the TrustChain project, containing architectural overviews, smart contracts, and code snippets demonstrating the core logic of the system. (The full application source code remains private).

---

## 🌟 Key Features

| Role | Capabilities |
|------|-------------|
| **Admin** | Approves/rejects university registration requests, manages access, views system-wide statistics |
| **University** | Issues and revokes certificates on-chain via an encrypted, in-browser wallet. (No private keys touch the backend!) |
| **Public** | Instantly verifies any certificate by uploading the PDF or scanning its printed QR code |

**Verification Outcomes:** `VALID` · `REVOKED` · `FAKE`

---

## 🛠 Tech Stack & Project Scope

The system is built on a modern, fully asynchronous stack and is designed for scale:

### Frontend
- **Framework:** React 18, Vite, React Router v6
- **Styling:** Tailwind-inspired Vanilla CSS with a full Light/Dark Theme system
- **Web3 Integration:** `ethers.js` v6 for client-side wallet generation and contract signing
- **State Management:** React Context API (Auth, Theme, Wallet)
- **Data Visualization:** Recharts for admin statistics

### Backend
- **Framework:** FastAPI (Python)
- **Database:** Motor (Async MongoDB)
- **Scale:** 
  - **25 API Endpoints** across **5 Routers** (Auth, Universities, Certificates, Verify, Activities)
  - Full CRUD operations with role-based JWT middleware
  - **4 Pytest files** structured for comprehensive testing
- **Storage:** IPFS (via Pinata) for decentralized PDF storage
- **Security:** AES-256-GCM (Encryption at rest), SHA-256 (Hashing), JWT Authentication

### Blockchain
- **Network:** Polygon Amoy Testnet
- **Smart Contract:** Solidity `^0.8.19`

---

## 🔒 Security & Architecture

TrustChain is designed with a zero-trust model for wallet management:
- **Client-Side Wallets:** University wallets are generated in the browser. The private key is encrypted using `scrypt` and AES-128-CTR into a Keystore V3 JSON file stored in `localStorage`. 
- **Backend Blindness:** The backend *never* sees the private key. It only funds the public address and confirms transaction receipts.
- **Data Privacy:** PDFs uploaded to IPFS are symmetrically encrypted with AES-256-GCM before upload. The resulting IPFS CID is *also* encrypted before being embedded in the QR code. Only the TrustChain backend can decrypt the QR code to find the file.
- **Immutability:** Certificate hashes are anchored to the Polygon blockchain.

[**➡️ Read the full Architecture Deep Dive**](./ARCHITECTURE.md)

---

## 📂 Repository Structure

```
TrustChain-Showcase/
├── ARCHITECTURE.md           # Detailed system flows and diagrams
├── contracts/
│   └── TrustChain.sol        # The core smart contract deployed on Polygon
└── code_snippets/            # Clean, sanitized excerpts of complex logic
    ├── backend_encryption.py # AES-256-GCM encryption service
    ├── backend_hashing.py    # PDF fingerprinting service
    └── frontend_wallet.jsx   # ethers.js keystore decryption and state
```

---

## 🎓 The Team

- **Backend Development:** Alqasam & Moabed
- **Frontend Development:** Frontend Team
- **Year:** 2026

*TrustChain — Graduation Project 2026*

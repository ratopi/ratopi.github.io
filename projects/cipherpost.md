---
title: CipherPost
description: End-to-end encrypted messaging as a Progressive Web App
layout: page
---

End-to-end encrypted messaging as a Progressive Web App, built with Elm and Erlang/OTP.

CipherPost is a zero-knowledge messaging system. All encryption and decryption happens in the browser using [OpenPGP.js](https://openpgpjs.org/) (RFC 9580). The backend — an Erlang/OTP server with Cowboy — stores only encrypted blobs and never sees plaintext messages.

### How it works

1. Each participant generates an OpenPGP keypair in their browser
2. Public keys are published to the backend
3. The sender encrypts a message with all recipients' public keys, signs it with their own private key, and sends the encrypted blob to the server
4. Recipients poll for new messages and decrypt them client-side

The backend is intentionally simple: it stores encrypted messages with a timestamp and serves public keys. Nothing more.

### Architecture

| Component | Technology |
|-----------|-----------|
| Frontend | [Elm](https://elm-lang.org/) PWA |
| Backend | [Erlang/OTP](https://www.erlang.org/) with [Cowboy](https://ninenines.eu/) |
| Crypto | [OpenPGP.js](https://openpgpjs.org/) (RFC 9580) — loaded as ESM module |

No npm or Node.js required. The frontend compiles to JavaScript via Elm, and OpenPGP.js is loaded directly from CDN.

### API

| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/keys` | List all public keys |
| GET | `/api/keys/:fingerprint` | Get a specific public key |
| POST | `/api/keys` | Register a public key |
| POST | `/api/messages` | Store an encrypted message |
| GET | `/api/messages/:fingerprint?since=ISO8601` | Fetch messages for a recipient |

### License

AGPL-3.0-or-later — if you run a modified version as a network service, you must make your source code available to users.

Source code on [GitHub](https://github.com/ratopi/cipherpost).


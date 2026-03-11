---
title: "CipherPost – end-to-end encrypted messaging"
layout: blog_post
abstract: A zero-knowledge messaging PWA built with Elm and Erlang — all encryption happens in the browser.
author: Ralf Th. Pietsch
date: 2026-03-11
category: project
---

Just started working on [CipherPost](/projects/cipherpost) — an end-to-end encrypted messaging system that runs as a Progressive Web App.

The idea is simple: the server should know nothing. All encryption and decryption happens in the browser using [OpenPGP.js](https://openpgpjs.org/) (RFC 9580). Each participant generates a keypair locally, publishes the public key, and from that point on, messages are encrypted client-side before they ever leave the browser. The backend — written in Erlang/OTP with Cowboy — stores only encrypted blobs with timestamps. It has no way to read what people are writing.

The frontend is built in [Elm](https://elm-lang.org/), which feels like a natural fit: a language that makes impossible states impossible, combined with cryptography that makes plaintext leaks impossible on the server side.

No npm, no Node.js. OpenPGP.js is loaded directly as an ESM module from CDN.

This is still early — but the core flow works: key generation, key exchange, encrypted message sending, polling, decryption, and signature verification.

Source code on [GitHub](https://github.com/ratopi/cipherpost).


---
title: Eliza.elm
description: An ELIZA-inspired chatbot in Elm
layout: page
---

An ELIZA-inspired chatbot implemented as a standalone, serverless web application using Elm.

Inspired by Joseph Weizenbaum's classic 1966 ELIZA program, this implementation extends the original concept with fuzzy keyword matching, intelligent clause limiting, response repetition avoidance, and a modern chat UI.

### Features

- **ELIZA-inspired conversation engine** – keyword-weighted pattern matching and response generation, inspired by the original Weizenbaum algorithm
- **Fuzzy keyword matching** – tolerates common typos (edit distance ≤ 1)
- **Intelligent wildcard capture** – limits captured text to the first meaningful clause, preventing nonsensical reflections in multi-sentence input
- **Response repetition avoidance** – tracks the last 8 responses to avoid repeating itself
- **Multi-language support** – English and German out of the box, easily extensible
- **Personalized sessions** – users enter their name and select a language before chatting; Eliza addresses them by name
- **Serverless** – runs entirely in the browser, no backend required

Try it out: [Eliza.elm](https://ratopi.github.io/eliza.elm/)

Source code on [GitHub](https://github.com/ratopi/eliza.elm).


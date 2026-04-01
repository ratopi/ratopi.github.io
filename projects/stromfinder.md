---
title: Stromfinder
description: Interactive map of all charging stations in Germany
layout: page
---

An interactive map showing all registered charging stations in Germany, built with Elm and Leaflet.

The data comes from the [Ladesäulenregister](/projects/ladesaeule) project, which converts the official CSV from the [Bundesnetzagentur](https://www.bundesnetzagentur.de/DE/Fachthemen/ElektrizitaetundGas/E-Mobilitaet/start.html) into a gzip-compressed JSON file. Stromfinder loads this data in the browser, decompresses it with [pako](https://github.com/nodeca/pako), and visualizes ~70,000 charging stations on an OpenStreetMap map. The data is updated weekly automatically.

### Features

- **Marker clustering** – ~70,000 stations rendered efficiently on OpenStreetMap
- **Detail view** – address, charging points, plug types, power ratings, opening hours
- **Color coding** – fast chargers (orange) vs. normal chargers (green)
- **Responsive** – works on desktop and mobile
- **Progressive Web App** – installable on phone and desktop, works offline after first load

### Tech stack

The UI is written in [Elm](https://elm-lang.org/). Map integration (Leaflet) and data loading/decompression (pako) are handled via Elm Ports in JavaScript.

| Component | Library |
|-----------|---------|
| UI / State | [Elm](https://elm-lang.org/) 0.19 |
| Map | [Leaflet](https://leafletjs.com/) 1.9 |
| Tiles | [OpenStreetMap](https://www.openstreetmap.org/) |
| Clustering | [Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster) |
| Decompression | [pako](https://github.com/nodeca/pako) (gzip in the browser) |

### How it works

The Elm application manages the UI state and JSON decoding. Communication with the Leaflet map and the pako decompression library happens through Elm Ports – a clean boundary between the pure Elm world and JavaScript side effects. A Service Worker provides offline caching so the app works without a network connection after the first load.

### Building

The project includes a `build.sh` script that compiles Elm to optimized JavaScript. For local development, a Docker setup is provided that builds everything (Elm compilation + pandoc rendering) in a container – no local Elm installation required:

```
cd docker
docker compose up --build
```

On every push to `main`, a GitHub Action compiles Elm, renders the about page with pandoc, generates a version file, and deploys the `public/` directory to GitHub Pages.

### Data note

The raw data (~80 MB uncompressed, ~5–10 MB gzip) is loaded from `ratopi.github.io/ladesaeule/`. The first load may take a few seconds depending on connection speed.

Try it out: **[ratopi.github.io/stromfinder](https://ratopi.github.io/stromfinder/)**

Source code on [GitHub](https://github.com/ratopi/stromfinder). Licensed under Apache License 2.0.


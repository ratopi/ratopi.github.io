---
title: Stromfinder
description: Interactive map of all charging stations in Germany
layout: page
---

An interactive map showing all registered charging stations in Germany, built with Elm and Leaflet.

The data comes from the [Ladesäulenregister](/projects/ladesaeule) project, which converts the official CSV from the Bundesnetzagentur into a gzip-compressed JSON file. Stromfinder loads this data and visualizes ~70,000 charging stations on an OpenStreetMap map.

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


Try it out: [ratopi.github.io/stromfinder](https://ratopi.github.io/stromfinder/)

Source code on [GitHub](https://github.com/ratopi/stromfinder).


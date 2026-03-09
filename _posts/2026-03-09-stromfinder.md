---
title: "Stromfinder – interactive map of German charging stations"
layout: blog_post
abstract: An interactive map visualizing ~70,000 charging stations in Germany using Elm and Leaflet.
author: Ralf Th. Pietsch
date: 2026-03-09
category: project
---

Just published [Stromfinder](/projects/stromfinder) – an interactive map showing all registered charging stations in Germany.

The data comes from my [Ladesäulenregister](/projects/ladesaeule) project, which converts the official CSV from the Bundesnetzagentur into a gzip-compressed JSON file. Stromfinder loads this ~80 MB dataset in the browser using [pako](https://github.com/nodeca/pako) for decompression and renders ~70,000 stations on an OpenStreetMap map with marker clustering.

Fast chargers and normal chargers are color-coded (orange vs. green). Clicking a marker shows details like address, plug types, power ratings, and opening hours.

The UI is written in [Elm](https://elm-lang.org/) with map integration via [Leaflet](https://leafletjs.com/) Ports. It works as a Progressive Web App – installable and offline-capable after first load.

Try it out: [ratopi.github.io/stromfinder](https://ratopi.github.io/stromfinder/)

Source code on [GitHub](https://github.com/ratopi/stromfinder).


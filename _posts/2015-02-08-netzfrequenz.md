---
title: "Project: Netzfrequenz – measuring mains frequency with an Arduino"
layout: blog_post
abstract: An Arduino sketch for determining the current mains frequency using nothing more than a piece of wire.
author: Ralf Th. Pietsch
date: 2015-02-08
---

Published [Netzfrequenz](/netzfrequenz) – a small Arduino sketch that measures the current mains frequency using nothing more than a short piece of wire connected to an analog port.

The mains frequency (50 Hz in Europe) is not as constant as one might think. It fluctuates depending on the balance between power generation and consumption across the grid. When too little power is fed into the grid, the frequency drops. When too much is fed in, it rises.

This kind of measurement could become interesting in the context of smart grids – the frequency can be measured at any location, independently of a central authority, to assess the load state of the entire grid. Local consumers could then be switched on and off accordingly. See also: [Smart Grid – einfach, dezentral, selbstorganisiert](http://www.solarify.eu/2015/01/27/205-smart-grid-einfach-dezentral-selbstorganisiert/).

### How it works

A short piece of wire (around 10 cm) is connected to analog port A0, with the other end left open. The wire acts as an antenna and picks up a noisy mains hum. The sketch measures the time between minimum crossings of this signal – which corresponds to the period. The reciprocal gives the frequency. To improve accuracy, the time for 50 periods is measured and averaged.

The measured frequency can be compared with the official grid frequency at [netzfrequenzmessung.de](http://www.netzfrequenzmessung.de/).

Source code on [GitHub](https://github.com/ratopi/netzfrequenz).


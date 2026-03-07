---
title: "Bencoding – BitTorrent's data format in Erlang"
layout: blog_post
abstract: First release of a Bencoding encoder/decoder in pure Erlang.
author: Ralf Th. Pietsch
date: 2018-10-23
category: project
---

Published [Bencoding](https://github.com/ratopi/bencoding) – an encoder/decoder for the BitTorrent serialization format, written in pure Erlang.

Bencoding is a simple but effective format used by the BitTorrent protocol for torrent files and tracker communication. It defines just four types: integers, byte strings, lists, and dictionaries.

To include it in your project:

    {deps, [bencoding]}.

More details on the [project page](/projects/bencoding).


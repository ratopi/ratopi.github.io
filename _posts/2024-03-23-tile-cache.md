---
title: "TileCache for OSM tiles"
layout: blog_post
abstract: A caching server for OpenStreetMap tiles, reducing traffic and saving resources on the real tile server.
author: Ralf Th. Pietsch
date: 2024-03-23
category: project
---

Since we need to display maps in a current project, I sat down and wrote a tile cache server in Erlang. It sits between your application and an OpenStreetMap tile server, caching tiles locally to reduce traffic and save resources on the upstream server.

Start it with Docker:

    docker run --rm -p 8008:8008 ratopi/tile-cache

Or with rebar3:

    rebar3 shell

Source code on [GitHub](https://github.com/ratopi/tile-cache).

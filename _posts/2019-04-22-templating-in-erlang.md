---
title: Templating in Erlang
layout: blog_post
abstract: Erlang is well suited for writing a template engine, due to its pattern matching capabilities
author: Ralf Th. Pietsch
date: 2019-04-22
image: printing
---
Erlang is not only perfect for big supervised application that run distributed with extreme availability times.
Erlang is also perfect for writing parsers due to its integrated pattern matching.

For the preparation of converting LaTeX-documents to asciidoc-documents I've written a very simple
LaTeX-parser in extremely short time; indeed it takes only some minutes to write it.
You find this parser at <a href="https://github.com/ratopi/texparser">GitHub</a>.

At work we use a templating engine, with docx-Templates as sources generating docx-Files.
It is written in Java and uses FreeMarker for doing the templating stuff.

So I thought by myself it must be simple to write a FreeMarker replacement in Erlang.
And in fact it was extremely simple, it takes me jut 34 minutes from executing

	rebar3 new app templater

to the initial git commit with first basic functuality and working tests.

You find the code at <a href="https://github.com/ratopi/templater">https://github.com/ratopi/templater</a>.

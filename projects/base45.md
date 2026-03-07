---
title: Base45
description: A Base45 encoder/decoder in pure Erlang
layout: page
---

A Base45 encoder/decoder in pure Erlang.

Implements the encoding scheme defined in [RFC 9285](https://datatracker.ietf.org/doc/rfc9285/). It was notably used for encoding the EU Digital COVID Certificate in QR codes.

### About Base45

Base45 encodes pairs of bytes (16 bit) into 3 characters, and a remaining single byte into 2 characters. It uses a 45-character subset of US-ASCII that is compatible with the Alphanumeric mode of QR codes.

The number 45 comes from the QR code standard (ISO/IEC 18004). In Alphanumeric mode, a QR code supports exactly 45 characters: the digits `0-9`, the uppercase letters `A-Z`, and 9 special characters. This mode is more compact than Byte mode, encoding two characters in just 11 bits. Base45 takes advantage of this by mapping binary data exclusively to these 45 characters, resulting in smaller QR codes than e.g. Base64 (which would require the less efficient Byte mode).

### Usage

    base45:encode(<<1,2,3>>).   %% => <<"X5030">>
    base45:decode(<<"X5030">>). %% => <<1,2,3>>

### Import

Erlang (rebar3):

    {deps, [base45]}.

Elixir (Mix):

    {:base45, "~> 3.0"}

Available via [Hex.pm](https://hex.pm/packages/base45). Source code and releases on [GitHub](https://github.com/ratopi/base45).

Licensed under Apache 2.0.

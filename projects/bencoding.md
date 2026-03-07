---
title: Bencoding
description: An encoder/decoder for the BitTorrent data format in pure Erlang
layout: page
---

An encoder/decoder for the [Bencoding](https://www.bittorrent.org/beps/bep_0003.html) data format in pure Erlang.

Bencoding is the serialization format used by the [BitTorrent](https://www.bittorrent.org/) protocol for torrent files and tracker communication.

### Type Mapping

| Bencoding Type | Erlang Type | Example (Bencoded) | Example (Erlang) |
|---|---|---|---|
| Integer | `integer()` | `i42e` | `42` |
| Byte String | `binary()` | `4:spam` | `<<"spam">>` |
| List | `list()` | `l4:spami42ee` | `[<<"spam">>, 42]` |
| Dictionary | `map()` | `d3:cow3:mooe` | `#{<<"cow">> => <<"moo">>}` |

Dictionary keys are always byte strings, encoded in sorted order as required by BEP 3. Encoding and decoding are roundtrip-safe.

### Usage

```erlang
%% Encode
{ok, <<"4:spam">>} = bencoding:encode(<<"spam">>).
{ok, <<"d3:cow3:moo4:spam4:eggse">>} = bencoding:encode(#{
    <<"spam">> => <<"eggs">>,
    <<"cow">> => <<"moo">>
}).

%% Decode
{ok, <<"spam">>, <<>>} = bencoding:decode(<<"4:spam">>).
{ok, #{<<"cow">> := <<"moo">>}, <<>>} = bencoding:decode(<<"d3:cow3:mooe">>).
```

Also works from Elixir without any wrapper:

```elixir
{:ok, encoded} = :bencoding.encode(%{"cow" => "moo"})
{:ok, value, rest} = :bencoding.decode("d3:cow3:mooe")
```

### Reading a Torrent File

```erlang
{ok, FileContent} = file:read_file("example.torrent"),
{ok, Torrent, <<>>} = bencoding:decode(FileContent),
Name = maps:get(<<"name">>, maps:get(<<"info">>, Torrent)).
```

### Installation

Erlang (rebar3):

    {deps, [bencoding]}.

Elixir (Mix):

    {:bencoding, "~> 1.0"}

Available via [Hex.pm](https://hex.pm/packages/bencoding). Source code on [GitHub](https://github.com/ratopi/bencoding).

Licensed under MIT.

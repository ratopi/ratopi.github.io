---
title: "Why Erlang? The Underestimated Strengths of a Proven Platform"
layout: blog_post
abstract: "Erlang is over 35 years old – and more relevant than ever. A look at the strengths that make this language so uniquely suited for modern distributed systems."
author: Ralf Th. Pietsch
date: 2026-03-20
category: blog
---

## The Language Built for Reliability

Erlang was developed at Ericsson in the late 1980s – with a clear goal: **Build telephony systems that must not go down.** The requirements back then sound like today's cloud architecture wish list:

- 99.9999999% availability (the famous "nine nines")
- Hot code upgrades without downtime
- Thousands of concurrent connections
- Fault tolerance as a core principle

What was originally built for telephone switching is now the foundation for WhatsApp, Discord, RabbitMQ, and many other systems that need to run reliably under extreme load.

---

## 1. Lightweight Processes

Erlang processes are **neither operating system processes nor threads.** They are managed by the BEAM VM and are extremely lightweight:

```erlang
%% Start a million processes? No problem.
[spawn(fun() -> timer:sleep(60000) end) || _ <- lists:seq(1, 1000000)].
```

A single Erlang process uses only about **300 bytes** of memory. For comparison: a Java thread requires at least 512 KB to 1 MB of stack. That means:

| | Erlang Process | Java Thread | Go Goroutine |
|---|---|---|---|
| Memory | ~300 bytes | ~512 KB | ~8 KB |
| Creation | ~3 µs | ~1 ms | ~6 µs |
| Maximum count | Millions | Thousands | Hundreds of thousands |

---

## 2. "Let It Crash" – Errors as a Feature

In most languages, you write defensive code:

```java
// Java: Defensive programming
try {
    connection = openConnection(host, port);
    data = connection.read();
    result = process(data);
} catch (ConnectionException e) {
    logger.error("Connection failed", e);
    retryWithBackoff();
} catch (DataException e) {
    logger.error("Data processing failed", e);
    fallbackStrategy();
} catch (Exception e) {
    logger.error("Unexpected error", e);
    emergencyShutdown();
}
```

In Erlang, things are fundamentally different. Processes are isolated – when one crashes, it doesn't affect any other. **Supervisors** monitor processes and restart them as needed:

```erlang
%% Supervisor configuration: If a worker crashes, it gets restarted
init([]) ->
    SupFlags = #{
        strategy => one_for_one,   %% Only restart the crashed process
        intensity => 5,            %% Max 5 restarts ...
        period => 60               %% ... per minute
    },
    Children = [
        #{id => worker,
          start => {my_worker, start_link, []},
          restart => permanent}
    ],
    {ok, {SupFlags, Children}}.
```

This is not a workaround – this is **the architecture.** Supervisor trees are structured hierarchically. If an entire subtree is beyond saving, it gets completely restarted without affecting the rest of the system.

---

## 3. Pattern Matching – Elegant and Expressive

Pattern matching in Erlang is far more than a `switch` statement. It permeates the entire language:

```erlang
%% Function clauses with pattern matching
handle_message({login, Username, Password}) ->
    authenticate(Username, Password);

handle_message({send_msg, From, To, Text}) ->
    deliver(From, To, Text);

handle_message({logout, Username}) ->
    cleanup_session(Username);

handle_message(Unknown) ->
    log_warning("Unknown message: ~p", [Unknown]).
```

No `if-else` cascades, no type checks. The code reads almost like a specification. And the compiler warns if a case is not covered.

---

## 4. Immutable Data – No Race Conditions

In Erlang, **all data is immutable.** There are no variables that can be overwritten:

```erlang
%% Once bound, always bound
X = 42,
X = 43.  %% Error! "no match of right hand side value 43"

%% Instead: New bindings
List1 = [1, 2, 3],
List2 = [0 | List1].  %% List2 = [0, 1, 2, 3], List1 remains [1, 2, 3]
```

Combined with process isolation, this means: **Race conditions are structurally impossible.** No `synchronized`, no `mutex`, no `volatile`. Processes communicate exclusively via message passing:

```erlang
%% Process A sends a message
PidB ! {self(), "Hello"},

%% Process B receives it
receive
    {From, Msg} ->
        io:format("Message from ~p: ~s~n", [From, Msg]),
        From ! {self(), "Thanks!"}
end.
```

---

## 5. Hot Code Loading – Updates Without Downtime

Erlang can **swap running code without stopping the system.** This is not a hack – it's a built-in feature of the BEAM VM:

```erlang
%% Version 1 is currently running
-module(pricing).
-export([calculate/1]).

calculate(Amount) ->
    Amount * 1.19.  %% 19% VAT

%% Version 2 is loaded – WITHOUT restart
calculate(Amount) ->
    Amount * 1.21.  %% New tax rate
```

Existing connections are not interrupted. New requests use the new code, while in-flight requests complete with the old code. This is why Ericsson switches run for years without a restart.

---

## 6. Distribution – Built In, Not Bolted On

Distributed systems are not an add-on package in Erlang. The BEAM VM can natively communicate with other nodes:

```erlang
%% On Node A
net_adm:ping('nodeB@server2').  %% Establish connection

%% Start a process on another node
Pid = spawn('nodeB@server2', fun() ->
    heavy_computation()
end),

%% Send a message to the remote process – same syntax!
Pid ! {process, data}.
```

Message passing works **transparently** – regardless of whether the process runs on the same machine or on another continent. The syntax is identical.

---

## 7. OTP – The Swiss Army Knife

OTP (Open Telecom Platform) is the real gem. It provides proven building blocks for robust systems:

- **GenServer** – Generic server process with state management
- **Supervisor** – Monitoring and restarting of processes
- **Application** – Packaging and lifecycle management
- **ETS** – Fast in-memory key-value store
- **Mnesia** – Distributed database, built in

```erlang
%% A GenServer in just a few lines
-module(counter).
-behaviour(gen_server).

init([]) -> {ok, 0}.                              %% Initial state: 0

handle_call(get, _From, Count) ->
    {reply, Count, Count};                         %% Return current value

handle_cast(increment, Count) ->
    {noreply, Count + 1}.                          %% Increment counter
```

---

## Who Relies on Erlang?

| Company | Use Case |
|---|---|
| **WhatsApp** | 2 billion users, ~50 engineers |
| **Discord** | Millions of concurrent connections |
| **RabbitMQ** | One of the most popular message brokers |
| **Ericsson** | Telecom infrastructure worldwide |
| **Klarna** | Payment platform |
| **Nintendo** | Push notification system |

WhatsApp is the most impressive example: at the time of its acquisition by Facebook, **~50 developers** managed a system serving **900 million users.** That ratio is only possible with Erlang.

---

## And What About Elixir?

Elixir runs on the same BEAM VM and offers a more modern syntax with a Ruby-like look:

```elixir
# Elixir – same power, more modern syntax
defmodule Counter do
  use GenServer

  def init(_), do: {:ok, 0}

  def handle_call(:get, _from, count), do: {:reply, count, count}
  def handle_cast(:increment, count), do: {:noreply, count + 1}
end
```

Elixir additionally brings excellent tooling (Mix, Hex), metaprogramming via macros, and with Phoenix a web framework that offers LiveView for reactive UIs – without JavaScript. **For those who want to leverage the BEAM platform, Elixir provides a modern entry point.**

---

## Conclusion

Erlang is not the right language for every problem. For numerical computations, GUI applications, or machine learning, there are better tools. But for what it was built for – **highly available, distributed, fault-tolerant systems** – it remains unmatched after more than 35 years.

The question is not "Why Erlang?" – but rather: **"Why are we still building distributed systems without the concepts that Erlang has offered since 1986?"**

> "If Java is 'write once, run anywhere', then Erlang is 'write once, run forever'."
>
> — *Joe Armstrong, creator of Erlang*


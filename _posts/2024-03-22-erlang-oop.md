---
title: Is Erlang an OOP language?
layout: blog_post
abstract: Some thoughts about what Erlang is ... and what it even means.
author: Ralf Th. Pietsch
date: 2024-03-22
---

*Updated March 7, 2026 – substantially revised and expanded.*

## Is Erlang an OOP language?

Yes – because Erlang processes are encapsulated elements that change their
state by exchanging messages.

In fact, Erlang's process model is remarkably close to what OOP was originally meant to be.
Each process owns its own memory – strictly isolated, no shared state.
The only way to interact with a process is by sending it a message.
The process decides how to react, when to react, and what to reveal.
This is encapsulation in its purest form.

Compare this to Java or C++, which claim to be object-oriented but depart from the original idea in two fundamental ways.
First, they replace messages with method calls – which are really just function calls in disguise.
A method call is synchronous, it exposes the interface, and it binds the caller tightly to the implementation.
A message, on the other hand, is asynchronous by nature.
The sender doesn't know – and doesn't need to know – how the receiver handles it.

Second, languages like Java undermine encapsulation by introducing visibility modifiers like `public` and `protected`.
The mere existence of `public` fields means that internal state can be accessed and modified from the outside.
Even `protected` is just a slightly narrower hole in the wall.
The wall that was supposed to protect the object's integrity.

Some may argue that OOP requires classes.
But classes are just a way to organize code – they are not the essence of OOP.
The essence is encapsulated state and message passing.
Every function in Erlang that spawns a process *is* a class – it creates an independent entity with private state that communicates solely through messages.

According to Alan Kay, encapsulating data and passing messages is the more important idea behind the term OOP.
Kay was inspired by biology and chemistry – how cells and molecules interact not by exposing their internals, but by sending chemical signals to each other.
No molecule reaches into another to rearrange its atoms.
They communicate through well-defined interfaces, and the receiver decides what to do with the signal.
Erlang's process model follows exactly this principle.
_[Alan Kay about the term OOP](https://userpage.fu-berlin.de/~ram/pub/pub_jf47ht81Ht/doc_kay_oop_en)_

## Inheritance is overrated

I think inheritance is one of the most overrated ideas in OOP.
Every beginner learns that red trucks inherit their characteristics from cars.
This example is completely irrelevant in practice.
Inheritance is a construct that is extremely rarely needed in daily work.

It can usually be replaced by delegation.
Delegation also avoids problems with multiple inheritance.
I like to call this the molecule model, in contrast to the onion model.
Molecules are far more variable than onions.
Change one atom in a molecule, and you may get completely different behaviour.
Try to change one of the inner layers of an onion without destabilizing its structure.

What matters far more is the exchange of messages between objects.
(That doesn't make Java or C++ or C# any better than Smalltalk, by the way.)

## Is Erlang a functional language?

Yes, because functions can be handled as any other type.

Tail recursion is another thing.
(Just compare a stack trace of Java with one of Erlang ... and you will understand.)

## Furthermore: Erlang is a declarative language

After the hype of functional programming, the next wave will – perhaps – be declarative programming.
What does it mean?
It means that you describe facts instead of paths to solutions.

Prolog is the best known declarative language.
If you want to find the grandfather, you just specify who is the father of whom
and then ask: who is the father's father?

Erlang and its pattern matching possibilities let you describe facts.
And together with ...

## "Let it crash"

Together with the paradigm of "let it crash", you are able to write rock solid
applications.

Why?
Because your code represents what you expect.
In a real life situation, with running software on real hardware, anything can
happen.
Claiming "this will never happen" is naive – instead, let the code crash and have
a supervisor restart it, bringing you back to a defined state.

## Conclusion

OOP, functional, declarative, "let it crash" ... in the end, these are all just words.
Words are useful – without having a word for something we cannot talk about it.
Yet these labels matter less than the underlying principle.
Programming is about expressing yourself in the most precise way possible.
That's why mathematics has developed a formula language to be precise.

So, be precise and express yourself ... and look for the language that allows exactly that.

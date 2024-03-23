---
title: Is Erlang an OOP language?
layout: blog_post
abstract: Some thoughts about what Erlang is ... and what it even means. 
author: Ralf Th. Pietsch
date: 2024-03-22
image: machine
---

Some thoughts about Erlang

# Is Erlang an OOP language?

In my opinion yes, because Erlang process are encapsulated elements that change their 
state due to interchange messages.

Some may argue, but OOP has classes.
In my opinion, classes are defined by functions that start an Erlang process.

You may compare it to Java or C++, which completely ignore the main fact of encapsulating the 
state of an object, by introducing protected and public members.
Java, C++, etc are ignoring the fact of message interchanging completely.
And due to Alan Kay, encapsulating data and message interchanging is the more important idea
behind the term OOP.
_[Alan Kay about the term OOP](https://userpage.fu-berlin.de/~ram/pub/pub_jf47ht81Ht/doc_kay_oop_en)_

What about inheritance?
I think inheritance is one of the most overrated ideas in OOP.
Every beginner learns that red trucks inherit their characteristics from cars.
This example is completely irrelevant in practice.
Inheritance is a construct that is extremely rarely needed in daily work.

Inheritance can usually be replaced by delegation.
Delegation also avoids problems with multiple inheritance.
That's what I call molecule model on contrast to the onion model.
Molecules are far more variable than onions.
By changing one atom in a molecule, you perhaps get a completely other behaviour.
Try to change one of the inner layer of an onion, without destabilize its structure.

So, much more important is the exchange of messages between objects.
(And that really doesn't make Java or C++ or C# any better than Smalltalk.)

# Is Erlang a functional language?

Yes, because functions can be handle as any other.

Tail recursion is another thing.
(Just compare a stack trace of Java with one of Erlang ... and you will understand.)

# Furthermore: Erlang is a declarative language

After the hype of functional programming, the next hype will - perhaps - be, declarative programming.
What does it mean?
It means that you describe facts instead of paths to solutions.
                                   
Prolog is the best known declarative language.
If you like to get the grandfather you just specify the fathers of each other and
then ask how's the father's father?

Erlang and its pattern matching possibilities let you describe facts.
And together with ...

# "Let it crash"

Together with the paradigm of "let it crash", you are able to write rock solid
applications.

Why?
Because your code represents what you expect.
In a real life situation, with running software on real hardware, everything can 
happen.
It's stupid to say "this will never happen", but it is not, if your code just stops working
and a supervisor restarts the code, so we are again in defined environment.
                
# Conclusion

OOP, functional, declarative, "let it crash" ... at the end, these are all only words.
Words are useful, because without having a word for something we can not talk about it.
But these words are less useful when it comes to what is programming all about.
At the end programming is to express yourself in the most precise way possible.
That's why mathematics has developed a formula language to be precise.

So, be precise and express yourself ... and look out for the language, which allows exactly that.

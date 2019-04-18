---
title: Creating a simple JSON parser with Erlang's pattern matching
layout: blog_post
abstract: Creating a JSON parser with a declaritive syntax should be simple. In this post we show how to implement a simple JSON parser in Erlang.
author: Ralf Th. Pietsch
date: 2018-10-14
draft: true
---

Let's begin with the simple ones.

parse_element/1 should be a function taking a binary an return one the following

	{ok, JsonObject, Rest}
	eof
	{error, Reason}



Straight forward parsing of "true" and "false" is implemented by

	parse_element(<<$t, $r, $u, $e, Rest/binary>>) ->
		{ok, true, Rest};
	
	parse_element(<<$f, $a, $l, $s, $e, Rest/binary>>) ->
		{ok, false, Rest};

For the string "true", it returns the atom "true" and the Rest of the binary string.
For "false" it's the same.

Next simple thing is to parse arrays

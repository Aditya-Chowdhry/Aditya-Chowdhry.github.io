---
title: "Hashes in Ruby (2020) - Gotchas with Ruby hash syntax and ruby symbols"
layout: post
date: 2020-07-11 04:00
tag:
- ruby
- rubyonrails
- ror
- rubyhashes
- symbols
- hashsyntaxes
- hashes-ruby

headerImage: true
image: /assets/ruby.png
hidden: false # don't count this post in blog pagination
description: "This blog post aims at bringing clarity to confusing ruby hash syntax involving ruby symbols."
jemoji: ""
category: blog
author: adityachowdhry
externalLink: false
---

# Hashes in Ruby (2020) - Gotchas with Ruby hash syntax and ruby symbols

## **Motivation- Why to write about Hashes in Ruby?**

There are already a lot of blogs and guides around Ruby, so why another? Despite the existing material on this topic, I have seen new devs who have just started with the language to get confused with hash syntax in ruby. We'll be discussing the why!

**Tl;dr**

## Ways to write a Ruby Hash

```ruby
{
	"color" => "red",
	"type" => "car"
}

#Getting color of vehicle value

vehicle["color"]
=> "red"
```

```ruby
{
	:color => "red",
	:type => "car"
}

#Getting color of vehicle value

vehicle[:color]
=> "red"
```

```ruby
{
	color: "red",
	type: "car"
}

#Getting color of vehicle value

vehicle[:color]
=> "red"
```

## **What's the problem with Ruby hash syntax?**

### Ruby Symbols And Change in hashes syntax

New devs starting out with Ruby usually overlook the concept of symbols and often discover the use cases and other factors during the process of coding.

What does it look like?

**:foobar**

A ruby symbol is often confused with a variable. But it is not. It is an identifier. I won't go in detail of explaining the concept of a Symbol in ruby. It is well explained here - [rubyguides](https://www.rubyguides.com/2018/02/ruby-symbols/)

**But then why are we even talking about it here?**

This is because symbols can be used in a Ruby Hash. Just like we used in these examples

```ruby
#Example 1 (symbol with hash-rocket)
vehicle = {
	:color => "red",
	:type => "car"
}

#Getting color of vehicle value

vehicle[:color]
=> "red"
```


```ruby
#Example 2 (just symbol, similar to a json)
vehicle = {
	color: "red",
	type: "car"
}

#Getting color of vehicle value

vehicle[:color]
=> "red"
```


Example 1 follows an old syntax of ruby to write a hash i.e a symbol ⇒ value. Here. **:color** is a symbol which has a value **red.** (This is still valid)

It has a bit complicated structure, thus ruby made it easier in version 1.9 by allowing to write a hash in the way it is mentioned in example 2

Here is the catch, **color:** is still a symbol, but now it looks neat and similar to JSON type structure or other language constructs. 

This is where problem brews up. A new dev looks at example 2 and tries to  write the following code:

```ruby
vehicle = {
	"color": "red",
	"type": "car"
}
```

Coming from Javascript mindset or other languages

To get color of vehicle a natural instinct would be to do:

```ruby
vehicle["color"]
=> nil
#whaaaat??
```

but what do we get on latest ruby version, a **nil**

But why? This is because `"color":`  is still a symbol. Also, being a simple one-word, ruby easily converts it into a symbol `:color`

So doing a `vehicle[:color]` would give a correct result

What if the key of hash is not a simple one word or having a whitespace? Like below examples

```ruby
person = {
	"first.name": "John Doe",
}

#To get first.name
#Valid syntax
person[:"first.name"]
=> "John Doe"
```

```ruby
person = {
	"first name": "John Doe",
}

#To get first name
#Valid syntax
person[:"first name"]
=> "John Doe"
```

Then ruby would treat the key as it is as a symbol(with quotes) i.e `:"first.name"` and `:"first name"`

The above things were fixed in Ruby 2.2 with feature request - [https://bugs.ruby-lang.org/issues/4276](https://bugs.ruby-lang.org/issues/4276)

		Thanks for reading the post! Hope this brings some sort of clarity. 
		Comment below if you have any questions!
	

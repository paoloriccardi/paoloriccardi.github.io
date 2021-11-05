---
title: Hey Oh, Let's Go (lang)
layout: post
categories: Software_Development Programming_Languages
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: I finally gave it a chance and I started to study Go. I've been programming more or less continuously for the latest 20 years or so and thus I gathered some experience with various programming languages. Yet Go felt different from the first impact, here are the first few things that struck me. 
---

##### What is Go
If you've been in computer science long enough you have seen lots of new kids on the block. Some of them eventually proved the test of time, while the less fortunate ones were put in a closet with all the other out of fashion buzzwords, where they patiently wait for their time to shine again.
![I double dare you](/images/blockchain.jpg){:width="75%" height="75%" .center-image}

[Go](https://golang.org/){:target="_blank"} came out at Google almost a decade ago, it was announced in 2009, and it quickly become the next cool thing. In a few years everybody wanted to put it on their resume so badly since it was seen by many as the *language for the cloud*.

Ok, let's go with small steps.
If you ask what Go is, that's the answer you get on its official website: *Go is an open source programming language that makes it easy to build simple, reliable, and efficient software*. 

Let's add that Go didn't come out of the blue. It is often referred as a C-like language and indeed among its ancestors there is the C language, as well as [CSP](https://en.wikipedia.org/wiki/Communicating_sequential_processes){:target="_blank"} and Pascal.

This rich heritage brings some interesting things to the mix, such as it's both a compiled and statically typed language, but another key aspect is its powerful set of primitives for concurrency derived from CSP. 

So it should be a language for great performances, perfect for networking and concurrency, easy to read with a minimum background and also easy write as long as you follow its tenets.
Anyway be warned, if you come from either an Object Oriented Language or a dynamically typed language or an interpreted language, you may need some time to get used to its way of doing things.

##### Essential bibliography
A couple of days ago, I picked up the excellent [Learning Go](https://www.oreilly.com/library/view/learning-go/9781492077206/){:target="_blank"} by Jon Bodner from my backlog of books and I decided to give it a try. It's very up to date and it's" focused on what the author calls an idiomatic approach, which means it teaches you how to do things the Go way, how to speak the "Go language" without any foreign accent. As you will notice reading the book, keeping it clean and orthodox is one of the mantra of Go. So forget your favourite Javisms, like going heavy on OO programming for structuring code, or all your Pythonic niceties, like automatic type conversion.

I think the idiomatic element is very important in every language in order to be able to fully leverage its potential but it become paramount in saving you a lot of frustrations for a language like Go where even the style of code formatting which the programmer should use is enforced

For example, are you the kind of person that put curly brackets right at the end of the method declaration or at the beginning of the newline? In Go you don't have this choice because the second one gives a compiling error. 

```go
func main()
{
    fmt.Println("This is not valid in Go!")
}
```

Speaking of bibliography, another great book which is worth mentioning and from which I'm sneak peaking from time to time, is the classic [The Go Programming Language](https://www.gopl.io/){:target="_blank"} by Alan A. A. Donovan and Brian W. Kernighan. Yes, that Brian W. Kernighan.

##### Standardization and enforcement, a possible explaination
To be honest, if you come from other languages, things like the one I described above can be a little bit of a shock. Furthermore let's be honest, we like to think ourselves as artists or at least creative craftsmen and serialization and standardization sounds more like industry than like art.

On the funny side, let's not forget that the argument of spaces vs tabs can break relationships as discussed in a famous [Silicon Valley episode](https://www.imdb.com/title/tt5218484/){:target="_blank"} and, by the way, in the Go universe it's tabs (and I agree on that specific tenet).

There are many things that are peculiar in Go and that I will learn to appreciate and leverage as far as I progress with the language but the "forced standardization" is the one that immediately captured my attention in a not so pleasant way. Nevertheless, after a little bit of deeper pondering, I think there is a reason, or at least a possible explanation, for removing these kind of choices from the availability of the programmer. 

Go was born as a programming language in a context where the codebases as well as the number of teams and individual contributors, were (and still are) big for the average software engineer standards. 
In such a situation, dealing with the idiosincracies of tens of other programmers in terms of coding styles and code formatting can become a real pain very quickly. Not to mention the possibilities to efficiently automate tasks on code. Choice creates variations.
In order to reduce entropy, there is a very small number of language keywords, so for example `for` is the only way to have a loop in Go.

This idea make sense even if you think about another aspect, the growth of a Project often comes with the necessity of increasing the head count for development, operations, maintenance and so on. This means hiring but even retraining/reskilling and replacing lots of new people frequently, so every new addition to a team will have to hit the ground running.

Standards help reducing the complexity that joining a new project implies. If your city is burning and the local fire department is failing to put down the fire it's easier to receive help from the firefighters of nearby cities if their hose couplings fit your fire hydrants. Does it seem like an unrealistic scenario? Go check the [Great Baltimora fire](https://en.wikipedia.org/wiki/Great_Baltimore_Fire){:target="_blank"} to see what I mean.

##### Old habits die hard
I've used several programming languages in my life: Basic, Pascal, C, Php, JS, Java, Objective C, but the one I've been using the most, in the last years is Python. 
Why? Well, the first reason that comes to my mind is that since I'm not so closely involved in the daily coding process anymore, so when I do usually it's for:
- Writing a blog post (such this one)
- Building a tactical tool with few to zero strings attached (e.g. cleaning a dataset or putting up a quick webservice for a PoC)
- Working on some pet project (I'll eventually pitch one of them in another post)

So usually no teams or codebases to comply against unless I choose to, and no particular technical boundaries.
Furthermore I don't do this as a regular activity, so I need something that is robust but even easy going and somewhat forgiving.
Python fits the role perfectly, you can do pretty much anything with it, even if it won't guarantee top notch performances but most of all you can pick it up after months of inactivity and feel at home right away, being productive in minutes.

In a way I got used to that cozy and familiar environment that Python was offering and in IT being in your comfort zone too much usually is up to no good. To put this under another perspective, I've been practicing martial arts for the last 20 years, over time I've met a lot of interesting people from different backgrounds and I tried to learn something from each and everyone of them, well once I met a Karate instructor who told me one thing that fits this situation perfectly: *Comforts kill you*. 

##### Surprises
When you come to Go from a different background (as I did), you'll have a lot of "wait a minute" moments reading the manual. This is because, as I said not only Go is a beast of its own but because it does things in its own way and it require you to adapt as a developer to that mindset.

That's not a bad thing per se but I admit that the first impact may be a thing to deal with.

Here are some of the things that struck my attention so far:
1. Source code formatting is enforced
2. Every variable not assigned to a value get the `zero` value of its own type
3. There is only one looping keyword, which is `for`, that can be used in 4 different ways according to your needs   
4. Variable's visibility is related to the block it is in, which mean that a variable can be *shadowing* another with the same name in a containing block
5. Go uses pass by value
6. There is no such a thing as automatic type conversion or automatic type promotion, so if you try to sum a `uint32` and a `uint64` you will get an error, also be aware that the `int` type varies upon the architecture (32 vs 64 bit)
7.  
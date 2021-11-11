---
title: Hey Oh, Let's Go (lang)
layout: post
categories: Software_Development Programming_Languages
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: I finally gave it a chance and I started to study Go. I've been programming more or less continuously for the latest 20 years or so and thus I gathered some experience with various programming languages. Yet Go felt different from the first impact, here are the first few things that struck me. 
---

##### The hype
If you've been in computer science long enough you have seen lots of new kids on the block. Some of them eventually proved the test of time, while the less fortunate ones were put in a closet with others out of fashion buzzwords that patiently wait for the chance to shine again.

The problem with buzzwords is that once the hype is started the sky is the limit. 
A new technology that may have proven some value in a certain context attracts throngs of snake oil sellers. Just name your problem and you'll find somebody willing to sell an overhyped technology (or methodology) to fix it no matter what. 
Unfortunately there is no such a thing as a silver bullet, there are (usually) different ways to achieve the same result and there are (always) tradeoffs.
 ![I double dare you](/images/blockchain.jpg){:width="75%" height="75%" .center-image}

But Go looks very different from snake oil. The [Go](https://golang.org/){:target="_blank"} programming language came out at Google almost a decade ago, in 2009, and it quickly become the next cool thing. In the following years it was used to power project that had a huge impact on the industry like Docker (2013), Kubernetes (2014) and CockroachDB (2015).
No surprise the Go keyword become hot both on tech job offerings and on CVs.

So as you can imagine there is some hype around it. What surprised me is that browsing around I found a lot of opinions about it that were either extremely positive or extremely negative, depending on who you speak to.
I've never had this kind of "all or nothing" approach towards technology, furthermore I don't feel qualified enough to express a meaningful opinion on Go yet but what I can say so far is that it's different from what I was used to. For that reason it took some effort and time to get in tune but on the other hand it has a lot of very powerful and yet very accessible features that cannot be overlooked.

##### What is Go
That's what the official website says: *Go is an open source programming language that makes it easy to build simple, reliable, and efficient software* and, consistently with the language, every word counts. 

Go didn't come out of the blue. It is often referred as a C-like language because of its syntax but also because the C language is among its most famous ancestors, as well as [CSP](https://en.wikipedia.org/wiki/Communicating_sequential_processes){:target="_blank"} and even Pascal.
This rich heritage brings some interesting things to the mix, such as it's both a compiled and statically typed language, it uses *pass by value* and it provides a powerful set of primitives for concurrency derived from CSP which, at least for me was its bigger selling point. 

So it should be the ideal choice for great performances, perfect for networking and concurrency, easy to read with a minimum background and also easy to write as long as you follow its tenets.
Anyway if you come from either an Object Oriented Language or a dynamically typed language or an interpreted language, you may need some time to get used to its way of doing things.

##### Essential bibliography
A couple of weeks ago, I picked up the excellent [Learning Go](https://www.oreilly.com/library/view/learning-go/9781492077206/){:target="_blank"} by Jon Bodner from my backlog of books and I decided to give it a try. It's very up to date and it's" focused on what the author calls an idiomatic approach, which means it teaches you how to do things the Go way, how to speak the "Go language" without any foreign accent. As you will notice reading the book, keeping it clean and orthodox is one of the mantra of Go. So forget your favourite Javisms, like going heavy on OO programming for structuring code, or all your Pythonic niceties, like automatic type conversion.

I think the idiomatic element is very important in any language to fully leverage its potential but it become paramount in saving you a lot of frustrations in a language like Go where even the style of code formatting which the programmer should use is enforced.

If you read this book, you'll find that one of the most recurring sentence will be something like "This feature is legal, but anyway if you have to use it too often, or if you need it beyond these circumstances, maybe you should consider refactoring you code logic to remove it". 
The tenet of producing clean code is everywhere and I resonate with this idea a lot. 

In my opinion, one of the worst thing that can happen to programmers is to think that it's enough for their code to just work. I would say this should be the minimum requirement for a professional, then there are all the so called *ilities* to ensure.
Taping a broken wing on a falling airplane may be a necessary emergency measure but as soon as the airplane has landed you should fix the issue in a permanent way.
Unfortunately, the IT world out there is full of temporary solutions that have become permanent, producing tons and tons of undocumented and unrecognized technical debt.

Speaking of bibliography, another great book which is worth mentioning and from which I'm sneak peaking from time to time, is the classic [The Go Programming Language](https://www.gopl.io/){:target="_blank"} by Alan A. A. Donovan and Brian W. Kernighan. Yes, that Brian W. Kernighan. 

##### In favour of standards
The idiomatic approach to Go puts a lot of emphasis not only on writing efficient code, but even on writing it efficiently. To achieve this purpose the authors tried to simplify the syntax as much as possible (e.g. reducing the number of keywords) but they also took into account how source code should be formatted.
For example, are you the kind of person that put curly brackets right at the end of the method declaration or at the beginning of the newline? In Go you don't have this choice because the latter will cause a compiling error. 
```go
func main() {
    fmt.Println("This is valid")
}

func main()
{
    fmt.Println("This is not")
}
```
To be honest, if you come from other languages, things like the one I described in the previous code snippet can be a little bit of a shock. Not only there are styling and formatting standards in Go, but they are enforced. Surely it doesn't help to alleviate the shock the fact that as programmers, we like to think ourselves as artists or at least creative craftsmen and serialization and standardization sounds more like industry than like art.

As a funny sidenote, let's not forget that the argument of spaces vs tabs can break relationships as discussed in a famous [Silicon Valley episode](https://www.imdb.com/title/tt5218484/){:target="_blank"} and, by the way, in the Go universe it's tabs (and I agree on that specific tenet).

There are many things that are peculiar in Go but the "forced standardization" is the one that immediately captured my attention in a not so pleasant way, to be honest. Nevertheless, after a little bit of deeper pondering, maybe I figured out a possible explaination for removing these kind of choices from the availability of the programmer. 

Go was born as a programming language in a context where the codebases as well as the number of teams and individual contributors, were (and still are) big for the average software engineer standards. 
In such a situation, dealing with the idiosincracies of tens of other programmers in terms of coding styles and code formatting can become a real pain very quickly. Not to mention the possibilities to efficiently automate tasks on code. 
In most programming languages when you have to iterate over a list of values you can use a `for` as well as a `while` loop right? Well these kind of choices at scale can create unnecessary variations of the code that may even do the same thing. So, in order to reduce entropy, Go has a very small number of keywords... if you need to iterate, then `for` is the only loop to use.

This idea make sense even if you think about another aspect, the growth of a Project often comes with the necessity of increasing the head count for development, operations, maintenance and so on. This means hiring but even retraining/reskilling and replacing lots of new people frequently, so every new addition to a team will have to hit the ground running.

Standards help reducing the complexity that joining a new project implies. If your city is burning and the local fire department is failing to put down the fire it's easier to receive help from the firefighters of nearby cities if their hose couplings fit your fire hydrants. Does it seem like an unrealistic scenario? Go check the [Great Baltimora fire](https://en.wikipedia.org/wiki/Great_Baltimore_Fire){:target="_blank"} to see what I mean.

##### Where I came from
I've used several programming languages in my life: Basic, Pascal, C, Php, JS, Java, Objective C, but the one I've been using the most, in the last years is Python. I'm not coding on a daily basis and when I am, usually it's for either:
- Building a tactical tool (e.g. cleaning a dataset or putting up a quick webservice for a PoC)
- Working on some pet project (I'll eventually pitch one of them in another post)

So usually no strings attached, no teams or codebases to comply with unless I choose to, and no particular technical boundaries.
Since I don't code as a daily activity I needed a language that proves robust but also easy to pick up after weeks.
Python fits the role perfectly, you can do pretty much anything with it and even if it won't guarantee top notch performances, its eco-system is wide and rich in terms of community support and libraries. Another cool feature of Python is that it can be easily understood by anybody...it fits academics as well as software engineers and tech enthusiasts. 

In a way I got used to that cozy and familiar environment that Python was offering, so if I got an idea for a pet project I tried it in Python first. That's not bad but it could become a limitation if not for the project itself for my ability to experiment and learn new things. 

To put it under another perspective, I've been practicing martial arts for the last 20 years, over time I've met a lot of interesting people from different backgrounds and I tried to learn something from each and everyone of them. Once I met a Karate instructor who told me one thing that fits this situation perfectly: *Comforts kill you*. 

When you come to Go from a different background (as I did), while learning Go you'll have a lot of "what the heck!" moments. This happens because Go is a beast of its own which does things its own way, so I needed some adjustment.

##### Change n.1: Pointers and memory
The last time I used pointers was around ten years ago, I had to rewrite in Objective C the Java codebase of a bunch of Android native apps (which by the way I had written some months before) to port them to iOS. I wasn't an Apple guy, I bought a third hand macbook pro and iphone just for the job and get rid of both of them right after, so my relationship with that particular language didn't last more than the necessary. 

Before that I used to have a way longer and older relationship with another language that used pointers, the good old C.
I discovered C during a university and in that phase of my life I used it quite a bit, mostly for fun. For instance I developed a Chess program for my bachelor degree final thesis and before that aplugin that allowed an open-source Ray Tracer to render Julia sets defined over quaternions. The following images were rendered (almost 12 years ago) with that extension.
![Julia sets over quaternions](/images/julias.jpg){:width="75%" height="75%" .center-image}

So when I started with Go I wasn't new to manage the memory for my own software and clean after them, but I was definitely out of shape. Lucky me, Go has a garbage collector which makes life a lot more easier than having to clean up by yourself using `free`, like in C. On the other side you cannot do pointer mathematics (like you could in C), unless you use the (rather self discribing) `unsafe` package from the standard library. 

My two cents is that having to learn how to deal with pointers with the help of a latency optimized garbage collector makes a huge benefit even for newbie programmers that want to lean how to keep control over memory allocation, well at least I would have loved a thing like that when I learned C.

So what you could do with pointers in Go? Well you could use them to have mutable function parameters for example. Go is pass by value, so it passes a copy of the data (which may mean a copy of the actual data for primitive types, structs and arrays and a copy of the pointer for slices).
Or you can use pointers to pass a big struct parameter to a function even if you don't want it to be mutable, just for improving performances.

##### Change n.2: No classes, no inheritance
If the pointer thing will take just some mental gymnastic to get used to it, the absence of classes (and inheritance) is something that require a deeper understanding because impacted the way a developer thinks code. 

If you've been in OO programming long enough there is a very high probability that you keep this book [Design Patterns: Elements of Reusable Object-Oriented Software](https://en.wikipedia.org/wiki/Design_Patterns){:target="_blank"} somewhere very close to your reach, as a hardcover in the bookshelf nearby your desk or as a pdf in your cloud storage. 

One of the things you learn from this book is the concept of "composition over inheritance". This makes a lot of sense, it's easier to define what you have in your pocket (preciousss) rather that what you are (Bilbo was a Hobbit but how could Gollum tell a Bolger from a Baggins? And why should he even care since he was only interested in the ring?). 

In other words, it's easier to define cleaner structures using relationships of the kind *HAS-A* rather than *IS-A*.

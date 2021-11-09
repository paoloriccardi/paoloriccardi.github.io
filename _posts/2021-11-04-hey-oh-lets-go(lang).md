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

In my opinion, one of the worst thing that can happen to programmers is to think that it's enough for their code to just work. I would say that this should be the minimum requirement for a professional. Taping a broken wing on a falling airplane may be a necessary emergency measure but as soon as the airplane has landed you should fix the issue in a permanent way.
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

##### Old habits die hard
I've used several programming languages in my life: Basic, Pascal, C, Php, JS, Java, Objective C, but the one I've been using the most, in the last years is Python. 

Why Python? Well, the first reason that comes to my mind is that since I'm not so closely involved in the daily coding process anymore, so when I do usually it's for either:
- Building a tactical tool with few to zero strings attached (e.g. cleaning a dataset or putting up a quick webservice for a PoC)
- Working on some pet project (I'll eventually pitch one of them in another post)

So usually no teams or codebases to comply against unless I choose to, and no particular technical boundaries.
Furthermore I don't do this as a regular activity, so I need something that is robust but even easy going and somewhat forgiving.
Python fits the role perfectly, you can do pretty much anything with it, even if it won't guarantee top notch performances but most of all you can pick it up after months of inactivity and feel at home right away, being productive in minutes.

In a way I got used to that cozy and familiar environment that Python was offering and in IT being in your comfort zone too much usually is up to no good. To put this under another perspective, I've been practicing martial arts for the last 20 years, over time I've met a lot of interesting people from different backgrounds and I tried to learn something from each and everyone of them, well once I met a Karate instructor who told me one thing that fits this situation perfectly: *Comforts kill you*. 

##### Pointers!!!
I discovered C during a university course (or rather a lab) that was about networks and afterwards I used it quite a bit, mostly for fun. Two of the most remarkable things I did with C was a Chess program for my bachelor degree final thesis and an extension for a Ray Tracer that allowed it to render Julia sets using quaternions. The following images were rendered (almost 12 years ago) with that extension.
![Julia sets over quaternions](/images/julias.jpg){:width="75%" height="75%" .center-image}



##### The last surprise
When you come to Go from a different background (as I did), while learning Go you'll have a lot of "what the heck!" moments. This happens because, as I said not only Go is a beast of its own but because it does things in its own way and it require you to adapt as a developer to that mindset.

That's not a bad thing per se but I admit that the first impact may be a thing to deal with. I had to reconsider some habits that with a new language wouldn't fit anymore, like the flexibility with types that Python allows.

Another major thing, at least for me, is that Go isn't particularly object oriented in the conventional sense, since it has no method overriding, inheritance or objects. 

I don't want to enter now in this subject but just to give a quick sketch:
- uses  `struct` to represent the state of entities and methods to describe behaviors instead of using a class for both
- follows the rule of thumb to favour composition over inheritance 

<!---
Here are some of the things that struck my attention so far:
1. Source code formatting is enforced X
2. Every variable not assigned to a value get the `zero` value of its own type
3. There is only one looping keyword, which is `for`, that can be used in 4 different ways according to your needs X  
4. Variable's visibility is related to the block it is in, which mean that a variable can be *shadowing* another with the same name in a containing block
5. Go uses pass by value
6. There is no such a thing as automatic type conversion or automatic type promotion, so if you try to sum a `uint32` and a `uint64` you will get an error, also be aware that the `int` type varies upon the architecture (32 vs 64 bit)
7.  There are lots of situation in the book where you will find words such as "If you find yourself needing to use fallthrough, try restructure your logic to remove the dependencies between cases" or "However, the need for a break statement (in switch cases ndr) might indicate that you are doing something too complicated. Consider refactoring you code to remove it"
8. It has goto
9. 
--->
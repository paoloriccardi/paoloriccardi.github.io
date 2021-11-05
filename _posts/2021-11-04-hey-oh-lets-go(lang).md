---
title: Hey Oh, Let's Go (lang)
layout: post
categories: Software_Development Programming_Languages
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: I finally gave it a chance and I started to study Go. I've been programming more or less continuously for the latest 20 years or so and thus I gathered some experience with various programming languages. Yet Go felt different from the first impact, here are the first few things that struck me. 
---

##### What is Go
If you've been in computer science long enough you have seen a lot of new kid on the block. Some of them eventually proved the test of time, while the less fortunate ones were put in the buzzword closet, where they wait for their time to shine again.

[Go](https://golang.org/){:target="_blank"} came out at Google almost a decade ago, it was announced in 2009, and it quickly become the next cool thing. In a few years everybody wanted to put it on their resume so badly since it was seen by many as the *language for the cloud*.

###### Wow
Let's go with small steps.
If you ask what's Go, that's the answer you get on its official website: *Go is an open source programming language that makes it easy to build simple, reliable, and efficient software*. 

###### You had my curiosity now you have my attention
Let's add that Go didn't come out of the blue. It is often referred as a C-like language and indeed among its ancestors there is the C language, as well as [CSP](https://en.wikipedia.org/wiki/Communicating_sequential_processes){:target="_blank"} and Pascal.

This rich heritage brings some interesting things to the mix, such as it's both a compiled and statically typed language, but another key aspect is its powerful set of primitives for concurrency derived from CSP. 

So it should be a language for great performances, perfect for networking and concurrency, easy to read with a minimum background and also easy write as long as you follow its tenets.
Anyway be warned, if you come from either an OO Language or a dynamically typed language you may need some time to get used to its way of doing things.

##### Essential bibliography
A couple of days ago, I picked up the excellent [Learning Go](https://www.oreilly.com/library/view/learning-go/9781492077206/){:target="_blank"} by Jon Bodner from my backlog of books and I decided to give it a try. It's very up to date and it's" focused on what the author calls an idiomatic approach, which means do things the Go way, speak the "Go language" without any foreign accent. As you will see reading the book, keeping it clean and orthodox is one of the mantra of Go. So forget your favourite Javisms, like going heavy on OO programming for structuring code, or all your Pythonic niceties, like automatic type conversion.

I think the idiomatic element is very important in every language in order to be able to fully leverage its potential but it become paramount in saving you a lot of frustrations for a language like Go where even the style of code formatting which the programmer can use is enforced

For example, are you the kind of person that put curly brackets right at the end of the method declaration or at the beginning of the newline? In Go you don't have this choice, one of the two gives a compiling error. 

```go
func main()
{
    fmt.Println("This is not valid in Go!")
}
```
Another great book which is worth mentioning and from which I'm sneak peaking from time to time, is the classic [The Go Programming Language](https://www.gopl.io/){:target="_blank"} by Alan A. A. Donovan and Brian W. Kernighan. Yes, that Brian W. Kernighan.

##### Standardization and enforcement, a possible explaination
To be honest, if you come from other languages, things like the one I described above can be a little bit of a shock. Furthermore let's be honest, we like to think ourself as artists of code and serialization and standardization sounds more like industry than like art.

On the funny side, let's not forget that the argument of spaces vs tabs can break relationships as discussed in a famous [Silicon Valley episode](https://www.imdb.com/title/tt5218484/){:target="_blank"}... by the way, in the Go universe it's tabs (and I agree on that specific tenet).

There are many things that are peculiar in Go, but the "forced standardization" is the one that got me first and after thinking about it I think there is a reason, or at least a possible explaination, for removing these kind of choice from the availability of the programmer. 

Go was born as a programming language in context where the codebases as well as the number of teams and people inside them, were (and still are) huge for the average software engineer standards. 
So it can become an issue if any programmers will have to deal with the idiosincracy of the others in terms of coding styles and code formatting. To reduce entropy, Go also reduces the number of keywords available, so if you need a looping block you have `for`, you won't have even `while` and `foreach`.

This idea make sense even if you think about another aspect, the growth of a Project often comes with the necessity of increasing the head count for development, operations, maintenance and so on. This means hiring, retraining/reskilling and replacing lots of new people that will have to hit the ground running.

##### My background
I've used several programming languages in my life: Basic (yes, I'm that old), Pascal, C, Php, JS, Java, Objective C, but the one I've been using most lately is Python. 
The first reason that come to my mind is that since I'm not so closely involved in the coding process anymore, when I have to code, I can just pick something to get the job done. The common reasons for me to open an IDE is:
- Writing a blog post (such this one)
- Build a tactical tool with few to zero legacy (e.g. cleaning a dataset or putting up a quick webservice for a PoC)
- Work on a pet project (I'll eventually pitch one of them in another post)

So usually no teams or codebases to comply against unless I choose to, and no particular technical boundaries.
Furthermore I'm not coding every day of the week, so I need something that is robust but even easy going and somewhat forgiving... just like Python. You can do pretty much anything with it, even if it won't guarantee top notch performances and you can pick it up after months of inactivity and be productive in minutes.

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
---
title: Hey Oh, Let's Go (lang)
layout: post
categories: Software_Development Programming_Languages
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: I finally gave it a chance and I started to study Go. I've been programming more or less continuously for the latest 20 years or so and thus I gathered some experience with various programming languages. Yet Go felt different from the first impact, here are the first few things that struck me. 
---

##### Introduction
If you've been in computer science long enough you have seen a lot of new kid on the block, hot technologies that eventually proved the test of time or less fortunate one that sinked in a sprawling see of buzzwords waiting for their time to shine again.

So when the industry comes out with the new "cool thing" that everybody want to put on their resume you start being cautious. [Go](https://golang.org/){:target="_blank"} has been around for a while if we consider that it was first announced in 2009 and it is continuously getting momentum.

So I finally did it, I picked up the excellent [Learning Go](https://www.oreilly.com/library/view/learning-go/9781492077206/){:target="_blank"} by Jon Bodner from my backlog of books and I gave it a try. I've also cleaned some dust from the classic [The Go Programming Language](https://www.gopl.io/){:target="_blank"} by Alan A. A. Donovan and Brian W. Kernighan. Yes, that Brian W. Kernighan.
Anyway the first has been my favourite reference trying to understand the language for two reasons, the first one is pretty obvious, it's more recent. The second one is more subtle... it has an "idiomatic" approach to the language, it means that it teaches the way you're supposed to write Go, as a Go programmer, not as a Python/C/Cobol/whatever programmer who's temporarily writing Go code.

It's fairly common to spot things like "In the language X you can also do things in a sort of language Y kind of fashion", javisms in Python or vice versa, well this is not the case, not with this manual and not with Go anyway.

Go has it's own way of doing things and the margin of choice left to the programmer in terms of coding style is reduced. 
For example, do you put curly brackets right at the end of the method declaration or on the newline? In Go you don't have this choice, one of the two returns error at compiling time. 

```go
func main()
{
    fmt.Println("This is not valid in Go!")
}
```

This is pretty surprising if you come from a world where people deciding between spaces and tabs can break relationships as discussed in a famous [Silicon Valley episode](https://www.imdb.com/title/tt5218484/){:target="_blank"}... by the way, for Go fmt it's tabs (and I agree on that specific tenet).


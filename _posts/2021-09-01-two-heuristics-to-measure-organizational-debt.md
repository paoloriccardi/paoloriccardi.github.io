---
title: Two heuristics to measure entropy in Organizations
layout: post
categories: Org
permalink: /Linenoise/:categories/:title/
description: 
---
##### Business Processes
A business process can be defined as a set of structured activities that, once completed, contribute to the accomplishment of a business goal or alternatively to the delivery of a service or a product to a customer.
The key word here is *structured*, every activity gets input and returns outputs from and to other activities, a common business process model is similar to a graph.

Things don't always go as planned, so behind the official paths there are detours because of workaround and exceptions and as time goes by, those detours proliferate.
Indeed processes evolves like they are a living things, they mutate. 

That's why processes can be a very complex subject of study and analyze, even using data driven approaches like [process mining](https://en.wikipedia.org/wiki/Process_mining){:target="_blank"}. Anyway, for the sake of this post it will be enough to start from a simple concept, just like every attrition in a machinery generates inefficiency (e.g. under the form of overheating) even process attritions generate inefficiency. Just like engines, even processes may have their bad omens.  

##### Bad Omens
If you look around in any Department of a relevant sized company, you'll probably be able to find an abundance of: 
1. Spreadsheet files 
2. Email communications

I know this may sound weird to people with a purely technical background but just take a moment and look at your Project Manager, your Line Manager, your head of department/head of sales, head of whatever... odds are he's in this kind of trouble every day of the week that ends with *Y*.

And if you look closely to not onrganizational roles, you will find something similar too... Everybody has a friend down in the engine room to tap when the k8s cluster is down and there is no time to go through the standard channels.

Of course you may work in a company that is not in this situation, well... good for you, I haven't seen many of them.

As you may have guessed by now, spreadsheets and emails are both bad omens.  

Some departments are so polluted with both that you won't be able to find a single process that's not relying to some degree on spreadsheet for project management, resource accounting, inventory management, sales reporting, order tracking or task lists and on emails for off-the-record communications when something diverges from the typical workflow (or sometimes even when everything is following the golden path). 

Don't get me wrong, spreadsheet and emails can be useful, if you're in trouble they will save your day again and again but their abuse is a clear signal that something is wrong. Why? Because they are workaround or tactical solutions at best and as they say *Unhappy the land that is in need of heroes*.

##### The Spreadsheet incident 
So I am saying that spreadsheets are evil, right? No, no, no.
The first spreadsheet software was called [VisiCalc]{https://en.wikipedia.org/wiki/VisiCalc} and it's impact on the computer industry in 1979 was huge.

Indeed spreadsheets have rock solid reasons to be widely used even today:
- easy to use for users who don't have a programming background
- perfect for quick and dirty tactical tools 

Sometimes it's totally fine to use spreadsheets as long as one is aware of their limitations (e.g. number of rows) and of the unintended consequences.

Let's assume every project manager uses spreadsheets to record project schedule and produce gantt diagrams. Now put yourself in the shoes of the department manager, maybe you want to know how many projects are active in your department. What do you do? You will have to ask every PM to brief you or to send you their project plans. Chances are you're going to face a long day staring at a screen and talking to people just to figure it out. Not to mention the fact that every spreadsheet you'll receive will likely use different styling, conventions, etc...
And what if you wanted to know about last quarter projects too? Again, PMs should search for the right version (ahah, that's funny) of the right file and send it to you.  

In other words, every PM has created his own private information silo and the worst part is that the creation, update and maintenance of those siloes didn't come cheap in terms of time consumption.

What if instead of project plans we wanted to check sales, which were tracked by our sales managers the same way? Again we will have to run through any single file in any single laptop, wherever they may be.

Do you see the recurring theme here?

Let's take our poor PM as an example but be aware that this habit is spread well beyond them, for example I've seen a Christmas holiday plan, with skill coverage per application area and services done with tons of spreadsheets.
Why a PM would invest time producing her own project management tool in the first place? Well there could be several reasons the first that come into my mind is that she doesn't have alternatives.



But nonetheless spreadsheet are commonly used, why? 
Well here it comes that strange noise from the engine you should be aware of, you don't know what's the problem but you know it's not good. Proliferation of spreadsheets may have different causes, among which:
- Your company doesn't have the right IT tools 
- Your company's IT is so full of work just trying to keep the lights up that people prefer the do it yourself approach
- The IT tools that support the process have blind spots
- People hide things
 
In other words, why do you need to trade emails with your colleague over a bugfix? Because something is not clear in your tracking system for example, or maybe because you need to notify your manager that you're going to take care of it and you will need some time. On the other hand why do you need to use a spreadsheet to track a project or to record this quarter prospects? Because you don't have any other IT tool to support you. 










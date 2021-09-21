---
title: Two heuristics to measure entropy in Organizations
layout: post
categories: Org
permalink: /Linenoise/:categories/:title/
description: In every complex organization there are two common artifacts that are omnipresent, emails and spreadsheets, right? Well what if I tell you that their presence in high volumes is a clear symptom that something is wrong. We can call it a heuristic if you want or process consultancy wisdom, either way in this post I'll try to explain in simple terms why they apply.
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
So I am saying that spreadsheets are a thing of evil, right? No, no, no.
The first spreadsheet software was called [VisiCalc](https://en.wikipedia.org/wiki/VisiCalc){:target="_blank"} and it's impact on the computer industry in 1979 was huge.

Indeed spreadsheets have rock solid reasons to be widely used even today:
- easy to use for users who don't have a programming background
- perfect for quick and dirty tactical tools (I use them at the beginning of every football season to draft my fantasy-football players)

My job as Architect taught my one big lesson: it's always about tradeoffs. Sometimes it's totally fine to use spreadsheets as long as one is aware of their limitations (e.g. number of rows) and of the unintended consequences.

For instance...

Let's assume in your company every project manager uses spreadsheets to record project schedule and produce gantt diagrams. One day or another you may want to know how many projects are active in your department. You will have to ask every PM to brief you and to send you their project plans. Chances are you're going to face a long day staring at a screen and talking to people just to have an idea. Not to mention the fact that every spreadsheet you'll receive will likely use different styling, naming conventions, etc...
And what if you wanted to know about last quarter projects too? Again, PMs should search for the right version (ahah, that's funny) of the right file and send it to you.  

In other words, every PM has created her/his own private information silo and the worst part is that the creation, update and maintenance of those siloes didn't come cheap in terms of time consumption.

What if instead of project plans we wanted to check sales? If they were tracked in the same way, we will have to run through any single file in any single sales manager laptop, wherever they may be.

Do you see the recurring theme here?

Here's the million euro question, why someone would invest time producing her/his own tool (e.g. for project management) in the first place? Well there could be several reasons and understanding them is not an easy job and it's beyond the scope of this post.
My point here is that spreadsheets pollution is a symptom that something isn't quite right and, whatever the root cause may be, the outcome produced typically have negative consequences on process performance and on the overall organization.

##### Let's talk about emails now
The reasons to consider an excess of email messaging a bad omen is pretty obvious. Beyond the smalltalk pleasantries, email messages usually are about information, either provided or requested. In either case it represents an integration to an information context that, appartently, is not clear enough by itself. For example, one day you are paged by your relevant one with the request *"please buy Milk"*, if you have to text back something like *"which brand? Low-fat or whole? Soy or cow?"*, we can presume that you are missing part of the context (e.g. your relevant one doesn't stand whole milk).

If a similar situation occurs (and it does) in business processes this may imply several things, just to mention a few: 
- people are not empowered enough to make decisions by themselves
- the procedure/workflow itself is not clear to the actors
- unplanned cornercases and exceptions
- missing information for a given request

Whatever the reason(s) you may have some issue to address but in the meantime you will have an obvious outcome: it will be very difficult to backtrack anything since the communications were done either totally or partially off the system and off the records. Good luck trying to trace back what happened. 

##### Conclusions
What's really missing here is a cohesive environment where data are shared and communications are integrated in the workflow. It may look simple, but beyond the more common cases you cannot always take for granted that you have the right tool to support every specific piece of task inside the process.

Be aware though, because usually tools cannot fix a process by themselves, even though they may help the transition to a better process. Most important of all you should start from the process and work your way to the it tools to support it, not vice versa. 

Applying some computer science common sense we can say that you won't fix a quadratic sorting algorithm simply by putting a better CPU, you will need to rewrite the algorithm using a different approach. 

In other words you need to sit down and reconsider the problem you were trying to fix in the first place... maybe yesterday your business process was just fine for the job but now perhaps the scenario is different and you will need to adapt. 









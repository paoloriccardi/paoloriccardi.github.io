---
title: Building OAS3 compliant, Rest API in Python, using FastAPI
layout: post
categories: Dev
permalink: /Linenoise/:categories/:title/
description: A Rest API is a common element of many web services, every programming language and every framework has its own solution to develop a Rest API, I was looking for a fast way to build a lightweight yet OAS compliant API in Python and so I found... FastAPI.
---

I've been looking around for a fast way to build Rest API for a work project. Recently, in a similar situation, while developing a pet project, I decided to use [Flask](https://flask.palletsprojects.com/en/2.0.x/){:target="_blank"} for the purpose. Flask is a lightweight web framework for Python, it's simple, it does its job, but in my opinion it doesn't provide, out of the box, all the elements that one would need building a modern Rest API for real. 

Does that mean that Flask is no good for Rest API? Not at all. It just means that you'll have to spend some extra time to do it, for example.

All in all I was looking for a quick way to build an unbloated and lightweight Rest API and I wanted it to be compliant with the last version of [OpenApi](https://spec.openapis.org/oas/v3.1.0){:target="_blank"} and last but not least, I wanted it to be easily and fully documented.

I spend a whole afternoon looking around and I came across a plethora of alternatives for Python but none of them looked the right pick: flask-restplus, flask-restful, Django, Tornado etc... to make things worse I a huge number of outdated tutorials, which made difficult for me to grasp the state of the art at the moment. I almost gave up and started considering other languages, my idiosyncrasy for JS was leading me straight into the arms of Go, where concurrency, curly brackets and structs await me.

Lucky me, I found [this article](https://rapidapi.com/blog/best-python-api-frameworks/){:target="_blank"} which contains a useful, broad picture of the general topic *Python and Rest*  and in the process, showcased many different alternatives, one of them being FastAPI. 

I decided to visit the [project website](https://fastapi.tiangolo.com/){:target="_blank"}, it claims to be fast to execute (as fast as Go and NodeJS), fast to code, robust and standards-based. It sounded incredibly appealing. So what I said to the god of Go was... Not today.

Even better, on the same website I found very straightforward, complete and well done Tutorial / User Guide. It took me less than a working day to be in the condition to complete a fully working Rest API, with a simple CRUD, backed by an SQL server for persistence.

One of the things that I enjoyed the most was the automatic creation of documentation via Swagger UI. Which means the ability to test each endpoint and to document it for other developer who are going to actually use it. 




---
title: Building OAS3 compliant, Rest API in Python, using FastAPI
layout: post
categories: Dev
permalink: /Linenoise/:categories/:title/
description: A Rest API is a common element of many web services, every programming language and every framework has its own solution to develop a Rest API, I was looking for a fast way to build a lightweight yet OAS compliant API in Python and so I found... FastAPI.
---

I've been looking around for a fast way to build Rest API for a work project. Recently, in a similar situation, while developing a pet project, I decided to use [Flask](https://flask.palletsprojects.com/en/2.0.x/){:target="_blank"} for the purpose. Flask is a lightweight web framework for Python, it's simple, it does its job, but in my opinion it doesn't provide, out of the box, every element that one would need in order to build a modern Rest API for the real world. 

Does that mean that Flask is no good for Rest API? Not at all. It just means that probably, you'll have to spend some extra time to do it.

To put it simply, I was looking for a quick way to build an unbloated and lightweight Rest API. Furthermore, since documentation and good standars are paramount when working with heterogeneous teams, I wanted it to be compliant with the most recent version of [OpenApi](https://spec.openapis.org/oas/v3.1.0){:target="_blank"} and use [Swagger](https://swagger.io/){:target="_blank"} out of the box.

I spent a whole afternoon looking around and I came across a multitude of alternatives for Python, it was a very discouraging puzzle of frameworks and extensions. To increase the overall confusion I found a huge number of outdated tutorials, which made difficult for me to quickly grasp the state of the art at the moment. 
At that point I almost gave up and started considering other options outside the Python world. 

Lucky me, I found an [article](https://rapidapi.com/blog/best-python-api-frameworks/){:target="_blank"} packed with useful informations, which brushed a broad picture of the more general topic *Python & Rest*, presenting several alternatives, one of them being FastAPI. 

I decided to visit the [project website](https://fastapi.tiangolo.com/){:target="_blank"}, it claimed to be fast to execute (as fast as Go and NodeJS), fast to code, robust and standards-based, all things considered it sounded incredibly appealing. 

##### ~~RTFM~~ Try the tutorial 
The thing that made me decide almost instantly for fastAPI is that on the project website I found immediately a very straightforward, complete and clear Tutorial / User Guide, rich of useful links to go deeper on specific topics.

Good documentation means that the developers cared for other human beings to _use_ their product and this is a thing I always appreciate, you know... being a human being myself.
So again, I strongly recommend you to [try it out](https://fastapi.tiangolo.com/tutorial/){:target="_blank"}. 

Retrospectively it was a good call since it took me less than a working day to complete a fully working Rest API, with a simple CRUD, backed by an SQL server for persistence.

Few words about what I got by the end of the basic user guide, roughly:
1. a main app, with 
    - the routes to the API endpoints and resources
    - basic error handling
    - different http methods, response type, body and path parameters
2. an sql-based persistance layer made of
    - a database (for the sake of the tutorial it's SQLite)
    - the crud operations on the database
    - the data models (via SQLAlchemy, defined as models in the tutorial)
    - the application models (via Pydantic, defined as schemas in the tutorial)
3. API docs which bring
    - simple, clear and complete documentation with little to no effort
    - the ability to try and test the endpoints as you go

##### Under the hood
FastAPI makes use of [starlette](https://www.starlette.io/){:target="_blank"}, a lightweight ASGI framework, which is typically served through an ASGI server implementation called [uvicorn](https://www.uvicorn.org/){:target="_blank"}. 

Data validation is a big topic with API, so to take care of all the data validation stuff, FastAPI makes heavy use of [Pydantic](https://pydantic-docs.helpmanual.io/){:target="_target"} which also helps when you have to define your own data model and pass it around, or converting it from the JSON contained in the body of a request. Most of the things you will be able to with a request after it hits an endpoint is empowered by pydantic. 

The tutorial uses [SQLAlchemy](https://www.sqlalchemy.org/){:target="_blank"}, so be warned since this may introduce some confusion between Pydantic Models and SQLAlchemy Models. Keep in mind that the firsts define a valid data shape (a schema), the seconds define (more or less) the sql tables that will represent the data.

##### Docker, yes you can
Deploying the service via Docker is pretty straightforward, you can [check the guide](https://fastapi.tiangolo.com/deployment/docker/){:=target="_blank"} for mode details. To be honest, my pick was to play it safe, using  `python:3.8` the official python image (based on the latest stable Debian release) and to add the packages I needed as requirements, mainly:  `setuptools`,  `fastapi`,  `uvicorn` and  `SQLAlchemy`.
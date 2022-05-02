---
title: How I did it, from mr. Html to dr. Jekyll
layout: post
categories: Software_Development
#permalink: /Linenoise/:categories/:title/
permalink: /Linenoise/:title/
description: The brief history of how and why I migrated my old html resume to GitHub pages, which by the way gave me the opportunity and the inspiration to add a small technical blog (which you are reading right now) using Jekyll. Neither DBs nor CMSs were harmed in the making of this blog.
---

In the recent years, my job responsibilities took me out of the active software development loop. So less then a month ago I decided to start a pet project, just for fun (more on this very topic in another post, hopefully). 

I started to set up the standard *paraphernalia*, which in my case consists of: VS Code with a couple of useful extensions, Docker for containers and, of course, Git. So as soon as the local environment was ready I logged in into my old Github account, I set up a new repo (which became soon three private repos and a public one) and I started coding quite happily. 

It took me a while, but as anybody with some experience in programming can testify, once you get in the zone it become rather natural, no matter how rusty your skills have become. 

When my inspiration for the new project cooled off just a little bit I started to realize that Github nowadays has more to offer than just simple version control, even with a free plan. So I started to look around.

The first thing that caught my attention was the ability to host a personal website per user (plus one per project if I'm not wrong) with [GitHub Pages](https://pages.github.com/){:target="_blank"}, rather hassle free. When I say hassle free, I mean that you're not supposed to update or maintain or worry about how your website is served.

I liked the idea to port my online resume, which was just a plain *html+css* website served by my old personal ~~server~~ VM, to GitHub Pages. Soon I realized I could do much more than this, thanks to [Jekyll](https://jekyllrb.com/){:target="_blank"} which, according to the author, is able to:
> Transform your plain text into static websites and blogs

One of the things that I missed in my previous resume was the possibility to drop in some content, articles, quick reviews about technical books I'm reading or pet projects.  

To sum up some of the pros:
- It's Free (as in free beer, free speech and free from hassles)
- Once you pick up the basics you can focus just on writing
- The process of content/code production, versioning and deploying is quite smooth
- The porting of my old *html+css* look and feel to Jekyll was a walk in the park
- Being able to blog without the burden of a CMS

##### Where to start?
Since I never had any contact with Jekyll before I had to start from the very beginning: what's Jekyll? Do I need to know Ruby to use it? How do I deploy a simple website and so on?
The official documentation is a good starting point, it comes with some useful [tutorial](https://jekyllrb.com/tutorials/convert-site-to-jekyll/){:target="_blank"}.

Theoretically you could just write your website according to jekyll standards and push it straight to github for publications, however to make things easier you should install jekyll (and Ruby) and use the command line to build the website, test locally and then eventually push it on GitHub, [here](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll){:target="_blank"}  is a good tutorial for doing this the clean way.

Some tips I collected along the way:
1. One you've built the basic layout structure, writing a pages and posts is just as simple as writing a `markdown` file, you just may want to specify in the `_config.yml` file your favourite md processor, highlighter and so on... 
2. For your own sanity, starting with a good [file structure](https://jekyllrb.com/docs/structure/){:target="_blank"} helps, a lot, since Jekyll will depend on it
    - One of those *magic* directory is `_data` where you can store `.yml` files for various purposes (f.e. defining the navigation menu) and retrieve them with something like this:
    ```
    for link in site.data.navigation 
        do_something
    endfor
    ```
    - Another one is `_site` where jekyll is going to put the generated html you will deploy, you can just put this directory into `.gitignore` if you're going to publish on GitHub Pages and forget about it 
3. Get familiar with the `Front Matter` (a sort of yml prefix included in pages and posts) it may save your day
4. The layouts allow you to concentrate on writing contents rather than tags, they can be composed effectively with inheritance and are basically html files with some space for contents, that can be enriched with some templating magic (f.e. loops, which are useful when you want to display your blogroll)
5. It is possible to use your own domain instead of `<username>.github.io` it took some minute for the DNS to propagate but it worked like a charm, following this [tutorial](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages){:target="_blank"} 



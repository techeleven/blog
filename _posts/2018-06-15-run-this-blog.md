---
layout: post
title: "Run this Blog"
date: 2018-06-15 09:26:14 +0100
tags: blog 
lang: en
author: matthias
---
Run this Blog
=============

How is this [blog] working form a technical point of view?

## Blog Infrastructure

This blog is running with [jekyll].

> Transform your plain text into static websites and blogs

## Hosting

The blog is hosted at github as [github page].

## Local Test Environment

To run this blog on a local enviornment we use a Docker container. In detail: just the preconfigured Docker container [jekyll-docker] 

As described in the documentation we wrap this in a docker-compose file:

    version: "3"
        services:
        site:
            command: jekyll serve    
            image: jekyll/jekyll:latest
            volumes:
            - ./:/srv/jekyll
            - ./vendor/bundle:/usr/local/bundle
            ports:
            - 4000:4000
            - 35729:35729
            - 3000:3000
            -   80:4000

Therefore you can just start everything by `docker-compose up` respectively `docker-compose start`.

Rebuild the blog is done by `docker-compose exec site jekyll build`.

Please see also the [how to use] section from [jekyll-docker].


[We]:               https://tech11.com
[blog]:             https://blog.tech11.com
[jekyll]:           https://jekyllrb.com/
[github page]:      https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/
[jekyll-docker]:    https://github.com/envygeeks/jekyll-docker/blob/master/README.md
[how to use]:       https://github.com/envygeeks/jekyll-docker/blob/master/README.md#usage-4
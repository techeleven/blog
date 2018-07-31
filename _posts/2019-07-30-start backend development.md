---
layout: post
title: "Start Backend Development"
date: 2018-07-30 15:03:33 +0200
tags: blog 
lang: en
author: matthias
---

##Preconditions

* Create a Bitbucket account
* Enable Bitbucket user to related projects
    * Access to policy
    * Access to journal
    * Access to tech11-release-parent
    * Acesss to tech11-platform-parent
* Install JDK 1.8.x
* Install Maven 3.x
* Install Docker
* Install eclipse + JBoss Tools plugin
* Install Wildlfly


## Test

    cd %SCM_DIR%

    git clone git@bitbucket.org:techeleven/journal.git
    git clone git@bitbucket.org:techeleven/tech11-release-parent.git
    git clone git@bitbucket.org:techeleven/tech11-platform-parent.git
    git clone git@bitbucket.org:techeleven/policy.git

    cd %SCM_DIR%\tech11-release-parent
    mvn clean install
    cd %SCM_DIR%\tech11-platform-parent
    mvn clean install
    cd %SCM_DIR%\tech11-journal-parent
    mvn clean install
    cd %SCM_DIR%\tech11-policy-parent
    mvn clean install

## DB setup

    docker run --name tech11-mongo -p27017:27017 -d mongo:3.4
    docker exec -it tech11-mongo /bin/bash

    //stop 
    docker stop tech11-mongo
    //start 
    docker start tech11-mongo
    //kill - remove
    docker rm -f tech11-mongo



[tech11]:   https://tech11.com
[cloud based]:   https://tech11.com/en/cloud-solutions

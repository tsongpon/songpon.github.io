---
layout: post
title: How to Install Gradle
comments: true
---

Gradle is automate build tools/dependency management  build on concept of Maven and Apache ant and uses Groovy-based domain-specific language (DSL) instead of the more traditional XML form of declaring the project configuration this make Gradle become a powerful tool. This post will introduce you how to install Gradle on your machile.

## Prerequisite
- JDK : You need Jave Development Kit(JDK) installed on your machine.
- Internet connection for downloading Gradle and project dependencies.

## Download Gradle
You can download Gradle [here](https://services.gradle.org/distributions/gradle-2.4-all.zip)
## Install Gradle
After download finish you will get one zip file on your download directory file name will look like gradle-x.x-all.zip (x.x is version number) to install Gradle you need to

1. Extract (unzip) gradle zip file, in our case I will extract zip file to be a directory name `gradle`
2. Move directory from 1. to appropriate location, in our case I will move to `/usr/local/` ,so after move I will have directory `/usr/local/gradle` on my machine
3. To be able to run gradle in everywhere we need to add Gradle directory on our `PATH` variable by open `~/.profile` (I am on mac OSX) with your prefer text editor in this case I will use vim
        vim ~/.profile
append this two lines
       export GRADLE_HOME=/usr/local/gradle
       export PATH=$PATH:$GRADLE_HOME/bin
save the file and use `source` command to reload new environment variable
       source ~/.profile
(in some case you need to open new terminal session after `source`)

## Test Your Installation
You can test your gradle Installation by run this command `gradle --v` if your Installation is correct you will get result look like this

    ------------------------------------------------------------
    Gradle 2.4
    ------------------------------------------------------------

    Build time:   2015-05-05 08:09:24 UTC
    Build number: none
    Revision:     5c9c3bc20ca1c281ac7972643f1e2d190f2c943c

    Groovy:       2.3.10
    Ant:          Apache Ant(TM) version 1.9.4 compiled on April 29 2014
    JVM:          1.8.0_45 (Oracle Corporation 25.45-b02)
    OS:           Mac OS X 10.10.4 x86_64

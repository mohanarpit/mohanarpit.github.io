---
layout: post
title: Ubuntu Setup
published: true
---

The excitement of a new OS or new laptop is palpable. But installing applications that you need
to get work done can involve a little drudgery. I formalized the setup in the form
of a shell script to ensure that most of the basic applications that I need are
installed automatically. You can find the complete script [here](https://github.com/mohanarpit/Ubuntu-Initializer).

All you need to do is copy the script install_script.sh and execute it. Some
of the applications that it installs are:
* Source Control: Git, SVN
* Languages: Python, Java, Php, Go, Nodejs
* Editors: Atom
* Databases: Mysql
* Servers: Tomcat, Apache2
* Utilities: Tmux, fail2ban, jq etc.

It even creates your key pair, if you don't already have one.
As you can see, it's geared towards web developers but nothing stops you from
commenting out applications that you don't wish to install.

Over the years, this script has saved me & my team from a lot of hours of hunting and
installing basic applications.

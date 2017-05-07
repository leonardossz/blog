+++
author = ""
menu = ""
share = true
image = "images/productivity.jpg"
tags = ["Software Development","Productivity Tips"]
draft = false
comments = false
slug = "12_tips_about_software_development_productivity"
title = "12 tips about software development productivity"
date = "2017-05-07T21:53:00+02:00"

+++

__Disclaimer__: This is my opinion and how I learned to deal with the everyday pressure to be more and more productive. For a experienced professional this may sound obvious ;)


If you're looking for an article about programming productivity and metrics like COCOMO, Function Points or Value-Based Software Engineering than you can leave now. [Here is what you're looking for.](https://en.wikipedia.org/wiki/Programming_productivity)

__Assumption__: You are a _young_ developer and your main environment is a _Unix-like_ computer operating system.

Now let's cut to the chase.

* __Use a decent IDE__ or at least learn effectively how to deal with its idiosyncrasies. Even the paid ones has its own quirks and bugs. Think seriously on how much time you spend with the setup of a new project, buggy plugins, dependency resolution problems, speed of debugging tools, slow code competition and so on. Most of the time I am using IntelliJ or PyCharm.

* __Use a decent Text Editor__. Sometimes an IDE is too much to edit a small configuration file or build a small program in Python. I recommend to take a look on [Sublime Text Editor](https://www.sublimetext.com/). There are tons of syntax highlighters and nice features to speed up your job, like regex search, distraction free mode, split editing etc.

* __Have a sane environment__. Don't work with a broken environment. The first thing you should know about the code you're about to modify is its last state. Be sure all you're seeing is running smoothly like tests, integrations etc or at least the buggy behaviour was already there (and probably you will fix it). How do you add more code without knowing if it was working before?

* __Upgrade only if necessary__. To keep a sane environment you have to trust on all updates you're applying. Don't blindly update your IDE or Operating System just because there's a new version, take a look on the what's new section and if it's a minor upgrade look for the fixes and see if you are being affected. Updates takes time and if you need to revert will take even more time.

* __Isolate your working environments__. If last point is not feasible or you work on several projects or even different versions of the same project than you need a good control of your environment. Leverage tools like [Docker](https://www.docker.com/), [Python VirtualEnv](https://virtualenv.pypa.io/en/stable/) in case of Python of course or even [Virtual Box](https://www.virtualbox.org/). This also helps to have a sane environment, avoid changing things on your own operating system.

* __Essential Cmd-line tools__: Have you tried to load a big text file on your IDE text editor, Sublime, Atom or gedit? Probably crashed or it was so slow that you gave up. If you're dealing with huge files use the basic tools like [head](https://en.wikipedia.org/wiki/Head_(Unix)), [tail](https://en.wikipedia.org/wiki/Tail_(Unix)) to have a sample of the contents. Also learn how to leverage [awk](https://en.wikipedia.org/wiki/AWK), [sed](https://en.wikipedia.org/wiki/Sed), [split](https://en.wikipedia.org/wiki/Split_(Unix)), [grep](https://en.wikipedia.org/wiki/Grep) and [less](https://en.wikipedia.org/wiki/Less_(Unix))

* __Don't repeat yourself__. Master your terminal tool and take a look on [Oh-My-Zsh](https://github.com/robbyrussell/oh-my-zsh). Learn how to quick search back and forth on your command history, tipically `CTRL+R` will trigger the _reverse-i-search_. Sometimes is better to transform your shell steps into a script (Bash, ZSH etc). Creating _aliases_ are always useful on those cases too.

* __Use a window manager and/or terminal multiplexer__. This is complementary to the last advice. This will give you the ability to start several virtual consoles and access all open login sessions within a single terminal window. The oldest one is the [GNU Screen](https://en.wikipedia.org/wiki/GNU_Screen). My favorite is [Byobu](http://byobu.co/).


* __There is always a validator or linter out there__: This often applies for the text formats you're dealing with, to name a few: [JSONLint](https://jsonlint.com/), [xmllint](https://linux.die.net/man/1/xmllint), [Code Beautify](http://codebeautify.org/xmlvalidator), [Hoconlint](http://www.hoconlint.com/).

* __Have a second or bigger monitor__. If you're on a desktop a bigger or even dual monitor is very effective to speed up your job because most of the time we are reading some documentation and coding. If you're using a laptop I'd say you must have a monitor to extend your working area.

* __Versionate everything__. If you're experimenting some approach for a hard problem may be worth to keep all history of your tries. If the code is something expendable you don't need to push into the cloud is just a local repository, `git init` and you're done and safe to freely experiment without the fear to lose something in between.

* __Use the Cloud__. If your disk fails badly what happens? Is not just code that you __must__ be pushing everyday but anything you have that is valuable for your work like the settings of your IDE, Maven settings, test files, `.rc` files like your `.zshrc` or `.bashrc` in your home dir and even some configuration in `/etc`. Take a look on the [rsync](https://en.wikipedia.org/wiki/Rsync) tool, Dropbox or even the Amazon S3 solution. It's not so expensive for small but critical valuable files. The amount of time required to restart working may be huge if you lost everything out of the blue.


Thanks for reading. 
---
layout: post
title: Installing Node
---

Being a node developer, I have installed node on quite a few machines a number
of times. I have come up with a "preferred" way of doing it that gets round 
a few common problems people have with setting up a good environment, so I
thought I would share.

## Version manager

[nave](https://github.com/isaacs/nave) is my version manager of choice. Its a
simple bash script and nothing more. Its the most lightweight and the best in my
opinion.

Install it (to /usr/local/bin or somewhere else in your $PATH) like this:

```sh
sudo sh -c 'curl -fsSL https://raw.githubusercontent.com/isaacs/nave/master/nave.sh > /usr/local/bin/nave && chmod a+x /usr/local/bin/nave'
```

And then use it like this:

```sh
sudo nave usemain stable # downloads the latest stable version
sudo nave usemain latest # downloads the most up to date version
# You can also do version numbers
sudo nave usemain 0.10.40
# And you can run scripts in subshells
nave use 0.12.0 node example.js
```

## Setting up npm correctly

By default, doing npm install -g will write to /usr/local/bin/bin, and you will
have to sudo that command every time you run it. Personally I don't like the
idea of giving everything I install through npm sudo access on my system by
doing this. So I get round this by installing my npm global packages somewhere
else.

In your ~/.npmrc, you can do:

```
prefix = ~/npm-global
```

Everything you install with npm install -g from then on will no longer
require sudo, and the above problem goes away. You will need to make sure that
~/npm-global/bin (or wherever you decide to point it) is in your path.

If you don't do this and you ever need to install a global module that isn't
on npm, but is on github and is not public, you will get a permissions error
back fomr github because your system will try to use roots ssh keys. Its
unlikely you will ever have this problem.

## Turn on some logging

In more recent versions of npm, a lot of the logging that you used to get when
installing modules has been turned off. I recommend turning it on, partly
because it gives the illusion that npm is faster than it actually is, but also
if something goes wrong you aren't forced to open or cat the produced
npm-debug.log file.

You can turn on info level logging like this in your ~/.npmrc:

```
logLevel = info
```

## Managing your npmrc's

Where I work we have a few private modules that aren't on the public registry
and are on our own private one that is only accessible via our VPN. This means
that I need to manually go and change which registry npm is pointing at
every time I am not in the office or not on the VPN.

There is a tool called [npmrc](https://www.npmjs.com/package/npmrc) that gets round this problem. It allows you to
keep multiple npmrc files in ~/.npmrcs and switch between them. You can install
it with npm like this:

```sh
npm install -g npmrc
npmrc # run this to setup the ~/.npmrcs dir
```

Then you can start creating npmrcs, and running npmrc will display them. The
output of that command for me is:

```sh
Available npmrcs:

 * clock
   default
```

And I can switch between them using:

```sh
npmrc clock # changes my ~/.npmrc to ~/.npmrcs/clock
```

I can keep the correct registry configuration in each file and switch between
them with ease. It does mean however that you will have to duplicate some
settings (like logLevel and prefix) across the different files, but when you
have done this once you will never need to touch them again.

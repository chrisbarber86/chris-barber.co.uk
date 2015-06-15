---
title: My Development Setup
thumb: my-development-setup-thumb.png
author: Chris
---

Over the past 7 years I've been honing my development toolkit to ensure I have
a reliable and easy to use setup that enables me to be productive. This post 
takes a look at my current development setup, from the hardware, to my terminal
setup, to my trusty editor software.

## Hardware

I've been a big fan of Apple hardware for a long time now, both at home and at
work I'm running a Macbook Pro (13" at home, 15" at work) and both are plugged
into 27" Cinema Displays. There is just something nice about being able to use
the cinema display as a dock for network access, USB connections etc.

On top of that I use the full size mac keyboard and the wireless magic mouse.

![home setup](/images/home-setup.jpg)

## OSX Environment

To ensure I have a happy time working with OSX I make use of the fantastic
[homebrew](http://brew.sh/) package manager. This makes installing and managing
packages a breeze, it's also really well supported and maintained giving me
a lot of confidence in what it delivers.

Right now I have quite a few packages installed, some are dependencies for
normal development, others are specific to things needed for work projects.

```
apple-gcc42     cmake       icu4c     libpng            node
pkg-config      ruby-build  autoconf  elasticsearch     imagemagick
libtool         openssl     qt        terminal-notifier automake
freetype        jpeg        lighttpd  rbenv             tmux
bash-completion git         libevent  mysql             phantomjs
```

## Managing Ruby Versions

For managing Ruby I make use of [rbenv](https://github.com/sstephenson/rbenv) by
[Sam Stephenson](https://github.com/sstephenson). This allows me to have multiple
versions of ruby installed at any one moment and easily switch between them for
a local folder or globally on my whole mac.

## Terminal App

Whilst the terminal in OSX is great, I prefer to use [iTerm 2](https://www.iterm2.com/).
I think this is mostly a personal preference thing, but it does provide some
good shortcuts which make it a lot easier to use. It also comes with Split Panes
and better support for colours and the mouse.

![split terminal window](/images/terminal-split.png)

## Bash Prompt

To spruce up the default bash prompt in OSX, I have a custom bash file which I
initially based on [@damian's](https://github.com/damian/) [.bash_profile](https://github.com/damian/dotfiles/blob/master/bash_profile)

The result is a prompt which is in colour and displays the current branch when
in a git repository along with an asterisk to denote if the current branch is
dirty or not.

![bash-prompt](/images/bash-prompt.png)

There are also several useful short commands for navigating folders, working
with git and bundler.

#### Navigation

* `ll` = `ls -l`
* `lla` = `ls -la`
* `..` = `cd ..`
* `...` = `cd ../..`
* `dev` = `cd ~/development/$1` (where $1 is any path provided after dev)

#### Git

* `g` = `git`
* `gs` = `git status`
* `ga` = `git add`
* `gb` = `git branch`
* `gc` = `git commit`
* `gd` = `git diff`
* `go` = `git checkout`
* `undo` = `git reset --soft HEAD~1`

#### Ruby

* `b` = `bundle`
* `be` = `bundle exec`

You can find out more from my [dotfiles](https://github.com/chrisbarber86/dotfiles) or
more specifically my [bash_aliases](https://github.com/chrisbarber86/dotfiles/blob/master/bash_aliases) file.

## Editor

Prior to working at [Sage One](http://www.sageone.com) I would mainly use [textmate](https://macromates.com/)
and occasionally [coda](https://panic.com/coda/).

When I started at Sage everyone was using Vim. It didn't take long for me to
become hooked and I've never looked back since. Infact I regularly find myself
typing Vim commands into things like Outlook and Word.

One of the key things to reducing the barrier to entry for Vim was that everyone
around me was using it and I was able to learn directly from pairing up with
other developers. I also quickly started to craft my own [dotfiles](https://github.com/chrisbarber86/dotfiles)
based on how they had their environments setup - much easier than starting from
scratch!

I make use of the [vundle](https://github.com/gmarik/Vundle.vim) plug-in manager
for vim which enables me to easily keep track of and configure my plugins. I
have several plugins installed, although I use some alot more than others:

The following are permenently visible on screen:

* [NerdTree](https://github.com/scrooloose/nerdtree) - A tree explorer plugin
* [powerline](https://github.com/powerline/powerline) - A statusline plugin for vim

I use these ones all the time

* [tcomment_vim](https://github.com/tomtom/tcomment_vim) - Comments code by line or in blocks using a single command
* [vim-surround](https://github.com/tpope/vim-surround) - Quoting/parenthesizing made simple
* [ctrlp.vim](https://github.com/kien/ctrlp.vim) - Fuzzy file finder
* [supertab](https://github.com/ervandew/supertab) - Tab autocomplete
* [vim-fugitive](https://github.com/tpope/vim-fugitive) - Git wrapper for using git commands in vim

These ones are just always on in the background

* [vim-coffee-script](https://github.com/kchmck/vim-coffee-script) - CoffeeScript support for vim
* [vim-endwise](https://github.com/tpope/vim-endwise) - Ruby helper - ensures code structures are closed automatically (end, endif, etc)
* [vim-markdown](https://github.com/plasticboy/vim-markdown) - Markdown support for vim

The following I use infrequently

* [vim-git](https://github.com/tpope/vim-git) - Suntax highlighting for Git
* [vim-rails](https://github.com/tpope/vim-rails) - Ruby on rails support for vim
* [vim-unimpared](https://github.com/tpope/vim-unimpaired) - pairs of handing bracket mappings

![vim](/images/vim.png)

The great thing about Vim is that being text-based makes it really lightweight
which means it's fast and responsive even with large files.

Being keyboard based it has a lot of key bindings so everything is really close
to home and I find it makes me a lot faster at typing without having to think
much about it. Leaving my mind free to ponder on the code I'm working on.

Another advantage about Vim is that it works great with [TMUX](http://tmux.github.io/)
to allow for pairing with remote colleagues who could be in a different country.

Of course there are downsides to vim, the integration with the mouse along with
copy/paste can be frustrating at times, but still more than managable.

### The End

I hope you found this interesting, feel free to ask me questions on [twitter @chrisbarber86](https://twitter.com/ChrisBarber86)
or take a look at my [dotfiles](https://github.com/chrisbarber86/dotfiles) on [GitHub](https://github.com/ChrisBarber86).

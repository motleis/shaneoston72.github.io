---
layout: post
title: "New MacBook Pro - set up for JavaScript development"
description: "A guide to how I set up my new MBP"
date: 2017-01-10
tags: [macbook, mbp, setup, dev box, javascript]
comments: true
share: true
---
# Setting up a new MacBook Pro for JavaScript development

* TOC
{:toc}

I was excited to receive my new MacBook Pro with Touch Bar today. After the ceremonial unpacking and being amazed by how light and attractive it was, I set about setting it up to my development machine.

If you've read any of my other posts here, you understand that I practicing to be a modern JavaScript master. A necessary first step is to build a laboratory (e.g. my MacBook) to practice my craft. Here's how I configured my MBP for optimal JavaScript development.

## First steps
1. Update the system with App Store > Updates to ensure that the latest operating system updates are installed. Restart the system.
2. Verify that the user account with which you will log in is an admin account. This is necessary to give this account _sudo_ privileges to run command-line (CLI) commands with administrative privileges.
3. I like a clean dock so I remove any unused or infrequently used icons.

## System Preferences and security
1. Set the secondary click (right click) preference on the track pad. I prefer "Click in bottom right corner".
2. Set "Require password immediately after sleep or screen saver begins" in _Security & Privacy > General_.
3. Set "Require an administrator password to access system-wide preferences" in _Security & Privacy > General > Advanced..._.
4. Turn on File Vault in _Security & Privacy_. This will require a restart and the power adapter.

## Development setup
### Basic setup
1. Install Xcode Command Line Tools (faster) or Xcode (slower) to get a compiler. Once one of these is installed, you can use Homebrew to install almost everything else.
2. Next, install [Homebrew](https://brew.sh), a package management system for macOS. Apply the instructions from the Homebrew website.
3. Add a file in the root of your home directory. To do so easily, type in CLI `nano ~/.bash_profile` and add `export PATH="/usr/local/bin:/usr/local/sbin:~/bin:$PATH"` to the file. This will give precedence to applications installed via Homebrew over any that are installed by Apple. Restart CLI.

### Git
Install Git. Xcode command line tools include an outdated copy of Git. Using Homebrew, install the latest stable version:
```
brew install git
```

#### Customise Bash for Git
You can add Git information to CLI.  Helpful as you get more comfortable with Git.
1. Run `brew update`.
2. Run `brew install bash-git-prompt`.
3. Edit `~/.bash_profile` with:

```
if [ -f "$(brew --prefix)/opt/bash-git-prompt/share/gitprompt.sh" ]; then
  __GIT_PROMPT_DIR=$(brew --prefix)/opt/bash-git-prompt/share
  source "$(brew --prefix)/opt/bash-git-prompt/share/gitprompt.sh"
fi
```

Once you have done this, you can further customise Bash with Git aliases. Add the following to `~./bash_profile`.

```
# -----------------
# Git Aliases
# ----------------
alias ga='git add'
alias gaa='git add .'
alias gaaa='git add -A'
alias gb='git branch'
alias gbd='git branch -d '
alias gc='git commit'
alias gcm='git commit -m'
alias gco='git checkout'
alias gcob='git checkout -b'
alias gcom='git checkout master'
alias gd='git diff'
alias gda='git diff HEAD'
alias gi='git init'
alias gl='git log'
alias glg='git log --graph --oneline --decorate --all'
alias gld='git log --pretty=format:"%h %ad %s" --date=short --all'
alias gm='git merge --no-ff'
alias gp='git pull'
alias gss='git status -s'
alias gst='git stash'
alias gstl='git stash list'
alias gstp='git stash pop'
alias gstd='git stash
alias gu='git push'
```

### Text Editor
I am all about using tools that have the lowest learning curve and support expansion as my skills and needs evolve. There are MANY opinions regarding which text editor is best for JavaScript. I have chosen Atom because I've used it for several months and have found it easy to use and to expand as needed.

```
brew cask install atom
```

Tell macOS to use Atom as your preferred editor by adding `export EDITOR="atom -w"` to `.bash_profile`.

Atom has a thriving and growing community to developers who have created tools that you can add to Atom as packages. There is a GUI interface in Atom through which you can search and install packages. You can also add them in CLI. I've added these basic packages to support my JS development.

#### Atom packages
##### atom-beautify
Beautify any file based on its extension.
```
apm install atom-beautify
```

##### git-plus
Do git things without the terminal.
```
apm install git-plus
```

##### linter
Base linter to which you add all manner of language-specific linters.
```
apm install linter
```

##### linter-eslint
Lint JS on the fly, with ES Lint.
```
apm install linter-eslint
```

##### pigments
A package to display colors in projects and files.
```
apm install linter
```

### Productivity Tools
#### Better SnapTool
This handy tool allows you to manage your window positions and sizes by dragging them about or by keyboard shortcuts. I use this daily to arrange Atom, iTerm, and any other window relevant to that on which I am working. You get it from App Store.

#### iTerm2
[iTerm2](https://www.iterm2.com/) replaces Terminal. It has several cool features that can make you more productive such as split panes and hotkey mapping to make the window active. There are a lot of other features that quite frankly I don't use but I'm sure will as I come to rely on CLI in my workflow.

#### Slack
This is quickly becoming (has become?) that de facto communication tool for developers.  If you aren't already using it, you will be.  Go ahead and install it now from the App Store.

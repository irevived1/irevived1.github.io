---
layout: post
title:  "Vim and Tmux Integration"
date:   2016-09-11 17:58:14 -0400
---

09.12.2016

Part 1: Installation with Vundle

On the day I was introduced to programming, my Professor asked everyone to download Visual Studio.  I didn’t know anything about programming and I thought Visual Studio was the one and only editor/compiler out there in this world.  Visual Studio also spoiled me so much that I did not have to use the terminal at all.  The moment after compiling, the console will automatically open up with your program running.  It’s got directory tree on the right, console on the bottom and the code on the main panel.  There weren’t the necessity to use the terminal at all.

As I learn more about programming and other programming languages on different operating systems, I learnt that Visual Studio can no longer spoil me as it used be.  Programming in my Linux Desktop or my Macbook became a manual labor where I had to switch back and forth between the editor and the terminal for compiling, running tests, or simply debugging.  Until one day, Vim and Tmux came to rescue.  

Vim and Tmux integration makes you want to time travel and go back to the time where you do everything in your terminal.  With the absence of GUI, there is no need to switch back and forth between your editor and the terminal.  Soon, you will forget about the presence of your trackpad or mouse.  

Tmux stands for Terminal Multiplexer.  It allows the user to split panes, create windows and sessions painlessly with one instance.  Let’s say you are logging in to a machine using SSH, you do not need to log in again for another window/pane, tmux will handle everything for you.

Vim is the improved version of the built in editor in all unix and linux system, Vi.  This is very self-explanatory, Vim is just like Vi, but better.  With the help of Vundle uniting all the plugins, Vim is just as competitive as any other editors out there.

Actually, at this point, Vim and Tmux are unable to communicate with each other.  We need two additional plugins to make this happen.

Introducing vim-tmux-navigator by christoomey and vimux by benmills, the ultimate plugin for this integration.  Vim-tmux-navigator unifies the vim panes and tmux panes and allows the user to painlessly switch between the panes.  

*Life without navigator:* To move between tmux panes, the user will have to press Control + B + one of the arrow/directional keys.  To move between vim panes, the user will have to press Control + W + h/j/k/l.  It is extremely tiring and confusing at times.  

*Life with navigator:* Control + h/j/k/l will handle both tmux and vim panes!

What does vimux do? Given the following scenario:

*Life without Vimux:* The user finish coding, moves to the terminal, runs rspec, moves back to editor, changes some stuff, moves back to terminal and runs rspec again.

Not too bad, but could be better!

*Life with vimux:* The user simple press Leader key followed by a better.  Boom! Vimux automatically sends “rspec” to the terminal and runs it.
(Though, the user will have to assign keys and commands to fit the user’s needs.) 

[Vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator)

[Vimux](https://github.com/benmills/vimux)


<font size="5em">Adding Plugins to Vim:</font>


[Vundle](http://https://github.com/VundleVim/Vundle.vim) makes plugin installation as easy as GUI programs.  Simple run:

```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

And put the following into your .vimrc file and there you have it!

(*.vimrc lives in your home directory and it is the vim configurations for current user.  Similarly, .tmux.conf will be the tmux configuration and it also lives in your home directory.*)

```
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'
" add your list of plugins below this line

call vundle#end()            " required
filetype plugin indent on    " required
" ALL OTHER CONFIGURATIONS BELOW THIS LINE:
```

Once you have Vundle, it literally takes a few seconds to install new plugins.
Let’s say we would like to install vim-tmux-navigator and vimux together, add:

```
Plugin 'christoomey/vim-tmux-navigator'
Plugin 'benmills/vimux'
```

Just include two lines of code below *Plugin 'VundleVim/Vundle.vim'* in your .vimrc. Then save and quit, and run ```vim +BundleInstall +qall``` in your terminal and there you have it!

Another method to install is to launch vim, in command mode and enter BundleInstall.

**NOTE:**  Some plugin may need extra configurations in your .vimrc.  Please read the README.md for each and very plugin.  If for whatever reason plugin is not working normally, it is highly possible that the configuration is not set up properly.

Here is a list of plugins that I have been using for a while:

[VundleVim/Vundle.vim](https://github.com/VundleVim/Vundle.vim)
* Vim Plugin manager

[christoomey/vim-tmux-navigator](http://github.com/christoomey/vim-tmux-navigator)
* You know this

[scrooloose/nerdtree](http://github.com/scrooloose/nerdtree)
* Adds Directory tree on the left side of the panel

[Syntastic](http://github.com/scrooloose/syntastic)
* Adds syntaxs checking and pinpoints the location

[vimux](http://github.com/benmills/vimux)
* You also know this

[vim-airline/vim-airline](http://github.com/vim-airline/vim-airline)
* Adds fancy status line on the bottom of your vim

[edkolev/tmuxline.vim](http://github.com/vim-airline/vim-airline)
* Makes tmux status line prettier than ever

[tpope/vim-surround](http://github.com/tpope/vim-surround)
* Adds the ability to surround text with brackets or html tags

[tpope/vim-repeat](https://github.com/tpope/vim-repeat)
* Allows you to repeat the previous plugin commands

[othree/html5.vim](http://github.com/othree/html5.vim)
* Adds html5 syntax to your collection

[godlygeek/tabular](http://github.com/godlygeek/tabular)
* Aligns your syntax based on your input

[majutsushi/tagbar](http://github.com/majutsushi/tagbar)
* Opens a window of all your tags on the right side of the panel

[Yggdroot/indentLine](http://github.com/Yggdroot/indentLine)
* Fancy indentation for your vim

[edkolev/promptline.vim](http://github.com/edkolev/promptline.vim)
* Makes your bash promptline fancier than ever

[kien/ctrlp.vim](http://github.com/kien/ctrlp.vim)
* A fuzzy finder for your files

[ervandew/supertab](http://github.com/ervandew/supertab)
* You heard it, its super tab for tab completion.

[vim-ruby/vim-ruby](http://github.com/vim-ruby/vim-ruby)

[tpope/vim-rails](http://github.com/tpope/vim-rails)
* Ruby programmer? get these two!

[alvan/vim-closetag](http://github.com/alvan/vim-closetag)
* Closes the tag for your html tags

[tpope/vim-commentary](http://github.com/tpope/vim-commentary)
* Just get this one

[tpope/vim-endwise](http://github.com/tpope/vim-endwise)
* Completes the end of every definition or if statements

[SirVer/ultisnips](http://github.com/SirVer/ultisnips)

[honza/vim-snippets](http://github.com/honza/vim-snippets)
* You'll have to visit their website for these.  I have lost my words for them.

[Shougo/neocomplete.vim](http://github.com/Shougo/neocomplete.vim)

With a few of the plugins, your terminal is now a legit editor and it also behaves like an editor.  Having directory tree on the left, tagbar on the right, and a little terminal on the bottom.  However you want to arrange it.  Vim and Tmux is highly customizable.

My configs can be found in this repo: [flatiron config with learn and learn submit](https://github.com/irevived1/vim-tmux-config)

Vim has a steep learning curve and it is a lifelong journey.  There will be sweat and pain and I believe one day it will be worth it.

Have a nice day,

-irevievd1



Git Training
============

Notes from my git training

Hour 1
------

Setting up git

  git config --global user.name "Your Name"
  git config --global user.email your@email
  git config --global color.ui auto  #Syntax Highlighting
  git config --global autocrlf input  #Default linefeed settings

Hour 2
------

Changing your preferred editor

  git config --global core.editor "emacs"   #EWWWWWW

Diffing

  git diff
  git diff --staged
  git diff HEAD

  git add -p  .  #Walk through diff and selectivly add changes

  git status -s -u  #Short output, show untracked files
 
  git diff -w  #Suppress the display of whitespace only changes

  git diff --color-words #Highlight changed words using only colors

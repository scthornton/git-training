Git Training
============

Notes from my git training

Hour 1
------

**Setting up git**

    git config --global user.name "Your Name"
    git config --global user.email your@email
    git config --global color.ui auto           #Syntax Highlighting
    git config --global autocrlf input          #Default linefeed settings

Hour 2
------

**Changing your preferred editor**

    git config --global core.editor "emacs"   #EWWWWWW

**Diffing**

    git diff
    git diff --staged
    git diff HEAD
  
    git add -p  .           #Walk through diff and selectivly add changes

    git status -s -u        #Short output, show untracked files
 
    git diff -w             #Suppress the display of whitespace only changes

    git diff --color-words  #Highlight changed words using only colors

Hour 3
------

**History**

    git log                   #Lists commits in reverse chronological order
    git log --stat            #Log with diffstat
    git log -p                #Generate patch
    git log --diff-filter=A   #Select only files that were added.  Could also be M,C,....
    git log --pretty=raw      #
    git log -3                #Show last 3 commit
    git log --author=User     #Show commits by User

**Ignoring Files**

    >vim .gitignore
    #Glob patterns,  one per line
    *.log   #Wildcard matching
    *.tmp   #Wildcard matching
    target  
    output/
    !special.log  #DO NOT ignore this file

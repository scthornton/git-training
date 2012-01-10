Git Training
============

Notes from my git training put on by Matthew McCullough of Ambient Ideas

    http://github.com/matthewmccullough
    http://github.com/matthewmccullough/git-workshop
    http://gist.github.com/1589518


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
    *.log         #Wildcard matching
    *.tmp         #Wildcard matching
    target  
    output/
    !special.log  #DO NOT ignore this file

    git config --global core.excludefiles "~/.gitignore"   #Global excludes.  

Be careful what you put in global excludes. It is not portable, does not propagate with your code. Things you should put in here are ide/os type crud files.

**Empty Directories**

    mkdir emptydir              #Git won't track this
    touch emptydir/.gitignore   #Now it will

**Preconfigured .gitignore**

>http://github.com/github/gitignore

**Removing Files**

    git rm FILENAME         #Directly remove and stage
    rm FILENAME             #Deletes, but does not stage
    git add -u .            #Picks up on deleted files,  -u == update
    git reset --hard        #Restores *tracked* files to their last commited state, cleans the staging area
    git checkout HEAD -- FILENAME  #Restores FILENAME to last commited state

**Moving/Renaming Files**

    git mv OLD NEW          #Composite command
    
Equivalent command:
 
    mv OLD NEW
    git add -A .            #All,  added/removed/modified

How to track moves/renames in your history

    git log --stat          #This will show files added/deleted.  Not renamed/moved
    git log --stat -M       #Show renames
    git log --stat -C       #Show copies/renames
    git log --stat -M90     #Set threshold of 90% on similarity index, for detecting moved/renamed files
    git log -2 --stat -C --find-copies-harder  #Looks through history looking for copies

Discussion on similarity index
   http://permalink.gmane.org/gmane.comp.version-control.git/217

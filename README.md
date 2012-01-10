Git Training
============

Notes from my git training put on by Matthew McCullough of Ambient Ideas

* http://github.com/matthewmccullough
* http://github.com/matthewmccullough/git-workshop
* http://gist.github.com/1589518

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

Hour 4
------

Cloning repositories

    git clone http://user@server/path/to.git
    git clone git://server/path/to.git             #Typically read-only
    git clone file://repository
    git clone git@github.com/user/repository

Branching

    git branch BRANCHNAME                           #Create BRANCHNAME
    git checkout REMOTE/BRANCHNAME                         #Switch to BRANCHNAME

    **Make your changes**

    git push -u origin BRANCHNAME:BRANCHANME        #Push BRANCHNAME to BRANCHNAME at remote repsitory, -u means track


Hour 5
------

Downloading objects from upstream (freshens your cache)

    git fetch             

Sharing your code

    git commit
    git push <remote>     #Send code to an upstream server
    git pull <remote>     #Combination command, fetches and merges to a local branch.  


    git branch -a         #List all branches, local and remote
    git merge BRANCHNAME  #Merges with the currently checked out branch
    git push              #Send your changes upstream

Remotes

> Vocabulary: (Ghetto simple)
> > Local: Your copy of the repository. Exists on your machine
> > Remote: Cached copy of upstream repository. Exists on your machine
> > Upstream: Repository from external source. Could exist on your machine, if you cloned using file://,  but probably exists on a server somewhere

> Default name is **origin**
> Remote branches are locally **immutable** (conceptually)
> Remotes can be thought of as bookmarks
>   Use as public/private repositories
>   Same repo/different protocol

    git remote -v                             #Shows all inbound/outboud address for each repository
    git remote add REMOTENAME GITREMOTEURL    #Add an alias for GITREMOTEURL called REMOTENAME

    git checkout BRANCHAME                    #Make a **local** branch of remote branch
                                              #If a branch exists in more than one remote, or is otherwise ambiguous, it will fail. 
                                              #You *must* be explicit in this case
    git checkout -b BRANCHNAME --track REMOTE/BRANCHNAME    #This will check out the branch you want

Purge 'remote' branches that have been removed from an 'upstream' repository

    git prune

Reversing your commits
    
> If you haven't pushed upstream

    git reset --soft HEAD~1                   #Rewind the history 1 step. --soft preserves changes to files and keeps them staged
    git reset --hard HEAD~1                   #Rewind the history 1 step. --hard DISCARDS changes

> If you have pushed upstream
> >   You can do the same,  but the graph of the commits as your other commiters know it has changed. 
> >   *What if*  you destroyed a commit they were basing changes on?    
    
    git revert COMMITNUMBER                   #Make a commit that negates a previous commit

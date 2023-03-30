Git allows a team of people to work together, all using the same files. And it helps the team cope with the confusion that tends to happen when multiple people are editing the same files.

There are many ways it can be set up and configured, but at my job, here's how we use it: when a new employee starts, he downloads all the files from Github, which is an online server we're all connected to.

So he has his local version of the files, I have my local version, our boss has his local version, etc.

When I make a change to some files, I go through the following process in the Terminal. (There are GUI clients for Git, but I prefer working on the command line.)

 > git pull

That pulls the latest changes down from github. If there are conflicts between those and my local ones, it tells me what they are, file-by-file, line-by-line, and I now have a chance to reconcile those differences.

After editing the files or creating new ones, I run this command:

 > git add .

Which adds all of my local changes to git, so that git knows about them. The dot after add specifically means to add all the changes I've made, e.g. new files I've added to my local folder or changes I've made to existing files. If I want, I can add only specific files, e.g.

 > git add myNewFile.js

I now write a comment about the adds I just made.

 > git commit -m "Fixed a major bug which stopped reports from printing."

Finally, I upload my changes to the server.

 > git push

Now, when my colleagues do a ...

 > git pull

... they will get my changes, and they will be notified if any of them conflict with their local versions.

There are all kinds of cool, useful commands for rolling back changes to a particular time or state. But probably the most useful thing about Git is branching. Let's say my team is working on code for an Asteroids game, and I get the idea for making spinning asteroids. This will involve making some major changes to the existing asteroids code, and I'm a little scared to do that. No worries, I can just make a branch.

First of all, I'll check which branches exist:


 > git branch 
master* 

So there's currently only one branch on my local machine, called master. The star by it means that's the branch I'm currently working in. I'll go ahead and create a new one:

 > git branch spinningAsteroids

That creates a copy of all the files in master. I'll now move into that branch.


 > git checkout spinningAsteroids 
> git branch 
master 
spinningAsteroids* 

I now spend a couple of hours in spinningAsteroids, doing whatever coding I need to do, not worrying about messing things up, because I'm in a branch. Meanwhile, I get a tech support call. They've found a critical bug and I need to fix it asap. No worries...

 > git checkout master

... fix bug ...


 > git pull 
> git add . 
> git commit -m "Fixed critical bug with high scores." 
> git push 

Now I can resume my work with spinningAsteroids.


 > git checkout spinningAsteroids 
> git branch 
master 
spinningAsteroids* 

... work, work, work ...

Okay, I'm now happy with my spinning asteroids, and I want to merge that new code into the main code base, so...


 > git checkout master 
> git branch 
master* 
spinningAsteroids 

 > git merge spinningAsteroids

Now the code from my branch is merged into the main code-base. I can now upload it.


 > git pull 
> git add . 
> git commit -m "added new cool feature! Spinning asteroids!!!" 
> git push 

There are many ways to use Git. This is just one of them.


# Github-command

Switch to a a previous commit to review code from that checkpoint

    # git checkout <your-commit address-here>

Sync a remote repository to local repository with automatic alias assigned called "origin"

    # git remote add <alias-name> <your remote repository link comes here>

Push from local branch "master" up to remote branch "origin" (where 'origin' is set as an alias to the remote repository)
    
    # git push origin master

Pull from remote branch "origin" down to local branch "master"
    
    # git pull origin master

Create a new branch to manage a side hustle in project

    # git branch <your new branch name>

View all branches in your repository, also marks the branch you are working on with *

    # git branch -a

Switch to a branch to work in it

    # git checkout <your-branch name-here>

Delete a branch
    
    # git checkout master
    // Deleting local branch
    # git branch -D <branch name to be deleted>

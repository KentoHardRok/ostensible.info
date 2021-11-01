+++
title = "Git outta here"
weight = 15
+++

#git/remoteadd

# Git Learnings

When you create a new repo and just need to add existing info to that repo this is what you would do

>echo "# obsidian-notes" >> README.md
>git init
>git add README.md
>git commit -m "first commit"
>git branch -M main
>git remote add origin git@github.com:KentoHardRok/notes.git
>git push -u origin main

So just a little context for my own well being. You have an option, either to create a local git repo or clone someone elses. Once you have a folder being tracked by your local git you can add a new remote origin (not sure if im using that right to be honest) what that means is when you do a pull or push its actually going to a new place. 
In the instructions above I created a new repo on my github, then on my local folder I initiated the git tracking, created my first commit then added the origin of the repo I created. Now they are linked! this can be done to copy of projects as well. 

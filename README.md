# gitPractice

* git is a vcs  it's two types of git

    1. centralized vcs
    2. distributed vcs
 
* git maintaines local vcs , but git hub maintaines remort repos.

* git init (in git init we have githooks , HEAD,INDEX )

* git have 5 stages
  
      1. bin  =>> git clean-fd
  
      2. working treee =>> git add <file path> (untracked files to tracked)

      3. staging area ==>> git commit -m "add changes" (tracked files will be stores in local repo)
  
      4. local repo ==>> git pull (all local repo files will be pushed to remort repo)
  
      5. remort repo
  
  
     
     git branch <name>
    
     git checkout -b <branch name>
    
     git branch -m <oldname> <new name>

## git squash

* to merge the 2 commits  into one

## git merge

when we change only in the future branch , we cannot change in the main branches we should follow the bellow two methods 

  1. fastforword merge
  2. un fost-forworded

### git fastforword merge : 

* head shows the latest commit in new feature branch

* git checkout <master>

* git merge <feature>

### git un fost-forworded

* head shows the last commit in the main branch

*  git checkout <master>

* git merge feature --noff


Incase we can change the both main branch and feature branch , we use the 3 ways to merge the code in to main branch

    

### 3 way merge 

*  this merge will be done only in main branch & feature and main branch changes forms some extra commit is called 3 way merge

* git checkout master

* git merge feature

### git rebase 

* inthese case we merge the code in both branches eaither in feature or main branch

* git checout master (or) feature

* git merge feature (or) master

* it have 2 parents , and after merge the commit ids will be changes

[referhere](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)





  

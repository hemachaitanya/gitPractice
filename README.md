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
  
  
     
     git branch branch-name
    
     git checkout -b branch name
    
     git branch -m oldname new name

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

### difference b/w git init ,git clone

* git init: creates new repository , it create .git folder and metadata dependencies

    --bare

* Creates a bare repository. it does not containes working directory 
    

    --template=path

* Specifies the directory from which templates will be used

    --quite

    
* Only prints "critical level" messages, Errors, and Warnings. All other output is silenced

     --separate-git-dir 
     
* on an existing repository and the .git dir will be moved to the specified  path.


* git clone : copy of  existing git repository


## git blame <filename>

* it shows the all commits history  across rename and copies for all commit messages

#### git blame -L 10,15 (for specific lines)

#### git blame 

![blame](./Images/blame.png)

![lines](./Images/line-blame.png)

* git blame -L 11,16 .\README.md

* git blame -R .\README.md

* git blame -M .\README.md

#### git fork and clone

* git fork is copy of remort to remort repos , but git clone have copy of remort to local 

* clone have only one central repo , fork have two individual central repos


### git log --log-size (or) git log --oneline --log-size

* it shows commit msg size also

#### git commit -m --allow-empty " "



[referhere](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)


[refer-git-complete-documentation](https://www.atlassian.com/git/tutorials/undoing-changes/git-revert)


I will also use an alias gl to show logs in pretty format.

alias gl="git log  --pretty=format:%C(red)%h%Creset %C(yellow)%d%Creset %s %C(green)(%cr) %C(yellow)<%an>%Creset"
git rebase -i (Interactive Rebase)
The git rebase -i command allows you to rewrite commit history interactively. You can edit, squash, or reorder commits before pushing them to the remote repository. This command is perfect for cleaning up a messy commit history before merging changes. Consider you have multiple commits that need to be squashed into one.

echo "Add feature A" >> file1.txt
git commit -am "Add feature A"

echo "Fix bug in feature A" >> file1.txt
git commit -am "Fix bug in feature A"

echo "Improve feature A" >> file1.txt
git commit -am "Improve feature A"

# Now squash these commits
git rebase -i HEAD~3
❯ git log --oneline
c749aa6 (HEAD -> master) Improve feature A
a884548 Fix bug in feature A
4a41935 Add feature A
c9e1266 Initial commit
Now let’s use rebase.

git rebase -i HEAD~3
It will pick top three commits automatically and then in editor window change the pick to squash for last two commits and save and exit the editor, Then another editor will ask for a final commit message just save and exits that editor too.

❯ git log
commit 3953f34672581e585c1a8244d1eb46c37ddebf3e (HEAD -> master)
Author: Rahul Beniwal <rahulbeniwal18112002@gmail.com>
Date:   Sat Sep 28 22:39:45 2024 +0530

    Add feature A
    
    Fix bug in feature A
    
    Improve feature A

commit c9e1266e9931383d61708135a6d7064138b72fbe
Author: Rahul Beniwal <rahulbeniwal18112002@gmail.com>
Date:   Sat Sep 28 22:35:55 2024 +0530

    Initial commit
2. git stash
Need to switch branches quickly but have untracked changes you’re not ready to commit? git stash save --include-untracked helps by stashing away both tracked and untracked files, keeping your workspace clean.

echo "Temporary change" >> file1.txt
git stash save --include-untracked
Before Stash

❯ git status 
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
 modified:   file1.txt
After Stash

❯ git status 
On branch master
nothing to commit, working tree clean


3. Binary Search for Bugs (git bisect)
   
When tracking down a bug in a large codebase, git bisect helps you perform a binary search through your commit history. It finds the specific commit where a bug was introduced, saving you from manually inspecting each change.

echo "Feature B" >> file1.txt
git commit -am "Add feature B" # Good commit

echo "Introduce bug in feature B" >> file1.txt
git commit -am "Introduce bug in feature B" # Bad commit
Now let’s use bisect.

Start the Bisecting Process: To initiate the binary search, use the following command:
git bisect start

Mark the Bad Commit: You mark the current commit (where you know the bug exists) as bad:
git bisect bad HEAD

Mark a Good Commit: Next, you need to tell Git which commit was the last known good state. Replace <commit-hash-of-good-commit> with the hash of the last commit that you know was working correctly:

git bisect good c9e1266e9931383d61708135a6d7064138b72fbe

After testing the current commit (e.g., Add feature B), you find that it still contains the bug.
git bisect bad
Repeat Until Done: Git will check out another commit. You continue this process of testing and marking until you find the commit that introduced the bug.
To stop this process after finding bug you can use git bisect reset.

4. git reflog
   
Ever wished you could recover from a hard reset or a forced push? git reflog tracks every change in your repository, even those that don’t exist in the commit history, helping you recover lost commits.

Consider you accidentally reset your branch and want to recover commits.

Before Hard Reset

❯ gl

e06395a  (HEAD -> master) Introduce bug in feature B (14 minutes ago) <Rahul Beniwal>
2e1a5a5  Add feature B (14 minutes ago) <Rahul Beniwal>
3953f34  (m2) Add feature A (29 minutes ago) <Rahul Beniwal>
c9e1266  Initial commit (39 minutes ago) <Rahul Beniwal>
After Hard Reset

❯ git reset --hard HEAD~1
HEAD is now at 2e1a5a5 Add feature B

❯ gl
2e1a5a5  (HEAD -> master) Add feature B (14 minutes ago) <Rahul Beniwal>
3953f34  (m2) Add feature A (30 minutes ago) <Rahul Beniwal>
c9e1266  Initial commit (40 minutes ago) <Rahul Beniwal>
Let’s use git reflog.

❯ git reflog
2e1a5a5 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~1
e06395a HEAD@{1}: checkout: moving from 3953f34672581e585c1a8244d1eb46c37ddebf3e to master
3953f34 (m2) HEAD@{2}: checkout: moving from 2e1a5a5e0f72fc74187c9fd664df1b49f66fe393 to 3953f34672581e585c1a8244d1eb46c37ddebf3e
2e1a5a5 (HEAD -> master) HEAD@{3}: checkout: moving from master to 2e1a5a5e0f72fc74187c9fd664df1b49f66fe393
e06395a HEAD@{4}: checkout: moving from 2e1a5a5e0f72fc74187c9fd664df1b49f66fe393 to master
2e1a5a5 (HEAD -> master) HEAD@{5}: checkout: moving from master to 2e1a5a5e0f72fc74187c9fd664df1b49f66fe393
e06395a HEAD@{6}: commit: Introduce bug in feature B
2e1a5a5 (HEAD -> master) HEAD@{7}: commit: Add feature B
3953f34 (m2) HEAD@{8}: reset: moving to HEAD
3953f34 (m2) HEAD@{9}: checkout: moving from m2 to master
3953f34 (m2) HEAD@{10}: checkout: moving from master to m2
3953f34 (m2) HEAD@{11}: rebase (finish): returning to refs/heads/master
3953f34 (m2) HEAD@{12}: rebase (start): checkout HEAD~1
3953f34 (m2) HEAD@{13}: rebase (finish): returning to refs/heads/master
3953f34 (m2) HEAD@{14}: rebase (squash): Add feature A
0ef6339 HEAD@{15}: rebase (squash): # This is a combination of 2 commits.
4a41935 HEAD@{16}: rebase (start): checkout HEAD~3
c749aa6 HEAD@{17}: rebase (finish): returning to refs/heads/master
c749aa6 HEAD@{18}: rebase (start): checkout HEAD~3
c749aa6 HEAD@{19}: rebase (finish): returning to refs/heads/master
c749aa6 HEAD@{20}: rebase (start): checkout HEAD~2
c749aa6 HEAD@{21}: rebase (finish): returning to refs/heads/master
c749aa6 HEAD@{22}: rebase (start): checkout HEAD~1
c749aa6 HEAD@{23}: rebase (finish): returning to refs/heads/master
c749aa6 HEAD@{24}: rebase (start): checkout HEAD~1
c749aa6 HEAD@{25}: rebase (finish): returning to refs/heads/master


❯ git checkout e06395a
❯ gl
e06395a  (HEAD) Introduce bug in feature B (19 minutes ago) <Rahul Beniwal>
2e1a5a5  (master) Add feature B (19 minutes ago) <Rahul Beniwal>
3953f34  (m2) Add feature A (34 minutes ago) <Rahul Beniwal>
c9e1266  Initial commit (44 minutes ago) <Rahul Beniwal>
5. Cherry-Picking Commits (git cherry-pick)
Need to apply a specific commit from one branch to another? git cherry-pick lets you select and apply individual commits without merging entire branches.

git checkout -b feature-branch
echo "Feature C" >> file1.txt
git commit -am "Add feature C"
❯ gl
97b1077  (HEAD -> feature-branch) Add feature C (2 seconds ago) <Rahul Beniwal>
e06395a  Introduce bug in feature B (22 minutes ago) <Rahul Beniwal>
2e1a5a5  (master) Add feature B (22 minutes ago) <Rahul Beniwal>
3953f34  (m2) Add feature A (38 minutes ago) <Rahul Beniwal>
c9e1266  Initial commit (48 minutes ago) <Rahul Beniwal>
Let’s copy 97b1077 changes.

❯ git checkout master
❯ git cherry-pick 97b1077
Auto-merging file1.txt
CONFLICT (content): Merge conflict in file1.txt
error: could not apply 97b1077... Add feature C
Be ready to fix merge conflicts if any 😆.

6. Hard Reset (git reset --hard)
If you need to discard all local changes and reset your working directory and staging area to a specific commit, git reset --hard is your go-to command. Use it with caution, as it will erase changes.

Before Hard Reset

❯ gl
2e1a5a5  (HEAD -> master) Add feature B (26 minutes ago) <Rahul Beniwal>
3953f34  (m2) Add feature A (42 minutes ago) <Rahul Beniwal>
c9e1266  Initial commit (52 minutes ago) <Rahul Beniwal>
On

❯ git reset --hard c9e1266 
After Hard Reset

❯ gl
c9e1266  (HEAD -> master) Initial commit (52 minutes ago) <Rahul Beniwal>





  

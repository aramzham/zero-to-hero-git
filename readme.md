Why we need a version control?
we are all humans and we need to get back to the history to see what we have done, why we have done or maybe someone else has done something

centralized version control systems don't keep history of commits, they copy the files to another folder when branching is need => expensive operation!!
tfs is cvc system, it uses pessimistic locking

in distributed version control you download the source code, you get the entire history of commits (save checkpoints)
if you don't have access to internet, you do your own local commits then when you're back online you push them to server

if you computer dies => you lose your uncommitted changes => push them to the server periodically 

git, like tfs, is a version control system to track your changes

git occupies around 94% of the market, svn - 5%, 1% - mercurial

download git from git-scm.com

git configuration levels
system - applies to all users on the machine
global - to your user
local - only to the repository you're in

git doesn't know anything about the file, you've never committed it => it's an untracked file

when you "git add a.txt" a.txt goes from working directory to staging area

when you "git commit ..." it goes into local repository, local repository history

git log - get the history of your repository

git add . - add everything in the current directory and down to tracking, if you want to add all your changed files, won't work if you are not at root level

git add -A - add everything regardless where you are

git reset HEAD~1 - remove the last commit (as if it didn't exist in the history) and preserve the changes 
git reset HEAD~n - undo the last n commits and preserve the changes

git revert sha_of_the_commit - keep the remove commit action as another commit, so you revert the changes and add another commit stating that

reset vs revert - reset will wipe out the commit from history (maybe you have accidentally entered some secrets in history or don't want your colleagues to know that you suck), revert will keep that reverting action as a commit

git commit --amend --no-edit - if you want to make changes to the last commit (applies ONLY to the last one) and not add a new commit, you just amend it, "--no-edit" means don't change the name of the commit

ignore the files from being commit by specifying them in special .gitignore file

git stash doesn't stash untracked files
git stash -u to stash them

git clean -f - remove all untracked files
git clean -fd - get rid of untracked files, folders and subfolders

git reset --hard - undo the changes on the tracked files

HEAD is the latest commit your branch is pointing to

git merge feature-a - (if we were on master) take all the commits that are on feature-a branch and not in master and bring to master

ideally branches should be short lived and merged to master/main on a daily basis

once you're done with the work remove the branch using "git branch -D branch_name"

when creating a new branch files are not copied, you just point to another commit

what to do when you accidentally committed your code onto a wrong branch?
- git reset HEAD~1
- git stash -u
- git checkout -b correct_branch
- git stash pop
- git add -A
- git commit -m "now committing on correct branch"

if you have local git repo and want to connect it to remote one (in this case GitHub) you'd need "git remote add origin https://github.com/{username}/{repository}.git"

git branch -M main - make the "main" as main branch :)

git push -u origin main - create an upstream branch main (on remote)

git reset c.txt - unstage c.txt

git checkout c.txt - undo the changes done on c.txt before you commit
git checkout *.txt - undo changes of files that have .txt extension
git checkout subfolder/**.txt - undo changes in subfolder txt files
git checkout **/*.txt - anybody, any subfolder with .txt

git fetch - get all the changes from remote repository to your machine but not into local repository

git fetch + git merge origin/main = git pull

git pull origin feature-a - pull changes from feature-a branch to your current local branch

f5d4a42 (HEAD -> main, origin/main) Update a.txt - you're up to date with origin

when you push your local branch and it turns out that you don't have it on the origin first possibility is to run "git push -u origin your_branch_name"
the other possibility is "git config --global --add --bool push.autoSetupRemote true"

rebase will take your commits and take into another branch without creating the merge commit => your history will look cleaner

squash and merge strategy will take your commits and pack it into a single one => cleaner history

clone vs pull - clone is the initial pulldown of the repo, once you have it you can pull the changes

git config --global alias.co "checkout" - this means that you can do "git co main" = "git checkout main"

git config --global alias.copm '!git checkout main && git pull' - go to main and pull it with "git copm"

some useful productivity tips from Scott Sauber
https://github.com/scottsauber/dotfiles/blob/main/.bashrc
put them all in .bashrc file at C:\Users\<username>
if you encounter some errors regarding refs type "git remote set-head origin main"

https://dangitgit.com/

when resolving a merge conflict think from remote perspective, current is the current situation on remote, the incoming is the changes that are going to go on remote

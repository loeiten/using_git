This is a small note of nifty things I've found while working with git.

# For the beginners:
http://readwrite.com/2013/09/30/understanding-github-a-journey-for-beginners-part-1#awesm=~oFlQCvoJank0tf
http://readwrite.com/2013/10/02/github-for-beginners-part-2#awesm=~oFlUvD0lcooGkC

# To not have to type the username and pw all the time:
NOTE: You have to change the URL from HTTP to SSH when making an SSH key

https://help.github.com/articles/generating-ssh-keys/

(if this is not so informative, this can help on the way
https://help.github.com/enterprise/11.10.340/user/articles/generating-ssh-keys/)

https://help.github.com/articles/changing-a-remote-s-url/

# Nifty to remember
```
git add -A # Adds everything
git add -u # Do not add new files
```
http://stackoverflow.com/questions/572549/difference-between-git-add-a-and-git-add

# gitdiff
Use `git d` instead of `gitdiff`

Eventually, `git diff --no-external`

http://stackoverflow.com/questions/3713765/viewing-all-git-diffs-with-vimdiff

# List all the files for a commit in Git
Get the checksum for git log

Either:
```
git diff-tree --no-commit-id --name-only -r <checksum>
```
or
```
git show --pretty="format:" --name-only <checksum>
```
http://stackoverflow.com/questions/424071/list-all-the-files-for-a-commit-in-git

# Revert to a previous Git commit
**NOTE**:
* This will destroy any local modifications.
* Don't do it if you have uncommitted work you want to keep.
```
git reset --hard <checksum>
```
http://stackoverflow.com/questions/4114095/revert-to-a-previous-git-commit

# Create folder at github
`git remote add origin https://github.com/uname/folder.git`

# Revert all changes
Remove all untracked files

`git clean -f`

Revert changes made to your working copy

`git checkout .`

Revert changes made to the index (i.e., that you have added)

`git reset`

Revert a change that you have committed

`git revert ...`

http://stackoverflow.com/questions/1146973/how-do-i-revert-all-local-changes-in-git-managed-project-to-previous-state

# How git works
http://stackoverflow.com/questions/2745076/what-are-the-differences-between-git-commit-and-git-push

# Branches
Clone a branch

`git clone -b <branch> <remote_repo>`

http://stackoverflow.com/questions/1911109/git-clone-a-specific-branch

Make branch

`git checkout -b <name_of_your_new_branch>`

Push branch

`git push origin <name_of_your_new_branch>`

See branches

`git log --graph --oneline --all`

Delete a branch

`git push origin --delete <branchName>`

http://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging

# Add a delete
`git rm $(git ls-files --deleted)`

# Resolve a confilct
https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line/

# Git on USB
## Make the repository
```
mkdir /path/to/usb/repository.git
cd /path/to/usb/repository.git
git init --bare
cd /path/to/source/
git init
git remote add usb file:///path/to/usb/repository.git
git push usb
```
## Pull from the repository
a) If there are stuff already in the folder:
```
git remote add usb file:///path/to/usb/repository.git
git pull usb
git fetch --all
git reset --hard usb/master
git push usb
```
b) In a clean folder
```
git clone file:///path/to/usb/repository.git
```
http://www.geppyparziale.com/post/13494900906/create-a-git-repository-on-a-usb-drive

# Download git to a server
```
cd ~
mkdir install
mkdir git
cd install
wget http://kernel.org/pub/software/scm/git/git-2.1.1.tar.gz
tar -xvf git-2.1.1.tar.gz
cd git-2.1.1
./configure --prefix=$HOME/src --exec-prefix=$HOME/src/git
make
make install

# Write the following to the terminal
export PATH=$PATH:$HOME/src/git/bin
# Add following to ./bashrc
# # Using git
# export PATH=$PATH:$HOME/src/git/bin
```
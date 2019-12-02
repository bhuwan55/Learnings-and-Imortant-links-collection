# Delete N no's of git commit(Remote repo)

> Caution!!: Deleting a commit deletes the changes made in the commit. 
It should only be used to remove the mistakely commited changes.

## 1. Switch to the branch:

``git checkout <branch_name>``

## 2. View the changes on the branch:

``git log``

## 3. Start rebasing the 'N' no of commits from back to the HEAD.

``git rebase -i HEAD~N``

**In the example below i've selected latest 4 commits**: ``git rebase -i HEAD~4``

```
pick ac9e2ed Custom User model
pick c0582ce asd
pick 830e408 asd
pick 5b473cf asd

# Rebase da2515a..5b473cf onto da2515a (4 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out

```
**Description:**
  - **ac9e2ed, c0582ce, 830e408, 830e408** are the commit id.
  - **Custom User Model, asd, asd, asd** are the commit message

## 4. Choose the commits you want to delete:

Replace the pick with **d** in the begining of each commits you want to delete.

**I'll be deleting last 3 commits**

```
pick ac9e2ed Custom User model
d c0582ce asd
d 830e408 asd
d 5b473cf asd
```

## 5. Save the file

## 6. Forcefully push those changes to the remote repo
``git push -f origin <branch_name>``



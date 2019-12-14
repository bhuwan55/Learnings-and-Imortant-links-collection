# Squash Commits 

## 1. Make sure you're on correct branch
``git checkout <branch_name>``

## 2. Start squashing N no of commits from back to head in interactive mode
``git rebase -i HEAD~<N>``

**In the example below i've selected latest 4 commits:** ``git rebase -i HEAD~4``
```
pick ac9e2ed Changed File A line
squash c0582ce Changed File A line 3
squash 830e408 Changed File A line 2
squash 5b473cf Changed File A line 1
```
Here commits with id **5b473cf, 830e408, c0582ce are appended on commit ac9e2ed**

## 3. Force Push the final squashed commits
``git push --force-with-lease <barnch-name>``

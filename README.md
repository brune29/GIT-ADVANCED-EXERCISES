# Git Advanced Exercises

## Part 1

### Missing File Fix

```bash
git status
# Untracked files:
# (use "git add <file>..." to include in what will be committed)
#       test4.md

# nothing added to commit but untracked files present (use "git add" to track)
git add test4.md
git commit --amend -m "chore:Create third and fourth files (fix-added 
test4.md)"
#[main d141072] chore:Create third and fourth files (fix-added test4.md)
# Date: Mon Sep 8 14:10:52 2025 +0200
# 2 files changed, 0 insertions(+), 0 deletions(-)
# create mode 100644 test3.md
# create mode 100644 test4.md
```


### Editing Commit History:
```bash
 git rebase -i HEAD~2

#[detached HEAD 462cacd] chore: Create second file
#Date: Mon Sep 8 14:10:17 2025 +0200
#1 file changed, 0 insertions(+), 0 deletions(-)
#create mode 100644 test2.md
#Successfully rebased and updated refs/heads/main.
git log --oneline

#22d0a75 (HEAD -> main) chore:Create third and fourth files (fix-added test4.md)
#462cacd chore: Create second file
#1185a4f chore: Create initial file
```

### Keeping History Tidy - Squashing Commits:
```bash
git log --oneline --graph
git rebase -i ba4eef5 
git push --force
```
### Splitting a Commit:
```bash
git log --oneline --graph -5
#f0f5008 (HEAD) chore:Create third and fourth files (fix-added test4.md)
#* 23480e9 chore: Create initial and second file
#* ba4eef5 Initial commit
git reset HEAD~1
git add test3.md
git commit -m "Create Third File"
git add test4.md
git commit -m "commit fourth File"
git log --oneline
#8541719 (HEAD) Create Fourth File
#127898b Create Third File
#23480e9 chore: Create initial and second file
<<<<<<< HEAD
<<<<<<< HEAD
#ba4eef5 Initial commit
```
### Advanced Squashing:
```bash
git log --oneline -6
#4b847bb (HEAD -> main, origin/main, origin/HEAD) commit readme
#04b687b commit readme changes
#8541719 Create Fourth File
#127898b Create Third File
#23480e9 chore: Create initial and second file
#ba4eef5 Initial commit

git rebase -i HEAD~4
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
#ba4eef5 Initial commit
>>>>>>> 04b687b (commit readme changes)
=======
#ba4eef5 Initial commit
>>>>>>> 4b847bb (commit readme)
=======
```
### Dropping a commit:
```bash
git log --oneline
#UNWANTED.TXT
#f3c9ab0 commit unwanted txt
#665515d (origin/main, origin/HEAD) readme latest changes
#11267b7 commit readme
#f3ac7af commit readme changes
#6b807f1 commit changes
#f09d6b4 commit the latest changes
#ebfdab1 commit readme
#73a660c Create Third and Fourth File
#23480e9 chore: Create initial and second file
#ba4eef5 Initial commit

git rebase -i HEAD~1
#Successfully rebased and updated refs/heads/main.
```

#### Reordering Commits:
```bash
 git log --oneline
 #commit latest changes on readme.md
#f3c9ab0 commit unwanted txt
#665515d (origin/main, origin/HEAD) readme latest changes
#11267b7 commit readme
#f3ac7af commit readme changes
#6b807f1 commit changes
#f09d6b4 commit the latest changes
git rebase -i HEAD~3
#Successfully rebased and updated refs/heads/main.
git log --oneline
#readme latest changes
#9f7b140 commit unwanted txt
#24b4ee4 readme
#11267b7 commit readme
```

### Cherry-Picking Commits:

```bash
git checkout -b ft/branch
#Switched to a new branch 'ft/branch'
"This is test5 content" | Out-File -Encoding utf8 test5.md
git add test5.md
git commit -m "Implemented test 5"
git checkout main
#Switched to branch 'main'
git log ft/branch --oneline -1
#Implemented test 5 Date: Wed Sep 10 14:05:39 2025 +0200 1 file changed, 1 insertion(+) create mode 100644 test5.md
git cherry-pick 3ec6376
git log --oneline
#Implemented test 5
#d0007a6 commit readme
#780f33b readme latest changes
#9f7b140 commit unwanted txt
#24b4ee4 readme
#11267b7 commit readme

```
## Part 2
### Feature Branch Creation:
```bash
git checkout -b ft/new-feature
### Switched to a new branch 'ft/new-feature'
```
### Working on the Feature Branch:
```bash
git checkout -b ft/new-feature
#Switched to a new branch 'ft/new-feature'
"This is the functionality of the new feature" | Out-File -Encoding utf8 feature.txt
git add feature.txt
git commit -m "Implemented core functionality for new feature"
git log --oneline -1
#63aa766 (HEAD -> ft/new-feature) Implemented core functionality for new feature
```
### Switching Back and Making More Changes:
```bash
 git checkout main
# Switched to branch 'main'
"This is the content for projectreadme" | Out-File -Encoding utf8 readme.txt
git add .
git commit -m "updated project readme"
```
### Local vs. Remote Branches:
```bash
git push -u  origin ft/new-feature
#completed with 2 local objects.
git switch main
```
### Branch Deletion:
```bash
git branch -d ft/new-feature
#Deleted branch ft/new-feature (was 63aa766).
git switch main
#Switched to branch 'main'
```
### Creating a Branch from a Commit:
```bash
git log --oneline
#a16eac9 (HEAD -> main) commit latest changes
#7dbb561 (origin/main, origin/HEAD) Merge branch 'main' of https://github.com/brune29/GIT-ADVANCED-EXERCISES
#bc2454b updated project readme
git checkout -b ft/new-branch-from-commit bc2454b 
#Switched to a new branch 'ft/new-branch-from-commit'
git add .
git commit -m "commit readme after creating a b from a specific commit"
```
### Branch Merging:
```bash
git checkout main
# Switched to branch 'main'
git merge ft/new-branch-from-commit
# Merge made by the 'ort' strategy.
```
### Branch Rebasing:
```bash
git log --oneline  
# 6075b1f (HEAD -> main) Merge branch 'ft/new-branch-from-commit'
# d52f3ff (ft/new-branch-from-commit) commit readme after creating a b from a specific commit
# a16eac9 (origin/main, origin/HEAD) commit latest changes

git checkout ft/new-branch-from-commit    
# Switched to branch 'ft/new-branch-from-commit'
git rebase main
# Successfully rebased and updated refs/heads/ft/new-branch-from-commit.
```
### Renaming Branches:
```bash
git branch -m ft/improved-branch-name
```

### Checking Out Detached HEAD:
```bash
git log --oneline
# 6075b1f (HEAD -> main, origin/main, origin/HEAD, ft/improved-branch-name) Merge branch 'ft/new-branch-from-commit'
# d52f3ff commit readme after creating a b from a specific commit
# a16eac9 commit latest changes
# 7dbb561 Merge branch 'main' of https://github.com/brune29/GIT-ADVANCED-EXERCISES
# bc2454b updated project readme

git checkout d52f3ff
# Note: switching to 'd52f3ff'.
# You are in 'detached HEAD' state. You can look around, make experimental changes and commit them ..
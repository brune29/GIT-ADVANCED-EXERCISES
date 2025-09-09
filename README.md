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



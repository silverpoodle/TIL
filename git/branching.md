# Branching and Merging

- Branch allows developers to isolate their work from others
- Branches can be merged into any branch

<br/>

### 1. Main Branch

- Default branch, sets main branch **pointer** at the initial commit
  - Commit -> pointer moves forward accordingly
- **HEAD**: Keep track of the branch you are currently working on
  - ALWAYS refers to the latest commit on the CURRENT branch
  - switch branch -> HEAD also switches

<br/>

### 2.  Branch Commands

```bash
# Create Branch
git branch <branch-name>
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/git1.png?raw=true" alt="image" style="zoom:60%;" />



```bash
# Switch Branch (HEAD changes too)
git checkout <branch-name>
git checkout -b <branch-name> #create & checkout NEW branch
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/git2.png?raw=true" alt="image" style="zoom:60%;" />



```bash
# Make changes and Commit
git status   //On branch devel
git add README.md
git commit -m "Commit 4"
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/git3.png?raw=true" alt="image" style="zoom:60%;" />



```bash
# Switch back to Main
git checkout master
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/git4.png?raw=true" alt="image" style="zoom:60%;" />



```bash
# Work on master & Commit
git status   // On branch master
git add README.md
git commit -m "Commit 5"
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/git6.png?raw=true" alt="image" style="zoom:60%;" />



<br/>

### 3. Merging Two Branches

**3-1. Fast-Forward Merge**

<img src="https://github.com/silverpoodle/typora-images/blob/main/merge1.png?raw=true" alt="image" style="zoom:40%;" />

- if the branch is a **Direct Descendant** (Linear Path)
- Moves the **HEAD pointer forward**
- NO new commits.

```bash
git checkout master

# discard commit5 & rewind to commit3
# HEAD ~1 moves pointer back one commit
git reset --hard HEAD ~1 // HEAD = commit3

git merge devel
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/merge3.png?raw=true" alt="image" style="zoom:40%;" />

<br/>

**3-2. 3-Way Merge**

<img src="https://github.com/silverpoodle/typora-images/blob/main/merge2.png?raw=true" alt="image" style="zoom:30%;" />

- conflict -> PAUSE merge (*unmerged*)
- `git status` : check unmerged file, study&resolve conflict
- resolved -> stage file -> commit (3-way merge)

```bash
// Master Branch
git checkout master
git reset --hard HEAD~1

// Change the email to abc@abc.com
git add README.md
git commit -m "Commit 5"

// Devel Branch
git checkout devel
git reset --hard HEAD~1

// Change the email to xyz@xyz.com to trigger conflict
git add README.md
git commit -m "Commit 4"

// 3-way merge with conflict
git checkout master
git merge devel
# Auto-merging README.md
# CONFLICT (content): Merge conflict in README.md
# Automatic merge failed; fix conflicts and then commit the result

git status
# On branch master
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#       both modified:      README.md
# no changes added to commit (use "git add" and/or "git commit -a")

// Modify README (resolve Conflict)

// commit
git add README.md
git commit -m "Commit 6"
```

<img src="https://github.com/silverpoodle/typora-images/blob/main/merge4.png?raw=true" alt="image" style="zoom:60%;" />



<br/>

### 4. Delete Merged Branch

```bash
git branch -d devel
```

<br/>

### 5. Amend Last Commit

- Want to change Commit message / Add more changes after making commit
  - AMEND recent commit instead of making new one

```bash
git commit --amend -m "<message>"
```

<br/>

### 6. Undo Git Changes

<img src="https://github.com/silverpoodle/typora-images/blob/main/undo4.png?raw=true" alt="image" style="zoom:60%;" />

**6-1 reset**

- resets currunt branch head to <commit>

- `--soft`, `--mixed`(default), `--hard`

  <img src="https://github.com/silverpoodle/typora-images/blob/main/undo1.png?raw=true" alt="image" style="zoom:60%;" />

  ```bash
  # HARD
  git reset --hard <commit-name>
  
  # Reset both staging area and working tree to the given commit, i.e., discard all changes after that commit
  # resetting your current HEAD branch to an older revision (rolling back)
  ```

  <img src="https://github.com/silverpoodle/typora-images/blob/main/undo2.png?raw=true" alt="image" style="zoom:60%;" />



<br/>

**6-2 revert**

- NO commit Deletions
- REVERTS THE EFFECTS of a certain commit
- GENERATE new commit that undoes all the changes
  - prevents losing history
  - safer way, compared to reset

<img src="https://github.com/silverpoodle/typora-images/blob/main/undo3.png?raw=true" alt="image" style="zoom:60%;" />




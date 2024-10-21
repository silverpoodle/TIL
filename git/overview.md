# Git Overview

### 1. **Version Control System (VCS):**

- A VCS manages file versions and stores changes (commits), allowing collaboration and tracking file history.

-  Centralized (CVS, Subversion): Single server contains all versioned files

  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021234812913.png?raw=true" alt="image-20240218203439687" style="zoom:50%;" />

  - •Distributed VCS(e.g., git): Each user has a full copy

    <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021234901716.png?raw=true" alt="image-20240218203439687" style="zoom:50%;" />

    



<br/>

### 2. **Git:**

- Git, created by Linus Torvalds in 2005, is a Distributed Version Control System (DVCS).

- **Commit Snapshots**: Git takes **snapshots** of file states when commits are made, storing only differences in unchanged files.

  - If files have not changed, Git doesn’t store the file again --just a link to the previous identical file it has already stored

    <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021235217004.png?raw=true" alt="image-20241021235217004" style="zoom:50%;" />

- **Commit Deltas(CVS, Subversion)**: Think of the information as a set of files and the changes(deltas) made to each file over time

  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021235452386.png?raw=true" alt="image-20241021235217004" style="zoom:50%;" />

  <br/>

### Git Basic

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021235625789.png?raw=true" alt="image-20241021235217004" style="zoom:50%;" />

<br/>

1. **File Lifecycle:**

   <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20241021234256898.png?raw=true" alt="image-20240218203439687" style="zoom:50%;" />

   - Untracked → Staged → Committed.

     

2. **Commands:**

   ```sh
   git init # create git repository on current folder
   git config # configure git setting
   	--global credential.helper store # credentials
   
   git status # show the status of files
   git add [filename] # stage a new file
   	add . # add all
   	add *.java # certain files
   git commit # commit ALL files in staging area
   	-m #provide message
   	
   git log # view commit history
   git diff # compare changes
   
   git rm --cached [filename] # unstage
   
   .gitignore # exclude certain files from vc
   
   git remote -v # list all remote names
   git remote rm origin # remove connection
   git push -u # set upstream branch for current local branch (main -> origin/main)
   
   git clone <repo-url> <working directory>
   ```

   <br/>

   3. **Git Tagging**

      - Tag a Specific Commit as being important (particular release)

      ```shell
      git tag -a <tag-name> -m <message> [commit No]# create annotated tag
      
      git tag # list tags
      git show v1.0.0 # retreive tag data
      git push origin v1.o.o # push tag to remote
      git push origin --tags # push all tags
      ```

      
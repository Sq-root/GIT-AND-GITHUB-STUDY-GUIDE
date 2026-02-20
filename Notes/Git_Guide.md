
## CHAPTER 1: The Foundations of Version Control

### Learning Objectives

- Understand the core problem Git solves.
- Define what a Version Control System (VCS) is.
- Evaluate manual versioning versus automated version control.
### 1.1 Introduction: Why Does Git Exist?

Before getting into what Git and GitHub are, let us understand first why Git is around.

Consider the Google Chrome browser (or any web browser you use for your research, visit websites, etc.). The Chrome you are using now did not look the same way when it was first made. Developers keep on developing it and upgrading it.

Suppose a developer added a feature, but later wants to discard it. He/she cannot do it if they don't have files of the previous version saved. This led to the development of Git.

> **📖 Definition: What is Git?**
> 
> Git is a **Version Control System**. It keeps track of all the files. Using Git one can:
> 
> 1. Easily recover files.
> 2. Find out who introduced an issue and when.
> 3. Roll back to a previous working state.
> 
### 1.2 The Need for Versioning: An Application Example

Suppose I made an app having **Version 1** containing files:

- `f1`
- `f2`
- `data.csv`

![Version example](../img/img8.png)

Which I upgraded to **App Version 2** and made changes in `f2` and called it `f3`.

It is very important that I have Version 1 files saved so that if anything bad happens (e.g., `f3` not working properly) I can roll back to Version 1.

### 1.3 The Manual "Zip" Method vs. Git

But still, is Git really required? **No!**

You could use a manual "Zip" copy & paste method:

![Zip method](../img/img1.png)

If I have a project, I can copy and paste the entire project every time I upgrade it. This method is not so good because:

1. **Space:** It consumes space. It will require a lot of storage if my project is very big.
    
2. **Metadata:** It does not give us information about who made changes and when.
    
3. **Precision:** Even if we add data to remind its change time, this method is not good because Git gives timestamps in **seconds** (i.e., in which second what changes have taken place).
    
4. **Collaboration:** It depends on you; if you have large storage and money to buy 100 hard disks, don't use Git. But also, you cannot send the full project along with version history to your teammates. So better understand Git and make life simple.
    
## CHAPTER 2: The Evolution of Version Control Systems

### Learning Objectives

- Compare Local, Centralized, and Distributed Version Control Systems.
- Understand why Distributed systems are the modern standard.
### 2.1 Local VCS

Here we use databases to keep track of files.

- **Advantages:** 1) We can roll back to previous versions. 2) Can track files. 3) No stress of pushing or pulling data from a server.
- **Disadvantages:** All changes remain in 1 computer only. If computer/hard drive is damaged, all data is lost. A lot of storage is required.
### 2.2 Centralized VCS

Here data is stored in a server. Developers push and pull from this server (e.g., Computer 1, Computer 2, and Computer 3 all pushing/pulling to the central server).

- **Advantages:** If a computer gets damaged, he/she can recover files easily. Many developers can work at the same time connecting to the server.
- **Disadvantages:** The copy stored in the centralized server is considered to be final. If the server is damaged, all data is lost. Some files can be recovered from a PC but cannot roll back.

![Centralized VCS](../img/img2.png)
### 2.3 Distributed VCS (The Smart System)

Here files are stored in the server as well as in the computer.

- **Advantages:** All computers receive the full project with full history. If the server gets damaged, the whole project along with previous versions are safe in the computer. Can roll back (complete backup).
- **Disadvantages:** None.

![Distributed VCS](../img/img3.png)

> **💡 Condition: The Logic of a Smart System**
> 
> We need a smart system which does not occupy large disk space. If we have a 5GB project, in that we don't have 5GB of source code (it is in KBs).
> 
> We need a smart system which will ignore static files and will pull only source code. If any file is changed, it should save **only that change**. It should not copy and paste the whole project which will require a lot of storage need. Its repository size will increase and will become difficult to give a full backup to users when needed.

## CHAPTER 3: The Origins & Architecture of Git

### Learning Objectives

- Learn the history of Linus Torvalds and Git.
- Differentiate between Git and GitHub.
- Understand Git's core features and the Three-Stage Architecture.

### 3.1 Who Created Git and the Story Behind It?

**Linus Torvalds** created Git, who was also the creator and main developer of the Linux kernel.

- **1991–2002:** Linux (OS) development was done in patches and archive files. There was no VCS.
- **BitKeeper:** BitKeeper VCS offered VCS for free to Linux development. But, later removed the free of charge status.
- **The Response:** So, Linus Torvalds created Git which provided free VCS.

### 3.2 What is GitHub?

GitHub is a hosting website, which hosts various Git repositories.

- There are many other such websites like Gitlab, Bitbucket, Perforce, Codebase, SourceForge, etc.
- A company can host its own VCS for its product.

### 3.3 Git Features

1. Tracks history.
2. Creates backup.
3. Almost every operation is local (exception: pull, push operations).
4. Scalable.
5. Supports non-linear development.
6. Distributed development.
7. Free.
8. Git has integrity: Git does the **SHA-1 checksum** of all files internally.

> **🔐 Checksum Example**
> 
> Suppose "VINAYAK" sends a 3GB `f1.txt` file to "You". Checksum is a string (e.g., `2196g4c2f6122`). Every file has a unique checksum. If anything is changed in files, the checksum is changed. If I send you `f1.txt`, our checksum should match; if not, then it has been changed in between. Git takes care that nothing is altered in between.

### 3.4 Git's Three-Stage Architecture

_Install Git in your laptop from its official website only. If you type `git scm` you will get the official website._

![Three-Stage Architecture](../img/img4.png)

1. **Working Directory:** The working directory/tree consists of files that you are currently working on. In this directory you view & modify files.
    
    - _Note:_ The difference between a working directory and a repository is: A Repo is essentially the `.git` hidden folder inside the working directory which tracks the files.
        
2. **Staging Area:** Staging area can be described as the **"Yellow Signal"** of a traffic light. Before you can commit/save/snapshot you stage them. It's a good practice adopted by programmers. The staging area can be considered as a real area where Git stores the changes.
    
3. **Git Directory (Repository):** Git directory means `.git` folder which stores all the data (current & previous commits/saved files) and tracks them and is hidden, hence cannot be seen inside the working directory/folder.
    
**We Follow This Sequence:**

`VERSION 1.0` ➔ `Upgrade` ➔ `STAGE (Fix errors)` ➔ `COMMIT` ➔ `VERSION 2.0`
## CHAPTER 4: The Git File Lifecycle & Tracking

### Learning Objectives

- Understand the four states of a file in Git.
- Learn how to track, stage, and commit files.
- Master ignoring specific files using `.gitignore`.

### 4.1 The File Status Lifecycle

A file in a Git repository exists in one of four states:

1. **Untracked:** Files Git doesn't know about yet. _(Red colour)_
2. **Unmodified:** Tracked files that haven't changed.
3. **Modified:** Tracked files that you edited. _(Red colour)_
4. **Staged:** Files ready to commit. _(Green colour)_

![File Status Lifecycle](../img/img5.png)

#### Example Lifecycle Scenario:

Suppose I have a project containing files: `f1`, `f2`, `temp.css`.

1. `$ git status` ➔ It will say no git repo.
2. `$ git init` ➔ Initialized my project into git repo but is still untracked.
3. `$ git add --a` ➔ Project is now tracking and unmodified.
4. Suppose `f1` is changed ➔ `$ git status` ➔ modified `f1`.
5. `$ git add f1` ➔ modified `f1` _(In green colour)_. `f1` is now staged also and tracked also.
6. `$ git commit -m "Initial commit"`
7. `$ git status` ➔ nothing to commit, working tree clean.

### 4.2 Git Ignore: How to Ignore Files in Git

Suppose I have a project having files `first.txt`, `second.txt`.

1. `$ git init` then `$ git add --a` ➔ Both are tracking.
2. `touch error.log` ➔ `$ git status` ➔ untracked file `error.log`.
3. `touch .gitignore` ➔ Now open the project and open `.gitignore` file. Type `error.log` in it and save and close.
4. `$ git status` ➔ untracked file: `.gitignore`... [Does not show `error.log`].
5. `$ git add .` ➔ tracked all files including `.gitignore`.
6. If I modify `error.log` and save it ➔ `$ git status` ➔ It will not show me modified `error.log` file in Red colour. In fact, it will not even mention its name. It will show working tree clean.

> **💡 Pro Tips for `.gitignore`:**
> 
> - If there are many "log wala files", then type `*.log` in `.gitignore` and all log ones will be ignored.
>     
> - If you wish to ignore a directory/folder, then write it in the `.gitignore` file, but remember it ignores a folder if it's empty.
>     

## CHAPTER 5: Core Git Operations & Commands

### Learning Objectives

- Execute basic Git commands.
- Compare file changes using diff.
- Skip the staging area efficiently.
### 5.1 The Command Cheat Sheet

| **Command**                           | **Description**                                                   |
| ------------------------------------- | ----------------------------------------------------------------- |
| `pwd`                                 | Present working directory.                                        |
| `cd`                                  | To change directory.                                              |
| `git status`                          | To check whether the working directory is git repo or not.        |
| `git init`                            | Initialized git repo.                                             |
| `git add --a` or `git add .`          | This command will stage all files, basically will start tracking. |
| `git add <filename.type>`             | It will track/stage only that file.                               |
| `git commit -m "msg"`                 | It will give message of what is committed.                        |
| `git log`                             | To check who has done commit & when. You will also get hash.      |
| `rm -rf .git`                         | To delete `.git` repo and to lose all tracking.                   |
| `git clone <url> <filename you wish>` | To clone repo from github.                                        |
| `ls`                                  | To list files.                                                    |
| `q`                                   | To quit `git log` & many other commands.                          |

_(Hash: Hashes are what enable Git to share data efficiently b/w repositories. If two files are the same, their hashes are guaranteed to be the same)._

### 5.2 Git Diff

This command shows changes b/w commits / staging area & working directory.

- `$ git diff`: Compares working directory with staging area. _(e.g., If I open `one.txt` file and typed "Hello" and modified it, `git diff` will show me what changes I have made)._
- `$ git diff --staged`: Compares staging area and previous commit.
    

### 5.3 Skipping the Staging Area

Suppose I have a project with only one file `hello.txt`. I initialize and track it.

Now I add another file `hello1.txt` and modify `hello.txt`.

- `$ git status` shows: `modified: hello.txt` and `untracked: hello1.txt`.
    

If I run: `$ git commit -a -m "Direct commit"`

- Result: `untracked: hello1.txt`.
    
    _(Remember: Only tracked files are committed, and command to skip staging untracked files are not committed)._
    
    You then have to `$ git add hello1.txt` to track the new file.
    

## CHAPTER 6: Advanced File Management & Logging

### Learning Objectives

- Rename, move, delete, and untrack files correctly.
- View and amend commit history.
- Restore and reset working directories.

### 6.1 How to Rename/Move and Delete Files

Suppose I have a git repository having files `one.txt`, `second.txt`, all tracked. Working tree clean.

**Renaming (Manual Way):**

Now I open folder and rename `one.txt` to `third.txt`.

- `$ git status` ➔ `deleted: one.txt`, `added: third.txt`.
- _(But I had renamed `one.txt` not deleted, so Git does not understand this)._
- `$ git add --a` ➔ `renamed: one.txt -> third.txt`. _(Now, Git understood that I had renamed)._
    

**Renaming (Git Way):**

If I have a file named `first.txt`:

- `$ git mv first.txt first-renamed.txt` ➔ File in the folder is renamed!
- `$ git status` ➔ `renamed: first.txt -> first-renamed.txt`. _(Here it stages file by default)._

**Deletion:**

Suppose I have a file `one.txt` in my repo.

- `$ git rm one.txt` ➔ `rm 'one.txt'`.
- `$ git status` ➔ `deleted: one.txt`. _(Here Git stages the file deletion)._
### 6.2 Untracking

Suppose I have files `F1`, `F2` and want to ignore `F1`. I put it into `.gitignore` file.

- `$ git status` ➔ modified `.gitignore`.
- `$ git add .` and commit.
- Now I add something into `F1` ➔ `$ git status` ➔ modified `F1`.
- _(You may think why it is showing this since I had put it in gitignore. It is because it was tracking it from start. We have to untrack it)._
    

To untrack:

- `$ git rm --cached F1`
- `$ git status` ➔ `deleted: F1`. _(It is not deleted, only untracked, but Git shows deleted msg)._
- `$ git commit -m "removed F1"`.
- If I add again something into `F1` ➔ `$ git status` ➔ working tree clean.
### 6.3 Viewing and Changing Commits (`git log`)

- `$ git log -p`: Along with commit shows what is removed and added.

- `$ git log -p -2`: Shows what is added & removed for the last 2 commits. _(You can replace 2 with 3, 4, 5, 6, n and it will show that many commits)._
    
- `$ git log --stat`: Shows in short how many lines are added and removed.
    
- `$ git log --pretty=oneline`: Shows commit in one line.
    
- `$ git log --pretty=short`: Shows commit in short.
    
- `$ git log --pretty=full`: Shows commit in long form.
    
- `$ git log --since=2.days`: Filter according to time. _(Instead of days you can add 'months' & 'years')_.
    
- `$ git log --pretty=format:"%h--%an"`: Custom format (`%h` = hash, `%an` = author name). You can also use `%ae` for author email. _(Visit website `git scm` for useful options for git log format)._
    

**Amending Commits:**

If you want to amend your previous commit message then:

- `$ git commit --amend` ➔ It will open an editor.
- `i` = to edit in editor.
- Type `escape :wq enter` = to exit.

### 6.4 Git Commands to Unstage and Unmodify Files

- **To Unstage:** I have a modified first.txt. `$ git add first.txt` (staged). To unstage: `$ git restore --staged first.txt`. `$ git status` shows `modified: first.txt... (unstaged)`.
    
- **To Unmodify:** Now suppose I delete my entire content in `first.txt`. `$ git status` shows `modified: first.txt`. If I command: `$ git checkout -- first.txt` ➔ my entire content will be recovered!
    
    - _(Note: But if I modified it, staged it and then commanded `git checkout -- first.txt` it won't work)._
        
- **Reset All:** If you have modified some files and want to go to previous commit use: `$ git checkout -f`.
    

### 6.5 What is Alias?

Alias means instead of writing big command write it in short form.

For eg. `$ git status` ➔ working tree clean.

If I type `$ git st`, Git will not understand this.

- Command: `$ git config --global alias.st 'status'`
    
- Now `$ git st` ➔ working tree clean.
    

## CHAPTER 7: Branching, Merging, and Collaboration

### Learning Objectives

- Understand isolated environments via branching.
    
- Resolve merge conflicts.
    
- Learn professional branching workflows and remote repository interactions.
    

### 7.1 How to Create Branches and Switch Branches

Suppose we are working on an e-commerce website. The main website which users are seeing is the **Master Branch**. If we try to add features on master branch without creating a different branch and it doesn't work then it can affect income & our brand status.

Therefore, we create a branch (e.g., **Design Branch**) and add features to it which is later on merged into the master branch. In this we don't disturb our master branch.

- _Example of features added in Design Branch:_ Added HTML files, Added CSS, Added Dashboard, Typed JS, Nav bar added, Added ICON, Recommendations, CHANGED BACKGROUND COLOUR. Then merged design into master.

![Branching Example](../img/img6.png)

### 7.2 Core Branching Commands

1. `$ git checkout -b <name of branch>`: To create a new branch and switch to a new branch (e.g., `develop`).
    
2. `$ git checkout master`: To return back to master branch.
    
    - _Example:_ Suppose your master branch contains files `F1, F2, F3, F4, and temp.csv` and you command `git checkout -b develop` and switched to new branch and deleted `F1` & `F2`. If you return back to master branch using command `git checkout master` all the files will be recovered.
        
3. `$ git branch`: To show all branches out there.
    
4. `$ git merge Develop`: If you want to merge branch 'Develop' into 'Master' branch. Make sure you're in master branch. `$ git merge Develop` ➔ Whoopee merged!

### 7.3 Merge Conflicts

Merge conflicts happen when there is an **Issue 1**, resulting in **Result A** on the Master Branch and **Result B** on the Feature Branch. Git asks us as to which result you would love to merge Result A or B into the main branch.

![Merge Conflict Timeline](../img/img7.png)
_Commit timeline:_

- `$C0` = initial commit
- `$C1` = next commit on top of C0
- `$C2` = next commit on top of C1 and so on

If you use VS code editor, it will mark two choices with conflict resolution markers which looks like:

```
<<<<<<< HEAD
(Master Branch Result A)
=======
(Feature Branch Result B)
>>>>>>> branch-name
```

Obviously, in real time projects you will have two or more outcomes and you can do merging using git command: `$ git add filename.type`. _(Just make sure that while merging you are in master branch and applying this git command there)._

### 7.4 How to Manage Branches: An Advice from a Sr. Engineer

> 💡 **Sr. Engineer Advice**
> 
> In git making branches is not expensive, it does not require storage, it only saves only changes and leaves a pointer on previous commit.

- `$ git branch -v`: Shows commit hash and commit msg (e.g., `* master 9761972xx Fixed bug`).
    
- `$ git branch --merged`: It will show branches you are currently in + branches you had merged.
    
- `$ git branch --no-merged`: It will show branches you have not merged.
    
- `$ git branch -d develop`: Delete branch name. _(It will first give error to confirm that you are not deleting by-mistakely and will ask you to type capital D)._
    
- `$ git branch -D develop`: Then it will delete branch!
    
### 7.5 Branching Workflow

1. **Long Running Branches:** This branches as name indicates are long. They exists till the project exists. Example: `master`, `develop`, `design`. Master branch will contain main code, in develop your development will be done & same with design, they all are long running keep upgrading project.
    
2. **Topic Branches:** It is a short lived branch that you create and use for a single particular feature work. They are typically light weight branches that you create locally and that have a name that is meaning-full to you.
    
### 7.6 Pushing Git Branches in Remote Repositories

To do this, go to the branch you want to push.

For example: If I want to push `develop` branch into remote repo I should be in develop branch (If you're not use git command - `git checkout develop`) and then to push it use command:

`$ git push origin develop`

_[Remember make sure to commit & check git status before pushing your branch into remote repo]._

If you want to name develop branch here in your local system to `newdevelop` (or `neurdevelop`) in remote repository, use command:

`$ git push origin develop:newdevelop`

**KEEP CONTRIBUTING, KEEP GROWING!**
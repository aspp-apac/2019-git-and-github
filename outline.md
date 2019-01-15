# 1.0 A quick review of git basics:

Covered commands:

* `git config`
* `git init`
* `git clone`
* `git add`
* `git commit`
* `git status`
* `git log`

#### Setting up git

We want git to record changes with authorship, so it's clear who changed what and when that happened. There are many options that we can set with `git config`, but today we'll refresh the basics

Identity:
```
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
```

Preferred Text Editor (used by git to modify commit messages, among other things):
```
git config --global core.editor "vim"
```
you can look up how to set your preferred editor [here](http://swcarpentry.github.io/git-novice/02-setup/index.html)

An aside: we can change git settings for repositories only, or for the entire system. This is up to your preference, but perhaps you have a project associated with a lab and want to change your user e-mail only for that particular project. You'd change the `user.email` option in the repository rather than for your whole user space. Changing config options is up to your use and needs.  

* locally with `git config [options]` or `git config --local [options]`. The config options are stored in `$REPOPATH/.git/config`. Your current working directory will need to be a a working git repository in order to set config options at this level.
* globally (for a particular user) with `git config --global [options]`. The config options are stored in `~/.gitconfig`
  * for windows: `C:\Users\username`
  * for apple: `/Users/username`
  * for linux: `/home/username`
* system-wide with `git config --system [options]`

tips:
- if you change your user config settings to and e-mail not associated with your remote (like github), you might have some issues pushing.
- you can modify your config on the command line or by editing the config files mentioned above.
- you can check your config settings by opening the config file or by executing `git config --list` or `git config -l`

#### Creating a repository

* To initialize a new repository from the command line: `git init` (this option doesn't require internet access or a github account)
* We can also get an existing repository from a remote server with `git clone https://github.com/orgname/reponame.git`. This command will create a new folder called **reponame** in your current working directory and will copy the contents of the remote repository into that folder. (this option requires internet, and depending on permissions you may need a github account)

We can check that a folder we're in is a git repository by executing `git status`. If the folder isn't a repository, git will tell us `fatal: Not a git repository (or any of the parent directories): .git`. We can also check by listing all files and folders (including hidden ones) in our directory with `ls -a`. A git repository will have a **.git/** folder that contains the history of our repository.

tips:
- each repository should be in its own folder, not in a subdirectory of another version-controlled folder
- every time you work on a project on a new computer you'll need to update your git config settings to ensure you have proper credit for the things you author
- if you have different config settings locally vs. globally the more refined config settings will override something more global. In that vein, local > global > system.

#### Tracking Changes

If you haven't yet, make a new project folder, navigate into it and then initialize the repository.
```
$ mdkir dissertation
$ cd dissertation
$ git init
Initialized empty Git repository in /Users/madicken/repos/dissertation/.git/
```

Our most used commands in git will be the following:
* `git add` will add a file to the staging area
* `git commit` will save or commit our staged files to
* `git status` will return information about the existing state of our repository.
* `git log` will show the commit log

Now that we've initialized an empty repository in `/dissertation/`, we can check the status:

```
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

A file in a git repository can be in one of four states: *untracked*, *unmodified*, *modified*, and *staged*. When we go through the process of editing a file, adding it, and committing it, we're cycling through these different states. These states are reflected when we use `git status` to look at the status of a directory. Let's create go through this process with regular `git status` checks and see what this looks like.

```
$ vi AUTHORS.md
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	AUTHORS.md

nothing added to commit but untracked files present (use "git add" to track)
$ git add AUTHORS.md
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   AUTHORS.md
$ git commit -m 'add my name to author list'
[master (root-commit) 96c67ed] adding my name to author list
  1 file changed, 1 insertion(+)
  create mode 100644 AUTHORS.md
$ git status
On branch master
nothing to commit, working tree clean
```

Here we've seen AUTHORS.md go from untracked -> modified -> staged -> unmodified. We can check the log to see what our history looks like.

```
$ git log
commit 96c67ed10232a25c6d8a1e6eb64e0c25b54d7e34 (HEAD -> master)
Author: Madicken Munk <madicken.munk@gmail.com>
Date:   Mon Jan 14 16:53:20 2019 -0600

    add my name to author list
```

The series of numbers and letters in the first line after the command is what is known as the *commit hash*:a unique identifier that is used to mark this particular snapshot of our repository. Note that this is the same identifier that git returned to us when we committed our changes, but only the first seven characters were shown.

If we choose to commit with `git commit` and no arguments, git will enter into a text editor. This is useful if we have a large set of changes that we want to describe more fully. The first, short commit message should be the TL;DR of our changes, while the longer detailed message might list specifics.

```
short, descriptive message for my dev work

Here I describe in detail a little more about the dev work that I did. Maybe I added a few new functions. I could list them here.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#       modified:   AUTHORS.md
#
```

When we save and exit the editor after writing out our commit message this way, git will return a similar message as before.

```
$ git commit
[master 2d701bb] add my name to author list
 1 file changed, 1 insertions(+)
```

Tips:
- when committing I personally like to use the shorthand `git commit -m "This is my message"`, but you can be more verbose with `git commit --message` or enter straight into a your preferred text editor with `git commit`. You might prefer to go into the text editor if you have a lot of changes to describe.
- any of the git commands can be followed a `--help` or `-h` option to learn more about what options are available to you
- If you're working with changes in many files, you can add all updated files to the staging area with `git add -u` and all files to the staging area with `git add -a`

#### Exploring History

The log will tell us about the history of the branches that we're on. I'm going to step out of the toy repository we've been working in to something a bit more complex to demonstrate the power of `git log` and its ability to tell us about our history.

A standard execution of `git log` will show us as much of the log that will fit into our shell's buffer at a time. At the bottom of the buffer you should see a `:`. This is the shell prompting you for navigation. You can page up or down within the log, or you can exit by pressing you `Q` key. Some of the log messages that were in the buffer may be printed in the shell when you exit.

Maybe we're only interested in the last few log messages. We can print only a designated number with `git log -n [number]`. Here I am printing the three most recent commit messages on matplotlib's master branch:

```
~/repos/matplotlib(master) $ git log -n 2 --sparse
commit a552780fa074feaa54750a9dbe935392f24f6576 (HEAD -> master, origin/master, origin/HEAD)
Merge: a728b91c9 4ef57532d
Author: Nelle Varoquaux <nelle.varoquaux@gmail.com>
Date:   Mon Jan 14 13:21:39 2019 -0800

    Merge pull request #13107 from anntzer/bboxbase

    Cleanup BboxBase docstrings.

commit a728b91c958f53eae1e41d38b2b6006f54666bcf
Merge: 2502fe6f0 2585d9fe2
Author: Nelle Varoquaux <nelle.varoquaux@gmail.com>
Date:   Mon Jan 14 13:20:18 2019 -0800

    Merge pull request #13108 from anntzer/capitalize-docstrings

    Capitalize some docstrings.
```

Sometimes we don't need the entire log message printed out in such a detailed format. We can get a condensed version of the log with the `--oneline` flag. Here's an example printing the last 10 log messages from matplotlib's master branch:

```
~/repos/matplotlib(master) $ git log -n 10 --oneline
a552780fa (HEAD -> master, origin/master, origin/HEAD) Merge pull request #13107 from anntzer/bboxbase
a728b91c9 Merge pull request #13108 from anntzer/capitalize-docstrings
2502fe6f0 Merge pull request #13115 from timhoffm/check-sphinx_copybutton
46350268f Merge pull request #13151 from timhoffm/doc-radiobutton
57d031d23 Merge pull request #13178 from anntzer/derole
beed2d80e Merge pull request #13089 from anntzer/quivermatrix
aef686b43 Merge pull request #13179 from anntzer/axis_artist-deprecated
d9d3bdb49 Avoid calling a deprecated API in axis_artist.
bacea6a99 Remove :func: markup from mlab docstrings.
6b3c015da Merge pull request #13047 from timhoffm/doc-contourf-extend-cmap
```

We can return to previous states in our repository with the commit hashes that are listed in the log. Here I'll go back a few commits:

#### Ignoring Things

What if you have a series of large data files that you'd like to put into your repository folder, but version controlling them isn't necessary? We can *ignore* files and entire folders from being tracked by git. Let's say I get a data file called `mydata.h5` and I want to ignore it. This is the series of commands that I'd execute to make that happen.  

```
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	mydata.h5

nothing added to commit but untracked files present (use "git add" to track)
$ vi .gitignore
$ cat .gitignore
mydata.h5
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

Note that once I've modified my .gitignore to include `mydata.h5` git will no longer show it as an untracked file. But since I've created a new .gitignore file that is something that I'll need to add and commit to my repository.

.gitingore files accept directories and wildcards to ignore entire subsets of files within the subdirectory structure of your repository.

```
$ cat .gitignore
*.zip
build/
mydata.h5
```

This particular .gitignore file will ignore all files ending in .zip, everything in the build folder, and a hdf5 data file called mydata.

# 2.0 Deleting and Canceling

Covered commands:
* `git rm` vs `rm <filename>`+`git add <filename>`
* `git mv` vs `mv <filename> <filename2>`+`git add <filename> <filename2>`
* `git diff`
* `git reset HEAD <filename>`
* `git checkout -- <filename>`

# 3.0 Branching

Covered commands + concepts:
* `git branch`
* `git checkout`
* detached head state

# 4.0 Merging

Covered commands + concepts:
* `git merge [branchname]`
* `git merge [branchname] [otherbranch]`
* merging vs. rebasing

A quick aside on rebasing:

Some projects prefer to use a rebase-based method for development.

# 5.0 Conflicts  

Sometimes we can't automatically merge a branch into its desired destination. When that happens 

# 6.0 Remotes

Covered commands + concepts:
* `git remote add [name] [url]`
* `git pull`
* `git fetch` and `git merge`
* `git push`
* forking
* pull requests
* comparing changes

# 7.0 A few extra git things!

#### Aliases

Sometimes we find ourselves looking up the same git command over and over again on stackoverflow. We can customize git with aliases, or shortcuts that are associated with a a particular configured command. For example, I use `git checkout -b [mynewbranchname]` a lot, so i could alias this with

```
git config --global alias.sprout "checkout -b"
```

As with other config options, we can check our aliases with `git config --list`. If we have a lot of config options, we can further pipe that to filter out only alias commands with `git config --list | grep alias`

#### Work in progress

What if you're working on something and somebody pushes changes to your project remote that are important to what you're doing? You could commit with a work in progress commit, but maybe that's not helpful to you right now. Enter `git stash`. What stashing does is "stashes" your changes in your repository and cleans your working area. What this looks like in practice is:

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   cats.md

no changes added to commit (use "git add" and/or "git commit -a")

$ git stash
Saved working directory and index state WIP on master: f7ae976 making notes on cats

$ git status
On branch master
nothing to commit, working tree clean
```

We can unstash our changes

reference: https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning

#### Editing a commit

What if you've committed something and realized you've made an error in your commit? Maybe you misspelled something in the commit message? Maybe you forgot to add a closing curly brace at the end of a dictionary in your code? Enter `git commit --amend`

######  Scenario 1: fixing a commit message

Let's say that I accidentally mess up my commit message
```
$ git commit -m 'this commit is missssspelled'
[master c86fefb] this commit is missssspelled
 1 file changed, 1 insertion(+), 1 deletion(-)
```
I can use `git commit --amend` immediately after to pop into most recent commit message file and edit it. (note: just like with git commit on its own, this will pop you into your chosen text editor that you specified at the beginning of the lesson). After we close out and save, git will tell us about our amended message.
```
$ git commit --amend
[master 59a2d70] this commit is not misspelled anymore!
 Date: Sun Jan 13 22:48:30 2019 -0600
 1 file changed, 1 insertion(+), 1 deletion(-)
```
*note that the commit hash has changed from **c86fefb** to **59a2d70** in this example*

######  Scenario 2: Adding additional changes to the most recent commit

Let's say now that I also forgot to add some changes that I wanted to include in my commit. I can again use `git commit --amend` to update my commit. This is the process I'd need to follow:
```
$ git add cats.md
$ git commit --amend
[master 4e624b8] this commit is not misspelled anymore!
 Date: Sun Jan 13 22:48:30 2019 -0600
 1 file changed, 2 insertions(+), 2 deletions(-)
```

Again, when I execute the --amend command I am put into my text editor so I could additionally modify the commit message if necessary.

*note that the commit hash has changed from **59a2d70** to **4e624b8** with this second amend*

Note: because amending a commit changes the hash associated with the commit, if you've pushed changes up to github already you'll need to *force push* to "rewrite history".

reference: https://www.atlassian.com/git/tutorials/rewriting-history

#### Adding only part of a file to the staging area

What if you've modified a file in a few locations and realize that part of your work thematically would be better in a different commit? What if your text editor deletes whitespaces at the end of lines and you don't want to commit that? We can interactively add part of the file with `git add --patch <filename>`

When this command is executed, git go through, chunk by chunk, and ask you if you'd like to add this file or not to the staging area with:
`Stage this hunk [y,n,q,a,d,/,j,J,g,s,e,?]?`

The options are as follows:
* y stage this hunk for the next commit
* q quit; do not stage this hunk or any of the remaining hunks
* a stage this hunk and all later hunks in the file
* d do not stage this hunk or any of the later hunks in the file
* g select a hunk to go to
/ search for a hunk matching the given regex
* j leave this hunk undecided, see next undecided hunk
* J leave this hunk undecided, see next hunk
* k leave this hunk undecided, see previous undecided hunk
* K leave this hunk undecided, see previous hunk
* s split the current hunk into smaller hunks
* e manually edit the current hunk
* ? print hunk help

When you're finished, you'll see with `git status` that the file is both in the staging area and not in staging.

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   cats.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   cats.md
```

# References:

The following links you may find useful to supplement this lesson. Many were heavily referenced to construct this lesson as well!

The pro git book:
* https://git-scm.com/book/en/v2

Previous course material:
* http://members.cbio.mines-paristech.fr/~nvaroquaux/teaching/2014-spss/git.html#slide1
* http://git-lectures.github.io/ and https://github.com/NelleV/git-courses
* https://python.g-node.org/python-summerschool-2013/_media/emanuele_olivetti_python_school_2013_git.pdf

Other git lessons:
* http://swcarpentry.github.io/git-novice/
* https://learngitbranching.js.org/
* https://jni.github.io/git-tutorial

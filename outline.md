# 1.0 A quick review of git basics:

#### Setting up git

```

```

#### Creating a repository

* To initialize a new repository from the command line: `git init`
* We can also get an existing repository from a remote server with `git clone https://github.com/orgname/reponame.git`. This command will create a new folder called **reponame** in your current working directory and will copy the contents of the remote repository into that folder.

We can check that a folder we're in is a git repository by executing `git status`. If the folder isn't a repository, git will tell us ``

A note: each repository should be in its own folder.

#### Tracking Changes

#### Exploring History

#### Ignoring Things

# 2.0 Deleting and Canceling

# 3.0 Branching

# 4.0 Merging

# 5.0 Remotes

# 6.0 Conflicts  


# 7.0 A few extra-advanced git things!

#### Work in progress

What if you're working on something and somebody pushes changes to your project remote that are important to what you're doing? You could commit with a work in progress commit, but maybe that's not helpful to you right now. Enter `git stash`. What stashing does is "stashes" your


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

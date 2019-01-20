# Condensed Git + Github

### Setup

`git config --global <option>` configures git settings. At minimum, you should set:
* `user.name "Your Cool Name"`
* `user.email yourmail@domain.com`
* `core.editor -flag yourfavoriteeidtor`

You can check config settings with `git config --list`

You can also configure locally and system-wide with:
`git config --local`
`git config --system`

### Creating a repository

Two options:
* `git init` in an existing folder
* `git clone https://github.com/username/reponame.git` to get an existing repository

### Tracking Changes

The general process to track changes in a repository
* edit your file(s)
* `git status` to check that the status of the file/repository
* `git add <filename>`
* `git commit -m "Short, descriptive message of change"`
* `git status` to check that the working directory is now clean
* `git log` to see that your commit shows up

### Deleting, Cancelling, Unstaging

* `git rm <filename>` will remove the file and show the changes in the staging
area. This is the same as `rm <filname>; git add <filnename>`
* `git mv <file1> <file2>` will rename file1 to file2. This is the same as `mv
file1 file2; git rm file1; git add file2`
* `git reset HEAD <filename>` will unstage a file that has been staged for
commit
* `git checkout -- <filename>` will bring us back to the version of the file of
our last commit. It will permanently remove any changes that haven't been
committed.

### Branching, Merging, Checkouts

* `git branch <branchname>` creates a new branch called branchname off of HEAD
* `git branch <newbranch> <oldbranch>` creates a new branch called newbranch
off of oldbranch.
* `git branch -d` will delete a local copy of a branch
* `git checkout <branchname>` will move HEAD from its current location to the
most recent commit of branch branchname.
* `git checkout -b <branchname>` will create a branch branchname off of the
current branch, and move HEAD from the current branch to branchname.
* `git checkout <commidID>` will move HEAD from the tip of the current branch
to a commit. This will put you in detached HEAD state.
* `git merge <branchname>` will merge branchname into the current working branch

### Working with a Remote

* `git remote add <remotename> <url>` will add a remote by remotename to your
repository and it will be associated with the specified URL.
* `git remote rm <remotename>` will remove a remote called remotename
* `git fetch <remote> <branch>` will get a copy of branch from remote.
* `git merge remote/branch` will merge remote/branch into the current working
branch.  

### Github specifics

* A **fork** is a copy of a repository associated with your user account. You
often will not have push permissions to a project, but you will always have
push permissions to your own fork. You almost always want to set `origin` to
track your fork and set the organization's home repo to `upstream` or something
that will be memorable for you.
* A **pull request** is a request to a project to pull your changes (i.e.
  fetch+merge) your changes into a particular branch. Pull requests can be
  located on the same remote (e.g. project/coolfix to project/master) or from a
  fork (e.g. youruseraccount/coolfix to project/master).
* An **issue** is a report of unexpected behavior in a project or an error/bug
report.
* You can reference issues in pull requests and other issues.
See:https://help.github.com/articles/closing-issues-using-keywords/ These
references help make repository maintenance easier. If a PR is merged, issues
can be automatically closed if proper language is used in the reference.

### Repo Hygiene

* All of your repositories should have a license file and a readme. The   
license can protect you and your work and ensure you get proper attribution for
what you're putting online. The readme can help interested users and individuals
to know more about the repository without digging into the code. This is also a
good place to link work that you reference in your repository and also direct
users how to install or build the work in the repo. github automatically renders
README files in each folder.

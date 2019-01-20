# Section 1.0:

Let's assume we're all writing a paper to a forward-thinking journal that plans
to have the entire paper written and reviewed with version control and on
github. This journal is also very permissive and is allowing you to write
everything in markdown (wow! So cool!). Right now, you're at a internet-free
writing retreat, so you're going to start version-controlling your work on your
computer without github for a while.

* set your config settings for your user name and email.
* check your config settings. Do you see anything interesting? What text editor
are we using in this workshop?
* If you haven't yet, create a github user account. Make sure the e-mail
address matches whatever you set in your config settings.
* check your configuration settings with `git config --list`
* navigate into a directory where you want to store repositories that makes
sense to you. (e.g. I like to store all git repos in a folder called ~/repos/)
* clone our example repository for this lesson at:
* Explore the log of the repository
* create a new file called introduction.md and edit it to include a
one-sentence introduction for a paper on your research.
* check the status of this file
* add the file to the staging area
* check the status of the file
* commit the file
* check the log of the repository again. Does it look different? How?

# Section 2.0: Deleting, Cancelling, Unstaging

* create a new file called results.md and add a sentence or two to it.
* add this file to the staging area
* remove this file from the staging area
* add this file back to the staging area
* commit this file
* move this file to a file called conclusions.md
* check that you've moved it with git status
* move it back to results.md
* check what it looks like with git status now that you've moved it back
* add another few sentences to this file that describe your results in more
detail.
* check that the changes exist with git status
* use git checkout to remove the changes of the file
* check the file status with git status

# Section 3.0: Branching

* create a new branch in your research paper repo called `appendices` and
checkout to it
* check out a previous commit on that branch. We discussed `detached HEAD`
state before. What does it look like? Try `git log` and `git status` in this
state. Discuss with your partner the different ways you'd go back to the most
recent commit of the appendices branch. Try them out. use `git status` and `git
log` to help you.
* After this, `git checkout appendices`
* Make a new file related to an appendix you plan to put in your paper. Add
some text to it, then add it to staging and commit it.
* Go back to the master branch. Try to delete the `appendices` branch with `git
branch -d`. What does it look like?

# Section 4.0: Merging

* check out master. Look at the history of this branch.
* check out `appendices`. Look at the history of this branch.
* Merge your appendices branch into master.
* If you're not on master, check out master and look at the history.
* Now try to delete the appendices branch like you did before. What happens?

# Section 5.0: conflicts

* check out the branch `background` look through its history.
* go back to master
* try to merge background into master. What happens?
* check the status with `git status`
* open and edit the file that has conflicts. Save your resolved conflicts.
* check the status again with `git status`
* add and commit your changes

# Section 6.0: remotes:

* check the remote URL with `git remote -v`
* make a fork of the example repository associated with this lesson to your
github user account.
* remove the remote origin
* add the fork of this project as `origin` to your local repository
* add the URL of my repository (the upstream) to a remote called munkm
* push your local master branch up to `origin`
* check on github that the history matches what you see on your local machine.
* fetch munkm/master
* merge munkm/master into your local master
* push this updated master to your new `origin`
* look at your remote repository on github. Does anything interesting show up
now that you've pushed these changes?

# Section 7.0: collaboration

* Look through the list of matplotlib gallery examples that need improvements
(this version of the gallery is built off of the current master branch):
  * Think about a change that would make them clearer. This can be
  documentation or adding code. We've added some suggested changes, but you're
  welcome to do a bit more if you think it would be clearer.
  * A good example to reference (and aspire to) is [this one](https://matplotlib.org/devdocs/gallery/images_contours_and_fields/image_annotated_heatmap.html#sphx-glr-gallery-images-contours-and-fields-image-annotated-heatmap-py)
  * Choose a fix that you want to make. Tell us all what change you want to
  make in the spreadsheet linked in zulip.
* Fork the matplotlib repository to your user account: https://github.com/matplotlib/matplotlib
* Clone the fork to your local machine
* Branch off of master
* Make your fix and commit it on your branch
* Make sure your fix complies with matpltolib's contribution guidelines:
https://matplotlib.org/devel/contributing.html#contributing-pull-requests. Add
and commit changes if necessary.
* Push this branch to your fork.
* Submit a pull request to matplotlib. When you do, link to your pull request
in the zulip chat so we can start reviewing it immediately.

Extra credit:
* look through the other groups' pull requests and submit a review on one of
  them. You can always review a pull request as a non-member of the community
  -- reviews from package users are especially helpful even if they're not core
  developers!
* submit a PR or file an issue to the lesson we did today!:
  https://github.com/munkm/git-github-tutorial/

# Using `git`
This is an introductory repository designed to help understand how the version control program git works and how it can help make collaborating and working on projects easier.

For easier viewing, an **[HTML version](https://htmlpreview.github.io/?https://github.com/utkuboduroglu/using-git/blob/master/README.html)** of the README is also available, which is the recommended version to view this tutorial.

## Why use `git`?
For any sort of project -- not necessarily just programming -- a version control program helps keep track of changes made to said project. Such programs eliminate the need to manually create backups for the project, and allows you to see previous revisions of your files. Because of this, `git`, a version control program, is a really popular choice to maintain a project.

## How it works
Very simply, git keeps track of your edits in a graph. You can check out nodes of this graph to view the previous edits on the project, or commit new nodes to add new changes. These graphs can then be synchronized to cloud services, like Github or BitBucket.

## How do I use `git`?
We will go over the terminal version of git in this tutorial, although you can do everything mentioned here over in a GUI version of git as well.

If you get lost at any step, you can always check out `git --help` to see a help page provided by the program itself.

### Initializing our repository
In order to use git, we need to tell it that we intend to use a directory as a project. We use the command **git init** to tell git that we have a project in our current directory:

<pre>
$ <kbd>git init</kbd>
Initialized empty git repository in .../project/.git/
</pre>

When we run the command, we see the prompt above telling us that we created a git repo in the `project/` directory.

### Cloning an already existing repository
If the project you're going to be working on already exists, you can instead 'clone' that project onto your machine. For example, let's say that you wanted to clone this repository onto your machine. To do this, you would use the clone command of git, and specify a path (either local or online) to a git repository to clone it:

<pre>
$ <kbd>git clone https://github.com/utkuboduroglu/using-git</kbd>
Cloning into 'using-git'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 1), reused 4 (delta 1), pack-reused 0
Receiving objects: 100% (4/4), done.
Resolving deltas: 100% (1/1), done.
</pre>

Although your prompt may not look exactly the same, this is the output you would get, showing where you cloned the project to, and how many objects you cloned. As an exercise, **try cloning this repository onto your machine.** We will use this repository as an example of how a git workflow works.

### Adding changes
After you either created or cloned your repository, you may want to make some edits and tell git to keep track of those edits. For example, open this `README.md` file in a text editor and change the line below:

<pre> <kbd> CHANGE THIS LINE HERE </kbd> </pre>

After you have added your changes, you may want to see what changed in your project. To see the current status of your project, just type `git status`:

<pre>
$ <kbd>git status</kbd>
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add &lt;file&gt;..." to update what will be committed)
  (use "git restore &lt;file&gt;..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
</pre>

Here, git tells you that the file `README.md` has changed, but you have not yet told it to keep track of the file. To do this, you first have to add the file to 'stage' it, i.e. tell it that you plan to send the file. Use `git add` to do so:

<pre>
$ <kbd>git status</kbd>
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged &lt;file&gt;..." to unstage)
        modified:   README.md
</pre>

If you haven't configured `git` before, you may need to enter a name and email for git to be able to tell others who made the changes. To do this, you can use the following two commands:

<pre>
$ <kbd>git config user.name  "Your name here"</kbd>
$ <kbd>git config user.email "your@email.here"</kbd>
</pre>

Now, you're ready to tell git that you have made all the changes you wanted to make, and that you're ready to send off the changes you've made. You can tell this to git by `git commit`, but to commit your changes, you also have to give it a meaningful message that describes what your commit has changed. You can pass your comment directly while committing with `-m "YOUR MESSAGE"`, or you can make git open your defined editor with `-a`. Here, we'll specify the message `"feat: first commit"`, and create our first commit with:

<pre>
$ <kbd>git commit -m "feat: first commit"</kbd>
[master 8cef6be] feat: first commit
 1 file changed, 1 insertion(+), 1 deletion(-)
</pre>

You can see a couple things in this output: the branch we committed our changes to, namely `master`, the id of our commit `8cef6be`, and the description we provided, `feat: first commit`. You can also see how many files we changed, how many characters we added and how many we deleted. This does not necessarily mean we deleted anything, it's just there because of how git keeps track of changes.

### Changes, sending and receiving changes
Right about now, you may want to send your commit to somewhere else, maybe your project is hosted on an online git service like Github. If you cloned this repository, you already have somewhere you can technically send your changes, you can see this with `git remote`. If you also want to see where `origin` points to, you can use `git remote get-url` to see this: 
<pre>
$ <kbd>git remote</kbd>
origin
$ <kbd>git remote get-url origin</kbd>
https://github.com/utkuboduroglu/using-git
</pre>

Now, let's say that you have a change in `master`, and you want to send this change upstream to `origin/master`. You can then do `git push` to push your changes (provided you're currently in the branch `master`):
<pre>
$ <kbd>git push origin master</kbd>
To https://github.com/utkuboduroglu/using-git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'https://github.com/utkuboduroglu/using-git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
</pre>

Uh oh! Seems like there was a change in master that you haven't kept up with. You'll get an error like this if you aren't up-to-date with the branch you want to push to. Fortunately, you can get the recent changes from the upstream branch by `git pull`.
<pre>
$ <kbd>git pull</kbd>
remote: Enumerating objects: 11, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 8 (delta 3), reused 8 (delta 3), pack-reused 0
Unpacking objects: 100% (8/8), 6.15 KiB | 98.00 KiB/s, done.
From https://github.com/utkuboduroglu/using-git
   d20ef60..6987016  master     -> origin/master
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
</pre>

#### Merge conflicts
It seems like we still have problems. We were able to get the changes with pull, but it seems like our changes conflict with something upstream. This is called a 'merge conflict'. We have yet to mention what a merge is, and it will be a bit before we do, but for now, we'll think of a merge conflict intuitively, i.e., that we had an issue 'merging' the upstream branch `origin/master` and the local branch `master` during our `push`. We will not be able to send our changes upstream without fixing all of the conflicts. If you were to check the status of our branch right now, you'd get more relevant information:
<pre>
$ <kbd>git status</kbd>
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 2 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
        modified:   README.html

Unmerged paths:
  (use "git add &lt;file&gt;..." to mark resolution)
        both modified:   README.md
</pre>

It seems that the file `README.md` were edited both upstream and locally. If you open the file, you'll see something like this:
<pre>
<<<<<<< HEAD
Changes made locally
=======
Changes made upstream
>>>>>>> 6987016029c64cd2a25f1f898cddc688bd94c514
</pre>

The content in between `'<<<<<<< HEAD'` and `'======='` are the changes you made locally and wanted to push upstream, and the content in between `'======='` and `'>>>>>>> 6987016029c64cd2a25f1f898cddc688bd94c514'` is what was changed upstream and what you pulled. Notice that `'6987016029c64cd2a25f1f898cddc688bd94c514'` is the id of the commit you pulled, similar to the one from before, but this one is the full id, whereas the one from before was just the shorter version.

It's up to us to resolve the conflict, we may want to keep only one change, we may want to keep both changes, or we may have to do more than just pasting; we may have to rewrite parts of our projects in order to fix it. After we've added our changes, we can remove the lines
<pre>
<<<<<<< HEAD
=======
>>>>>>> 6987016029c64cd2a25f1f898cddc688bd94c514
</pre>

After we made our changes, we have to stage our files and create another commit. The reason we do this is because we actually 'merged' two branches, namely `origin/master` and `master` (one is upstream, and the other is our local branch). If you check the status of the branch, you'll now see:
<pre>
$ <kbd>git status</kbd>
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 2 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   README.html
        modified:   README.md
</pre>

Now when you run `git commit` to resolve the conflict, you can optionally enter a description, but git already creates one for you. You'll receive the following messages:
<pre>
$ <kbd>git commit</kbd>
[master bb63a61] Merge branch 'master' of https://github.com/utkuboduroglu/using-git
$ <kbd>git status</kbd>
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
</pre>

It says that we are ahead by 2 commits. If you want to see what these commits are, you can use `git log` to see them. Here are the mentioned 2 commits.
<pre>
$ <kbd>git log</kbd>
commit bb63a618fcc32ff364d7c1fe069fff6d7729f3c0 (HEAD -> master)
Merge: 8cef6be 6987016
Author: Utku Boduroglu <utkubod@gmail.com>
Date:   Mon Feb 1 00:04:04 2021 +0300

    Merge branch 'master' of https://github.com/utkuboduroglu/using-git

commit 6987016029c64cd2a25f1f898cddc688bd94c514 (origin/master, origin/HEAD)
Author: Utku Boduroglu <utkubod@gmail.com>
Date:   Sun Jan 31 23:37:35 2021 +0300

    chore: setting up push/pull/pull requests
</pre>

We can finally send our merge commit upstream, and again, we do this using `push`. We can explicitly specify which branch to push from, and which remote to push to by `git push <remote> <local-branch>`.
<pre>
$ <kbd>git push origin master</kbd>
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 6 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 530 bytes | 530.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/utkuboduroglu/using-git
   6987016..bb63a61  master -> master
</pre>

### Git branches and merging
You'll recall that we mentioned something called a branch called `master` that we've yet to talk about. We've said that git keeps track of your project in a graph, and so an important part of this graph is that it can have branches that diverge at points and possibly merge at other points, as it was with the merge conflict we resolved earlier. We regularly want to work on changes that we do not want to push onto a main branch, so we create other branches to work on our changes, and merge them onto our main branch when we decide that our changes are ready to be introduced into our project.

If you type `git branch` right now, you'll see that the only branch we have is `master`:
<pre>
$ <kbd>git branch</kbd>
* master
</pre>

It is convention that the first branch to be created in a git project is named 'master', although this is not necessary.

Let's say that you have some other changes you want to make, but do not want to push to master. Then what we want to do is create a new branch, which we can do with the `git branch` command. Let's say that we want to create a branch called `markdown-changes`. If you were to just say `git branch markdown-changes`, you'd notice that no output was produced. So, taking a look at `git branch`:
<pre>
$ <kbd>git branch</kbd>
  markdown-changes
<kbd>* master</kbd>
</pre>

You'll see that although we created the branch `markdown-changes`, we are still in `master`. To switch branches, or checkout as it's called in git, we say `git checkout markdown-changes`, and upon doing so, we'll get a message saying that we switched to the `markdown-changes` branch. Creating a branch and switching to it is so commonplace while using git, you can do all of it with a single command:
<pre>
$ <kbd>git checkout -b new-branch</kbd>
Switched to a new branch 'new-branch'
$ <kbd>git branch</kbd>
  markdown-changes
  master
<kbd>* new-branch</kbd>
</pre>

Let's say that we made new commits in the branch `markdown-changes` and we're sure that we want to introduce this commit to the branch `master`. We can do this by first checking out the branch we have the changes in, namely `master`, and merging the branch with `markdown-changes`.
<pre>
$ <kbd>git checkout master</kbd>
Switched to branch 'master'
$ <kbd>git merge markdown-changes</kbd>
Updating bb63a61..3405081
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
</pre>

If you have any problems while merging, git will tell you that you have a merge conflict. This is what git referred to when we tried to push our commit upstream and we were behind. You may have noticed that git had 'Fast-forward' in the merge output message. This is not that important for now, but we will get to this later on.

### Stashing changes
Let's say that you are working on something in your current branch and you have to do something that would change your working directory, like switching to another branch or pulling. You definitely don't want to restore your changes, but you also have to do what you were doing. Git offers a very useful command for this: `stash`. As the name implies, git can stash your changes so you can do whatever you wanted to do, and give you your changes back when you're done. You can use the command `git stash` directly to stash whatever changes you've made but not comitted.
<pre>
$ <kbd>git status</kbd>
On branch markdown-changes
Changes to be committed:
  (use "git restore --staged &lt;file&gt;..." to unstage)
        new file:   oldfile

Changes not staged for commit:
  (use "git add &lt;file&gt;..." to update what will be committed)
  (use "git restore &lt;file&gt;..." to discard changes in working directory)
        modified:   newfile
$ <kbd>git stash</kbd>
Saved working directory and index state WIP on markdown-changes: e08328f Merge branch 'master' into markdown-changes
$ <kbd>git status</kbd>
On branch markdown-changes
nothing to commit, working tree clean
</pre>
And to recover your changes later on,
<pre>
$ <kbd>git stash pop</kbd>
On branch markdown-changes
Changes to be committed:
  (use "git restore --staged &lt;file&gt;..." to unstage)
        new file:   oldfile

Changes not staged for commit:
  (use "git add &lt;file&gt;..." to update what will be committed)
  (use "git restore &lt;file&gt;..." to discard changes in working directory)
        modified:   newfile

Dropped refs/stash@{0} (735838eebf551a9b87567e1dbc136049eee84590)
</pre>
One cool thing about stashes is just like you can checkout branches and commits, you can also `checkout` stashes! If you had any stashes, you can view them with `git stash list` and checkout the stash you want with its id:
<pre>
$ <kbd>git stash list</kbd>
stash@{0}: WIP on markdown-changes: e08328f Merge branch 'master' into markdown-changes
$ <kbd>git checkout stash@{0}</kbd>
Note: switching to 'stash@{0}'.

HEAD is now at b07b925 WIP on markdown-changes: e08328f Merge branch 'master' into markdown-changes
</pre>
You can undo the checkout with `git switch -`.

### Making mistakes
No one is infallible. We all make mistakes from time to time, and there will probably come a time when you've made a mistake and want to fix it. For example, we have previously merged `master` and `markdown-changes`, and let's say that since then, we've added a new commit onto `master`. We have later on decided that this commit should not be in our project and wish to remove it. We can use the command `git reset` to do this. Although reset does many other things, for our purposes, the following command 'forgets' our most recent commit:
<pre>
$ <kbd>git reset --hard HEAD~1</kbd>
HEAD is now at 3405081 feat: added things
</pre>

We have not explained what `HEAD` is, but you can think of it as a pointer that points to either a branch or a commit. All your work is actually stored in this `HEAD` pointer, and actions like committing depend on it. `HEAD~1` is just a pointer to the commit 1 before the commit `HEAD` points to; we tell git to act as if the tip of our branch is `HEAD~1` instead. If we want to point to the previous commit, we can also use the notation `HEAD^`, and if we have a specific commit that we want to roll back to, we can just use its id, like the ones from before; both long and short ids will work fine.

Let's say that you were too late in recognizing your mistake, and you pushed the commit you wanted to delete. In this case, it is extremely dangerous to reset the pushed commit, as other people may have already pulled it to their machines, and the reset may mess with their workflow. Instead, git has another feature that allows us to create another commit that basically reverts all the changes we made in the erronous commit, appropriately named `git revert`. Let's say that the change we want to revert is pointed to by our `HEAD`. Then we can tell git to revert the commit by
<pre>
$ <kbd>git revert HEAD</kbd>
[master fc8dad0] Revert "chore: setting up git-revert again"
 1 file changed, 1 insertion(+), 1 deletion(-)
</pre>

If we were successful with creating our revert commit, we can push it upstream for people to pull and revert our changes. Git will prompt us to enter a custom message for our revert, but it automatically has one at the ready. We do not necessarily have to revert only one commit; if it is possible, git can revert back to any commit we point to, whether by a pointer or by the commit's id.

### Checking differences 
At any time, you may want to check what you have changed in your workspace, or may want to compare commits to see what the difference is between them. For this, you can use `git diff`. If you have changes in your workspace, `diff` gives you something like
<pre>
$ <kbd>git diff</kbd>
diff --git a/README.html b/README.html
index 2dc9295..3ef35bc 100644
--- a/README.html
+++ b/README.html
@@ -252,7 +252,13 @@ SOME CHANGES
<kbd>+SOME MORE CHANGES</kbd>
-REMOVED CONTENT
</pre>

You'll see three different types of lines: ones that start with '+', ones that start with '-' and ones that start normally, which respectively indicate that a new line has been added, a line has been removed and the line remains unchanged. You'll also see that the header has some relevant information. You'll see the command executed, where the old file is in the 'directory' `a` new one is in `b` (these are not really directories, but git writes it like this for easier reading). The line with `@@` shows what line we were on, how many lines were in the original section, what line we are on in the final edit and how many lines the final section contains. In this case, our section started on line 252 and consisted of 7 lines, and by the time we were finished with our edit, it again started on line 252 and consisted of 13 lines. 
You can use the `diff` command on any two pointers, like commit ids or `HEAD~k`.

### Pull requests
One final thing we should mention is pull requests. If we do not have permission to push changes to a branch, but would like our changes to take place in that branch anyway, we can instead send what's called a 'pull request'. It is possible to use git directly for pull requests, but it is much easier to do it through Github, which we'll use for this section of the tutorial. 

#### Creating a pull request in a project where you can push upstream
Here are the usual steps for creating a pull request:

* If you haven't created any commits you want to push yet, create a new branch and create your commits in that branch. If you have, switch to that branch, assuming that you have permission to push onto that branch, let's say `names`.

* Push the commit you want to push onto the remote; the push command will push `names` to `origin/names` by default.

* After you've successfully pushed your commit onto the upstream branch, you will be able to see the branch `names` in the Github repository, namely at '[https://github.com/utkuboduroglu/using-git/tree/names](https://github.com/utkuboduroglu/using-git/tree/names)'.

* Now, you can create a pull request for the commit we made from [the pulls page in my repo](https://github.com/utkuboduroglu/using-git/pulls).
  - Press the button labeled 'New pull request'.
  - Change the compare branch to `names`.
  - After Github confirms that we're able to merge, press the 'Create pull request' button.
  - In the next page, specify the one-line description of the commit and provide a meaningful explanation as to what the commit is about and why it should be pulled.
  - Hit 'Create pull request' to create your pull request.

After this point, it is up to the maintainers of the branch to look over your pull request, and decide on pulling or not pulling the commit.

#### Creating a pull request in a project where you CANNOT push upstream
If you have no permissions in the project whatsoever, you can still send a pull request, but the process is slightly different. Instead of directly creating a commit and pushing it upstream, you instead have to push your commit to something called a 'fork' of the repository. Here are the steps for creating a pull request:

* Create a fork of the repository you want to create a pull request for. Let's consider creating a pull request for my repository. Visit [https://github.com/utkuboduroglu/using-git](https://github.com/utkuboduroglu/using-git) in a web browser. Sign in to your Github account. Over on the right upper corner, there is a button labeled '`Fork`'. Press it.

* After pressing the fork button, Github will create a repository in your account that is forked from mine. `clone` that repository onto your machine using its link.

* After you clone the repo onto your machine, `checkout` the branch `names` (you may have to use `-b` while using `checkout`) and make your changes and commit them.

* With your `HEAD` pointing to the commit you want to create a pull request for, `push` your commit upstream to your own repo.

* After you've pushed your commit to your fork, the steps are the same as the ones above; you'll be prompted to create a pull request for the initial repo you forked from.

### Creating your own pull request
Let's practice creating your own pull request. Using some of the things you've learned from this page, create a pull request to pull your changes to the `names` branch and edit the line below to state your name and what you thought about the tutorial (be honest `:)` ).

```
[utku] I had a lot of fun writing this!
```

#### Helping out with this tutorial
If you have any changes you think are necessary, or anything you think this tutorial needs, you can submit your changes by sending me a pull request. If I consider your changes appropriate, I will accept them.

This is the basic workflow while using git: we create commits from the changes we make, we push our changes upstream, we pull changes from upstream, and if we have merge conflicts, we resolve them. For a project with multiple maintainers, this turns out to be a more efficient way of working on a project in contrast to working with e-mailing zip files etc. Up to now, what we have shown is sufficient to use git for most use cases. There will probably be things you don't know and things we haven't covered (which is a lot), but you can always refer to:
* git itself by using `git --help`. If you have a specific command you don't understand, you can also do `git <command> --help` to get the specific help page of that command.
* Online documentation, like [this website maintained by the Git community](https://git-scm.com/docs/). 

You're obviously not restricted to these, however. If you want to check out more that is related to git, look at the resources section.

## Some tips
Writing meaningful messages for commits and pull requests is really important for other contributors to understand what the commits/requests are about. [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) is a commit description standard that helps fix some of the problems that occur with ordinary commit messages. It is recommended that you create commit messages following this convention. **Please use conventional commits while writing commit messages.** It helps with readability and [parsing](https://github.com/conventional-changelog/conventional-changelog) commit messages becomes easier.

## Resources
You can check out the following resources to help you learn more about git:

* [Learn git branching](https://learngitbranching.js.org/), a website designed like a game in which you solve levels about using git, with a helpful graph view to help you visualize git's graphs.

* [Learn git in y minutes](https://learnxinyminutes.com/docs/git/), a cheat-sheet website that highlights the uses of specific languages, along with tools like git.

* [gittutorial](https://git-scm.com/docs/gittutorial), a tutorial on git (similar to this one) provided by SCM that explains the commands more thorough than this one.

* The repository [firstcontributions/first-contributions](https://github.com/firstcontributions/first-contributions) is a great repository for practicing creating pull requests.
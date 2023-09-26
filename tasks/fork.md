# Creating a fork

Our next step in learning git and GitHub is designed to prevent the problem we
encountered at the end of our first task. Some of you may have been able to
push your changes to `names.txt` to the repository with no conflicts. However,
the rest of you likely had to deal with a conflict: resetting your changes,
pulling the new changes from the repository stored on the cloud, redoing your
changes, and then pushing the repository. If you were unlucky, you may have had
to do this more than once!

When working on a repository that many people have copies of, the owners of the
repository typically don't want people to have the ability to commit anything
at any time in any way. Version control is only useful if you're able to fully
control the versions that you're dealing with. One solution to this problem
involves creating a fork of someone's repository, making changes there, then
submitting those changes (called "pull requests") to the owner to review. We
will learn how to create a fork of a repository here.

## Forking learn-git

First, we will go back to [the main page](https://github.com/bualpha/learn-git)
for our learn-git repository. This time, instead of clickig the `<> Code`
button, we will instead click on the `Fork` button at the top of the page.

//TODO: insert image circling fork button

When we "fork" a repository, what we are doing is creating a copy of the
owner's repository that we own. GitHub copies all of the contents of the
repository, creating a new repository under our username. You can think of this
roughly as going `Ctrl-C` `Ctrl-V` to someone else's work, sticking your name
on it, and starting to make your own edits to it.

Once you've created your own fork, you'll come to a page that gives you several
settings. The only one you should change right now is the "Description"
section. You can add whatever short description of your new repository you'd
like to. Think of this as tweet-sized; try to keep it to less than 140
characters.

![fork settings](/img/fork/fork_settings.png)

Once you've finished this, congratulations! You should be able to either see,
or navigate to, a page that looks like this (the exact content may be
different):

![your new fork](/img/fork/new_fork.png)

Notice the areas circled. This new fork is a brand new repository under *your*
username. While it is still connected a bit to the original learn-git
repository, you own this copy.

Clone this repository on your computer in the same way you did for the original
repository. Remove your first clone of learn-git, as you won't be using this
anymore - you'll be now working out of your new fork that you've created.

## What's the difference?

Here are some of the main differences between a fork and a clone of a
repository. We'll get into the differences between these and a branch in your
next task.

- Forking creates a copy of the original repo under your GitHub account,
cloning just downloads a copy to your local machine.
- A fork establishes a connection with the original repo, a clone does not. 
- Forks allow you to freely experiment with changes without affecting the
original project, clones do not provide this isolation (as you may have noticed
from your first task).
- Forked repos can be used to create pull requests back to the original
project, clones cannot.
- Forks show up in your GitHub account's repo list, clones do not. This is
because you own your fork, while you don't own a clone of someone else's
repository.
- You can push commits to a forked repo since you own it, you typically cannot
push to the original repo from a clone.
- Forks can diverge over time as you make changes, clones always match the
original repo (so long as you keep up to date with the hosted repository).

If you want more detail on differences between forking and cloning, see
- [Stack Overflow](https://stackoverflow.com/questions/7057194/what-is-the-difference-between-forking-and-cloning-on-github)
- [The Server Side](https://www.theserverside.com/answer/Git-fork-vs-clone-Whats-the-difference)

## Syncing our new fork

Because we are programmers who are not afraid of the command line, we are going
to sync our fork to the original learn-git repository hosted by bu-alpha using
bash. First, we will configure our remote repository; then, we will show how
to update our repository to match the original.

### Configuring a remote repository

First, open your command line (Mac and Linux) or Git Bash (Windows). Navigate
into your fork using the `cd` (change directory) command.

The first thing we'll do is check if we have a remote repository set up for our
fork. Use the command `git remote -v` to list your configured repositories; the
`-v` flag (`verbose`) shows the URLs after the names of our branches. Right
now, we only have one branch (`origin`) and no remote branch configured.

![git remote -v](/img/fork/git_remote_v.png)

To configure our remote branch, we will need to specify the *upstream*
repository to configure. To do this, go back to the original learn-git
repository that is owned by BU Alpha (**not your fork**). Copy the SSH
address if you've configured GitHub using SSH; otherwise, use the HTTPS link
provided. Navigate back to your terminal and paste the link into your command
line at the end of this command (as shown here):

    git remote add upstream git@github.com:bualpha/learn-git.git

Run the command `git remote -v` again. Your terminal should now look something
like this:

![git remote -v again](/img/fork/git_remote_v_2.png)

If you'd like to see the official GitHub page on configuring a remote
repository, check out
[this link here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-repository-for-a-fork).

### Updating your fork

Now that you've configured our fork with the original repository, it's time to
learn how to update your fork. To sync your fork, first run the command 
`git fetch upstream`. `git fetch` allows us to retrieve changes made to another
repository since our last check-in. In this case, we are retrieving the changes
made to our `upstream` repository, which we just configured in the last step to
be BU Alpha's learn-git repository. You should see something like this on
your terminal:

![git fetch upstream](/img/fork/git_fetch_upstream.png)

Now that you've gotten the updates to the original repository, the next step
is to merge your local repository and BU Alpha's repository using the command
`git merge`. Merging bring your default branch (usually `main`) into sync with
the repository you have set as `upstream`, without losing any changes you've
make (unlike sometimes with `git pull`).

Sometimes, you'll see a lovely message like this:

![git merge good message](/img/fork/git_merge.png)

Other times, you'll have to deal with merge conflicts. For now, [check out
GitHub's page](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts)
on handling with merge conflicts. We'll deal with those in a later section.

## Why do we use forks?

You may have seen some of the benefits of forking already. One of the main
benefits of forking is visible in the chaos of the first task. When a repository
allows anyone to push commits to it, this can lead to confusion and a
repository in disarray. As a result, owners of repositories that have more than
one contributor typically don't add other collaborators to their repository,
preferring instead to handle pull requests through forks.

By allowing you to create a copy of someone's repository, forking gives you the
freedom to do as you wish! You can choose to make that repository your own,
going off in a completely different direction than what the original owners
intended. You can also choose to work with the owners and maintainers, helping
with tasks that they want to accomplish, updating the project to accomodate new
tools and changes.

Forks are also the main way your workflow will be structured going forward.
Unless you are working on a personal project or on something where you are the
sole contributor, you will likely be forking someone else's repository, making
changes there, and trying to merge those changes with the larger codebase
(through pull requests). See [this Stack Overflow 
post](https://stackoverflow.com/questions/31209669/github-why-should-i-fork)
or [the GitHub 
documentation](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
for more good reasons on why to use forking when working on projects. We'll get
into the workflow of forks over the next few tasks coming up, as well as how to
use git to manage your project well.

## Forking in the Quantitative Finance Club

You are all going to be working on projects this semester with teammates. You'll
be writing code in Jupyter notebooks, creating papers and presentations, taking
notes, aggregating research materials and links, and doing other things that
require collaboration. While this could be done through something like Google
Drive, an email chain, or frequent meet-ups, using GitHub will allow you more
freedom in what you can do as a team. It will also give you the chance to put
together a professional project that you can add to your resume, your portfolio,
or your website to showcase to companies that might want to hire you. This will
make it easy for them (and others) to evaluate the work you've done.

One of your team members will create your initial repository on GitHub, and
depending on your size and the nature of your project, you will all either be
added as contributors or create individual forks of the repository. Weigh the
benefits and risks of being contributors vs. creating forks before deciding
to do so. Additionally, if your project deals with the BU Alpha organization
on GitHub, you'll be required to fork the specific repository and submit pull
requests for us to review.

Now that you've created and synced your fork, [learn about branching and
merging in git](/tasks/branch.md) with your next task. 
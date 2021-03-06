# SeanMaxVersionControl

Git commands

1.)cherry-pick

    git cherry-pick is a powerful command that enables arbitrary Git commits to be picked by reference and appended to the current working HEAD. Cherry picking is the act of picking a commit from a branch and applying it to another. git cherry-pick can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.

    Atlassian. (n.d.). Git Cherry Pick | Atlassian Git Tutorial. Atlassian. Retrieved 11 September 2020, from https://www.atlassian.com/git/tutorials/cherry-pick

example:

<img src="img/CherryPicking.png>

2.)unstaging

    To remove files from stage use reset HEAD where HEAD is the last commit of the current branch. This will unstage the file but maintain the modifications.

    git reset HEAD <file>

    To revert the file back to the state it was in before the changes we can use:

    git checkout -- <file>

    To remove a file from disk and repo use git rm and to remove a directory use the -r flag:

    git rm '*.txt'
    git rm -r <dirname>

    If we want to remove a file from the repository but keep it on disk, say we forgot to add it to our .gitignore file then use --cache:

    git rm <filename> --cache

    Unstage | GitLab. (n.d.). Retrieved 11 September 2020, from https://docs.gitlab.com/ee/university/training/topics/unstage.html

    Our example:

    We have an html with Hey, It's, Ya and Boi's.
<img src="/img/unstaging1.png" />

    I 'accidently' deleted this component!
<img src="/img/unstaging2.png" />

    Now I can revert it back
<img src="/img/unstaging3.png" />

3.)unmodifying

    Unmodifying a Modified File
    What if you realize that you don’t want to keep your changes to the CONTRIBUTING.md file? How can you easily unmodify it — revert it back to what it looked like when you last committed (or initially cloned, or however you got it into your working directory)? Luckily, git status tells you how to do that, too. In the last example output, the unstaged area looks like this:

    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   CONTRIBUTING.md
    It tells you pretty explicitly how to discard the changes you’ve made. Let’s do what it says:

    $ git checkout -- CONTRIBUTING.md
    $ git status
    On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

        renamed:    README.md -> README
    You can see that the changes have been reverted.

    Git—Undoing Things. (n.d.). Retrieved 11 September 2020, from https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things

    Our example:

    In the example I first modify the read my file and check the git status which shows it has been changed.

<img src="img\gitunmodify1.png">

    I think used git checkout -- README.md to restore the file to before I modified it, and on checking the git status again it was restored.

<img src="img\gitmodify2.png">

4.)undoing

    At any stage, you may want to undo something. Here, we’ll review a few basic tools for undoing changes that you’ve made. Be careful, because you can’t always undo some of these undos. This is one of the few areas in Git where you may lose some work if you do it wrong.

    One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to redo that commit, make the additional changes you forgot, stage them, and commit again using the --amend option:

    $ git commit --amend
    This command takes your staging area and uses it for the commit. If you’ve made no changes since your last commit (for instance, you run this command immediately after your previous commit), then your snapshot will look exactly the same, and all you’ll change is your commit message.

    The same commit-message editor fires up, but it already contains the message of your previous commit. You can edit the message the same as always, but it overwrites your previous commit.

    As an example, if you commit and then realize you forgot to stage the changes in a file you wanted to add to this commit, you can do something like this:

    $ git commit -m 'Initial commit'
    $ git add forgotten_file
    $ git commit --amend
    You end up with a single commit — the second commit replaces the results of the first.

    Git—Undoing Things. (n.d.). Retrieved 11 September 2020, from https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things


5.)rebasing

    In Git, there are two main ways to integrate changes from one branch into another: the merge and the rebase. In this section you’ll learn what rebasing is, how to do it, why it’s a pretty amazing tool, and in what cases you won’t want to use it.

    The Basic Rebase
    If you go back to an earlier example from Basic Merging, you can see that you diverged your work and made commits on two different branches.

    Simple divergent history
    Figure 35. Simple divergent history
    The easiest way to integrate the branches, as we’ve already covered, is the merge command. It performs a three-way merge between the two latest branch snapshots (C3 and C4) and the most recent common ancestor of the two (C2), creating a new snapshot (and commit).

    Merging to integrate diverged work history
    Figure 36. Merging to integrate diverged work history
    However, there is another way: you can take the patch of the change that was introduced in C4 and reapply it on top of C3. In Git, this is called rebasing. With the rebase command, you can take all the changes that were committed on one branch and replay them on a different branch.

    For this example, you would check out the experiment branch, and then rebase it onto the master branch as follows:

    $ git checkout experiment
    $ git rebase master
    First, rewinding head to replay your work on top of it...
    Applying: added staged command
    This operation works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn.

    Git—Rebasing. (n.d.). Retrieved 11 September 2020, from https://git-scm.com/book/en/v2/Git-Branching-Rebasing

<img src="img\rebasing.png">

    6.)stashing

    Often, when you’ve been working on part of your project, things are in a messy state and you want to switch branches for a bit to work on something else. The problem is, you don’t want to do a commit of half-done work just so you can get back to this point later. The answer to this issue is the git stash command.

    Stashing takes the dirty state of your working directory — that is, your modified tracked files and staged changes — and saves it on a stack of unfinished changes that you can reapply at any time (even on a different branch).

    Git—Stashing and Cleaning. (n.d.). Retrieved 11 September 2020, from https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning

    our example: I added the text for stashing, checked to see it was there in the status, and then used git stash to stash it so I can switch branches. I then went back in to the branch and did a git stash apply, and it brought back my previous work that was uncommited..

<img src="img\stashing1.png">
<img src="img\stashing2.png">






    7.)cleaning

    Cleans the working tree by recursively removing files that are not under version control, starting from the current directory.

    Normally, only files unknown to Git are removed, but if the -x option is specified, ignored files are also removed. This can, for example, be useful to remove all build products.

    If any optional <path>... arguments are given, only those paths are affected.

    Git—Git-clean Documentation. (n.d.). Retrieved 11 September 2020, from https://git-scm.com/docs/git-clean


    our example:

    Cleaning removes files that aren't part of the version control. I create a new fiile called anewreadme.md, and ran git clean -f which removed the file from the directory.

<img src="img\cleaning.png">

8.)branching workflow

    The core idea behind the Feature Branch Workflow is that all feature development should take place in a dedicated branch instead of the master branch. This encapsulation makes it easy for multiple developers to work on a particular feature without disturbing the main codebase. It also means the master branch will never contain broken code, which is a huge advantage for continuous integration environments.

    Atlassian. (n.d.). Git Feature Branch Workflow | Atlassian Git Tutorial. Atlassian. Retrieved 11 September 2020, from https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow

    our example:

    For our work flow we created two seperate branches "Sean and Max" using git checkout -b sean etc. We then developed our work on our alternate branches and merged them into master using a pull request.


<img src="img\branchworkflow.png">


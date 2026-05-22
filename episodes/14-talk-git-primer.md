---
title: (Talk) Git Control System
teaching: 20
exercises: 0
break: 0
---

::::::::::::::::::::::::::::::::::::: instructor

Estimated: 15:30 - 16:00

Source: https://fdmrwth.pages.rwth-aachen.de/rdm-overview/modules/coding/git.md

:::::::::::::::::::::::::::::::::::::

## Introduction: Why should I use Git?

I am not exaggerating when I say that there is not a single concept that more changed the way I
work day in and day out than Git. It is the one of the first things I install on a new machine,
one of the first things I start when I start a new project, and one of the first things I teach
to new developers.

If you've ever dabbled in programming before now, you've probably come across a situation where
you wanted to make a change to a file, but you were afraid to do so because you didn't want to
break anything or lose your work. You might have gotten around this my making a copy of the file
and calling it "main2.py" or "main_backup.py". And before you know it you have four or five
slightly different versions of the same file, and you have to start picking through them to
bring your original file back to the state you had in mind.

Git solves this problem by keeping track of all the changes you make to your files, and allowing
you to move back and forth between them at will. It also allows you to share your changes with
other people, and to work on the same files at the same time without stepping on each other's toes.

## Installation

Git is available for all major operating systems, and can be installed from the following links:

- [Windows](https://git-scm.com/download/win)
- [Mac](https://git-scm.com/download/mac)
- [Linux](https://git-scm.com/download/linux)

There are various implemetations of Git, including versions that come built-in to IDEs like
Visual Studio Code or GUIs like GitHub Desktop or TortoiseGit. For the purposes of this guide,
we will be using the command line version of Git. The concepts are the same, but we will type
our commands into a terminal window instead of clicking buttons.

## Configuration

The first thing after installing git is to configure it with your name and email address. This
information will be used to identify you when you make changes to your files. You can do this
as a default for all Git repositories on your computer with the following commands:

```bash
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```

> You can also specify both values for a specific Git repository by omitting the `--global` option
> while you are inside a Git repository.

## Specifying the *main* branch name

Historically, *master* has been the default name for the main branch of a Git repository, but in recent
years it has been replaced by *main*, as the term *master* has some negative connotations. You can set
the global (for your user account) default branch name to *main* with the following command:

```bash
git config --global init.defaultbranch "main"
```

## Creating a Repository

Let's start by creating a new repository. A repository is a folder on your computer, what we call being "Git controlled", in that Git will
keep track of changes. To create a new repository, create a folder
somewhere on your computer and navigate to it in the terminal.

> *Common Commands for Navigating in the Terminal:*
>
> - `mkdir my_folder`
>
>   - Create a new folder called "my_folder"
>
> - `cd my_folder`
>
>   - Change directory to "my_folder"
>
> - `cd ..`
>
>   - Change directory to the parent folder
>
> - `ls`
>
>   - List the contents of the current directory

We'll start by creating a new folder called "git_workshop":

```bash
mkdir git_workshop
```

You can verify that your folder exists by using the command `ls` to see all of the files in the current directory. The folder "git_workshop" should appear in that list.

Next we'll "change directory" to the folder we just created:

```bash
cd git_workshop
```

Once you are in the folder you want to use as your repository, run the following command:

```bash
git init
```

This will create a new repository in the current folder - your terminal should now look like this:

![git init](img/git/git-init.PNG)

The blue "(master)" text at the end of the line indicates that we are currently in a Git controlled
directory called "master".

"master" has always been the default name for the main branch of a Git repository, but in recent
years it has been replaced by "main", as the term "master" has some negative connotations. You can
rename the branch with the following command:

```bash
git branch -m main
```

## Making & Tracking Changes

Now that we have a repository, let's make some changes to it. We'll create a new file in our
directory called `main.py` and add some code to it.

````python
print("Hello, World!")
````

You can do this with the text editor of your choice. Our directory now looks like this:

![git init](img/git/add-file.PNG)

### Checking the status of the repository

If we run the following command:

```bash
git status
```

> `git status` is a great command to just pause and take stock of what is going on in your
> repository. It will tell you what files are being tracked, what files are not being tracked, and
> what changes have been made to the files that are being tracked.

For now, we can see that Git has noticed that we have a new file in our directory, but it is not currently
tracking it:

![git before adding](img/git/git-status-pre-add.PNG)

### Staging (adding) changes

To tell Git to start tracking this file, we need to add it to the staging area. You can think
of the staging area as a place where you put files temporarily, before you send them off to be
stored. We can add our file to the staging area with the following command:

```bash
git add main.py
```

If we run `git status` again, we can see that our file is now being tracked:

![git after adding](img/git/git-status-post-add.PNG)

### Committing changes

So we've added our file to the staging area, but we haven't actually saved it yet. To save the
changes we've made to the file, we need to commit them. We can do this with the following command:

```bash
git commit -m "Add main.py"
```

The `-m` flag stands for "message", and the text that follows it is the message that will be
attached to the commit. This message should be a short description of the changes you made in this
commit.

> Generally, it's good to keep commit messages short and to the point. There are better places to
> put long-form documentation than in your commit messages.

When we run the command, we can see that Git has saved our changes:

![git commit](img/git/git-commit.PNG)

Practice
========

Make a change to the file `main.py` and add/commit it with a message of your choice. Run
`git status` after each step to see what is happening.

If you have time, try making a few more changes to the file and adding/committing them, or adding
a new file to the repository.

### Exploring change history

If we want to see a history of the changes we've made to our repository, we can use the following
command:

```bash
git log
```

This shows you information about each commit, including the commit hash, the author, the date, and
the commit message:

![git log](img/git/git-log.PNG)

## How the magic of Git pays off

So this is maybe not so impressive yet. We've created a repository, added a file, and made some
changes to it. But we could have done all of this with a text editor and a file explorer. Why
should we bother with Git?

Let's imagine we were in a bind - we need to go back to the way our file was before our last
commit. We can do this!

### Checking out past versions

If we run the following command:

```bash
git checkout HEAD~1
```

We can open our file and see that it has reverted back to the state it was in before our last
commit:

![git checkout](img/git/git-checkout.PNG)

If you open our file in a text editor, you can see that it has reverted back to the state it was
in before our last commit.

> `HEAD` is a special keyword in Git that refers to the most recent commit. The `~1` means "one
> commit before HEAD". You can use `~2` to go back two commits, `~3` to go back three commits, and
> so on.

Notice however that the blue text at the end of the line has changed from "(main)" to
"((abcd1234)...))" - this is because we are now in a "detached HEAD" state. This means that we are
not currently on our "main" branch, and that any changes we make will not be saved.

This is great for when you want to look at an old version of a file, but you don't want to make
any changes to it.

If you want to go back to the most recent commit, you can run the following command:

```bash
git checkout main
```

And you will be back on your main branch.

### Working with branches

Say we want to make some changes to our file, testing out some new code or a new way of doing
things, but we want to make sure we can always go back to the way things were before. We can do
this by creating a new branch:

```bash
git branch new_feature
```

This creates a new branch called "new_feature" that is identical to our "main" branch. But it
doesn't look like anything has happend? We have created a branch, but we haven't switched to it
yet. We can do this with the following command:

```bash
git checkout new_feature
```

You should now see that the blue text at the end of the line has changed to "(new_feature)" to
indicate that we are now on the "new_feature" branch.

![git branch](img/git/git-branch.PNG)

> Because programmers are lazy, there is a shortcut for creating a new branch and switching to it
> at the same time. You can use `git checkout -b new_feature` to do both of these steps in one
> command.

When we are done working on a specific feature and we want to make
it available in the *main* branch, we need to merge the feature branch
into the *main* branch.

```bash
git checkout main
git merge my_feature_branch
```

This "classic" form of merging will generate a so-called merge commit
incorporating all changes from the feature branch into the main branch.
Depending on the changes you may need to resolve conflicting changes
during the merge.

Practice
========
In our "new_feature" branch, make a change to the file `main.py` and add/commit it with a message
of your choice.

We can now switch back to our "main" branch with the following command:

```bash
git checkout main
```

If you open the file`main.py` in a text editor, you will see that the changes you made in the
"new_feature" branch are not present. This is because the changes you made were only saved in the
"new_feature" branch, and not in the "main" branch.

We can switch back to the "new_feature" branch with the following command:

```bash
git checkout new_feature
```

And now our changes are back! No more `main2.py` or `main_backup.py` files - we can keep all of
our changes in separate branches, and switch between them at will!


## Remote Repositories

The real power of Git comes when you start working with other people. You can link your local
repository to a remote repository, and push your changes to it. This allows other people to see
your changes, and to make changes of their own, which you can then pull into your version of the
repository.


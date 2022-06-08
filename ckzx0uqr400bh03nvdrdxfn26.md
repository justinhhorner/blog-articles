## Installing Git on macOS and Windows

Imagine we’ve worked on our game for several months (or longer), and one day we lose part or all of the project 😱! Alright, calm down; that didn't happen (hopefully).

Let’s go with a less disastrous scenario. Let’s say you just realized you introduced a bug sometime in the past, maybe a week or so ago. Out of all the scripts in your project, how do you find what changes introduced the bug?

It would be great to have a time machine that could show us changes we’ve made and compare them to our current code to choose what we keep or change. This time machine could also help us in the first scenario where we’ve potentially lost everything in our project. As long as we notify this time machine as we make changes, we can always get back to a recent backup of our project.

Alright, enough about the time machine - I know it’s been overdone, and the analogy is obvious; yes, Git is the time machine.

# What is Git?
[Git](https://git-scm.com/) is one of many Version Control Systems (VCS) that provides a means of managing versions of almost anything, source code, fonts, documentation, books, etc. In addition to the benefits already mentioned, Git supports branching and merging to facilitate collaboration for teams of any size.

That covers what Git is and how it benefits us. The next article will be a gentle introduction to Git where I’ll cover all the basics you’ll need to know to get started.

If you’re on Windows, head to the next section [Using Winget](#heading-install-with-winget-windows). If you’re on macOS, you can skip down to the [Using Homebrew](#heading-install-with-homebrew-macos) section.

# Install with Winget (Windows)

To install Git via Winget, let’s first search to find packages available for `git`.

```
winget search git
```

You’ll see several results. Down the list you should see the following.

```
Name                                Id                             Version
---------------------------------------------------------------------------
...
Git                                 Git.Git                        2.35.1.2
...
```

That’s the package we want. So we can install it using the install command like so.

```
winget install -e --id Git.Git
```

You’re ready to move on to [Verify Installation](#heading-verify-installation).

# Install with Homebrew (macOS)

To install Git with Homebrew, let’s first search to find packages for `git`.

```
brew search git
```

You can also search at brew.sh, which will lead you to the [git formula](https://formulae.brew.sh/formula/git#default). 
Now we’ll install Git.

```
brew install git
```

# Verify Installation

Once Git is installed, open a new terminal session and run the version command.

```
git --version
```

If the installation was successful, you should see the version number output to the terminal.

# Summary

The next step in our development environment setup is complete! Now that we have a VCS, we can commit our work to our local machine and push our project files to a remote repository.

In the next article, I’ll provide you with a gentle introduction to using Git. We’ll cover the commands you’ll need to work through the rest of the tutorial series. You’ll always have a backup of your project and see changes as we work through the series.

Take care.
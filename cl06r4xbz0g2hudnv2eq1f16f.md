## Introduction to Git

As promised in the last article, it’s time we go over an introduction of Git to explain the basics that we'll need to know for this series.

# What is Git?

As a refresher, [Git](https://git-scm.com/) is a distributed Version Control System (VCS) that provides a means of managing the source and versioning of almost anything: code, fonts, documentation, books, etc. Learning how to use Git is valuable outside of game development, as it is used for collaborating on web, mobile, game projects, and more.

By distributed, I mean that the source code is not stored solely on a single, centralized server. Everyone working on a project has a complete copy of the code.

Up to this point, we’ve been using the terminal to install software for our development environment. My hope is that this has given you confidence using the terminal if you’ve never (or rarely) used it before. Why? Because Git is a command-line program! 

Although there are graphical user interfaces for Git, I recommend you learn how Git works via the terminal before using a GUI client, since all of them rely on the same commands under the hood, and it will benefit you greatly to know what they are doing as you click around.

# What is GitHub?

You may have heard of [GitHub](https://github.com) (or [GitLab](https://gitlab.com), [BitBucket](https://bitbucket.org), etc.) before and wondered what they are, and how do they relate to Git. If Git is used to create repositories and make commits locally, GitHub is a remote backup you can sync with. GitHub is a platform that you can push your code to and keep private or share publicly. Git and GitHub are two separate products - GitHub acts as a remote to your local Git repository. This article will focus solely on Git, but we will introduce GitHub later when we create our game project.

# Our First Repository

Git knows nothing about directories on your computer until you tell it to initialize a folder as a Git repository. In this article, we’ll create a temporary folder to use for learning purposes. Let’s do that now.

Create a folder anywhere you’d like and name it something like `intro-to-git` and navigate to it.

```bash
mkdir intro-to-git
cd intro-to-git
```

To initialize our new folder as a Git repository, we’ll use the [init](https://git-scm.com/docs/git-init) command (make sure you’ve changed directory (cd) into the new directory first).

```bash
git init
```

You may see a message similar to this when you run the init command.

```bash
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
```

You probably don’t want to see this each time you create a new repository, so let’s follow the advice to set the default branch name in Git’s global configuration. The name is up to you - run the following command to set the name that future repositories will use.

```bash
git config --global init.defaultBranch <initial-branch-name>
```

Below that, you should see a message indicating you’ve created an empty Git repository successfully. 
```
Initialized empty Git repository in <your/folder/path/.git/>.
```
The `.git` folder is managed by Git and contains the repository data it needs.

# Staging

Our directory is currently empty, so there are no files for Git to track. You can verify this for yourself by using the [status](https://git-scm.com/docs/git-status) command.

```bash
git status
```

Which will output:

```bash
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

Let’s add a new file for Git to track. We’re not focused on the contents of the file, so for simplicity 

I’ll create a text file called `first-file.txt`

```bash
echo 'This is the first file in our git repository!' >> first-file.txt
```

If we run `git status` again, you’ll notice the difference in the output since adding the new file.

```bash
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	first-file.txt

nothing added to commit but untracked files present (use "git add" to track)
```

This brings us to the first important concept to understand about git: staging. When Git tells us that we have untracked files, it is saying that there are changes it knows about, but we have not told Git that we want to *stage* those changes to be committed. Again, untracked files will not be included in a commit until we tell Git that we want them to be staged for a future commit.

In order to stage our new file, we use the [add](https://git-scm.com/docs/git-add) command.

```bash
git add first-file.txt
```

The add command can accept multiple files at once. Say we had two files, `first-file.txt` and `second-file.txt`, we could stage both files to be committed using:

```bash
git add first-file.txt second-file.txt
```

If you had many changes it would be quite cumbersome to have to list them all out this way. Alternatively, you can tell git to stage all of the untracked files in the directory using a period to indicate all.

```bash
git add .
```

Let’s run status once more to see the changed output.

```bash
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   first-file.txt
```

Now that we’ve staged the file, Git is letting us know there’s a file ready to be committed!

# Committing

Creating a new commit is nearly as easy as staging files. As you may have guessed, we use the [commit](https://git-scm.com/docs/git-commit) command to do so. 

Each commit has a message that details the intent of the changes associated with the commit. We provide the message using the `-m` option.

It’s common for the first commit of a repository to have a message of “Initial commit”. Let’s make our first commit now.

```bash
git commit -m "Initial commit"
```

After running this command you may see a message similar to the following:

```bash
Your name and email address were configured automatically based
on your username and hostname
```

Don’t worry about this for now. We will address it in the [Configuration](#heading-configuration) section. For now, focus on the last part of the message.

```bash
1 file changed, 1 insertion(+)
create mode 100644 first-file.txt
```

You just made your first commit! If you run `git status` again, you can see we’re now back where we started with no changes to commit.

```bash
On branch main
nothing to commit, working tree clean
```

# Commit Log

That’s great, we made a commit and gave it a message, but how can we see the history of commits we’ve made? We use the [log](https://git-scm.com/docs/git-log) command for that. Let’s take a look at our first commit.

```bash
commit 3e1a3a547e6c2035a3805a29e792ac245b400ca3 (HEAD -> main)
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Wed Feb 23 23:42:45 2022 -0500

    Initial commit
```

There’s quite a bit to unpack here, so let’s go through each line of the log output.

First, we see a commit hash that starts with `3e1a3a5`. This is a unique hash that identifies the commit. Anytime you want to reference a commit you can use its hash.

After the hash, we see that the commit was made on the main branch. We’ll talk about branching a bit later, but just know that we can have multiple branches and the HEAD is a pointer to the current commit being viewed.

Next up we see author information followed by the date and time of the commit. Author name and email can be set globally and per project. We’ll learn how to customize this in the [Configuration](#heading-configuration) section.

Last but certainly not least we have the commit message that we provided. These messages are incredibly helpful so you know at a glance the purpose of the commit.

To return to the input prompt of the terminal, press `q`.

# Modifications

Now let’s make a modification to our first file and commit it. I’ll update the text and then run `git status`

```bash
echo 'We have updated the file!' >> first-file.txt
```

```bash
git status

On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	      modified:   first-file.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git has tracked our modification to the file, now it’s up to us to tell it we want to stage it for a commit. Remember how to do that, right? Exactly! We need to use `add` to stage the file, and then commit it with the `commit` command. I’ll use the period as a shortcut to stage the file.

```bash
git add .
git commit -m "Modify first-file.txt"
```

Now we should see two commits in the log output.

```bash
commit 01ed0b3f33fdddaf169b057854bc0776b0e8b134 (HEAD -> main)
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Thu Feb 24 00:09:32 2022 -0500

    Modify first-file.txt

commit 3e1a3a547e6c2035a3805a29e792ac245b400ca3
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Wed Feb 23 23:42:45 2022 -0500

    Initial commit
```

# Configuration

Looking at the `Author` section of the log, you can see Git is using an email address ending with `@Justins-iMac.local` by default, which I certainly don’t want to use going forward. To change this, we need to update the configuration.

Configuration in Git can be done at both the global level (which will be applied to all future repositories) as well as the local project level. I typically change the global settings to my personal email address and update local projects when necessary.

You can update your name and email address globally with the config command and global flag.

```bash
git config --global user.name "Your Name"
git config --global user.email "Your Email Address"
```

To confirm your changes, simply use the same commands without providing a value.

```bash
git config --global user.name
git config --global user.email
```

There are more configuration settings for you to explore in the [documentation](https://git-scm.com/docs/git-config).

# Branching

Up to this point, we’ve been working on the default branch, named `master` or `main`. We’ve seen that every time we use the `git status` command, but what is a branch, exactly?

If you think about the commits made in a repository, think about a branch being the latest commit in that repository. In our case, our main branch is a pointer to our latest commit. Let’s look at the log once more to prove this.

```bash
commit 01ed0b3f33fdddaf169b057854bc0776b0e8b134 (HEAD -> main)
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Thu Feb 24 00:09:32 2022 -0500

    Modify first-file.txt

commit 3e1a3a547e6c2035a3805a29e792ac245b400ca3
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Wed Feb 23 23:42:45 2022 -0500

    Initial commit
```

Our latest commit with hash 01ed0b3f is showing that it is the latest commit, which is on the main branch.

The ability to create multiple branches allows us to easily collaborate across teams working on multiple features simultaneously! This means at any point, a branch can be created to work on a new feature, bug fix, or prototype, and later merged back into the main branch.

Let’s create a new branch where we’ll add a second file that we will later want to add to our project. To create a new branch we’ll use the [branch](https://git-scm.com/docs/git-branch) command.

```bash
git branch add-second-file
```

How can we verify that the branch was created successfully? We can list the branches using the branch command with no arguments.

```bash
git branch
```

You will see our two branches, `main` or `master` and `add-second-file`. The asterisks (*) indicates the branch we are currently on, in this case, `main`. We can switch to our new branch using the [checkout](https://git-scm.com/docs/git-checkout) command. 

```bash
git checkout add-second-file
Switched to branch 'add-second-file'
```

After a few commands, we’ve successfully created a new branch and set it as our current branch. You might be wondering if there’s a shortcut so that we can create a new branch and check out it at the same time; yes, there is!

Let’s delete the `add-second-file` branch and recreate it with the shortcut. You can delete branches using the branch command with the `-d` flag. We’ll first need to switch to the `main` branch.

```bash
git checkout main
Switched to branch 'main'

git branch -d add-second-file
Deleted branch add-second-file (was 01ed0b3).
```

Now we’ll use the checkout command once more to checkout to a new branch using the `-b` flag.

```bash
git checkout -b add-second-file           
Switched to a new branch 'add-second-file'
```

If we take a look at the log status you’ll see that HEAD is pointing to the add-second-file branch, which is exactly the same as the main branch because we’ve yet to add a commit in the `add-second-file` branch. 

Let’s go ahead and create a second file, stage it, and finally commit and see how the log output changes.

```bash
echo 'This is the second file that we worked on in a separate branch!' >> second-file.txt
git add .
git commit -m "Add a second file"

1 file changed, 1 insertion(+)
create mode 100644 second-file.txt
```

Here’s the log output showing the new commit.

```bash
git log

commit c54ab495fe188fe6247744142e41008e811d8ccd (HEAD -> add-second-file)
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Sat Feb 26 22:15:06 2022 -0500

    Add a second file

commit 01ed0b3f33fdddaf169b057854bc0776b0e8b134 (main)
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Thu Feb 24 00:09:32 2022 -0500

    Modify first-file.txt

commit 3e1a3a547e6c2035a3805a29e792ac245b400ca3
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Wed Feb 23 23:42:45 2022 -0500

    Initial commit
```

Notice an important difference in the output. Our HEAD, which is a pointer to the current commit, is now on add-second-file, which points to our latest commit. However, the main branch is no longer pointing to the same commit. The last commit in the main branch is behind by one on commit 01ed0b3f33.

This means Git realizes that our new branch is ahead of the main branch by one commit, and when merging `add-second-file` into `main`, it will merge the changes from the new commit into `main`.

# Merging

We’ve talked about the process of merging, but how exactly do we go about merging our new branch into `main`? First, let’s switch to our main branch once more.

```bash
git checkout main
```

Now we can use the [merge](https://git-scm.com/docs/git-merge) command.

```bash
git merge add-second-file

Updating 01ed0b3..c54ab49
Fast-forward
 second-file.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 second-file.txt
```

The response from the merge command tells us exactly what happened during the merge process. Let’s break it down.

First, it states it is updating our main branch (commit 01ed0b3) with commits from the source branch (commit c54ab49).

Next, we see that our `main` branch is able to fast-forward because our main branch pointer can be updated to match the merged branch without the need to create a merge commit. Lastly, we see there is on change in create mode to create `second-file.txt.`

You can probably guess what the log output will be. Let’s take a look.

```bash
git log

commit c54ab495fe188fe6247744142e41008e811d8ccd (HEAD -> main, add-second-file)
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Sat Feb 26 22:15:06 2022 -0500

    Add a second file

commit 01ed0b3f33fdddaf169b057854bc0776b0e8b134
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Thu Feb 24 00:09:32 2022 -0500

    Modify first-file.txt

commit 3e1a3a547e6c2035a3805a29e792ac245b400ca3
Author: Justin Horner <justin@Justins-iMac.local>
Date:   Wed Feb 23 23:42:45 2022 -0500

    Initial commit
```

That’s right, we’re back to both branches pointing to the same commit because they are now identical.

# Summary

I hope you found this introduction to Git helpful. In a future post, we will cover how to host our repository on GitHub and how to fetch and pull commits to your local machine so you’re always up-to-date with the latest work that’s been committed to the remote repository.

Take care.
Stay awesome.
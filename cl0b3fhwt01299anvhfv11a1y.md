## Creating a New Unity Project

It’s finally time to create our Unity project. You’re already somewhat familiar with Unity Hub, and we already have a version of Unity installed (you did install a version of Unity, right? RIGHT? - okay, we'll wait while you install one).

Perfect. Now, let’s get started.

# Create a Unity ID
If you haven’t created a Unity ID yet, let’s walk through the process. Luckily, with a Unity ID, we can obtain a personal license at no cost (unless you consider the cost of creating yet another account). Your Unity ID will give you some incredible additional perks within the ecosystem, like being able to download assets from the Asset Store and get involved in the official forums. 

Let’s go ahead and create an account to get this step out of the way.

Navigate to the [registration page](https://www.notion.so/Creating-a-New-Unity-Project-8b1223086c054143a0aab043119c894f) to create your new Unity ID.

![sign-in-page.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645994310232/5TS5uPsMg.png)

Now let’s sign in to Unity Hub. Click the profile icon to the left of the settings cog, then click Sign in. Sign in with your credentials and you'll be authenticated and navigated back to Unity Hub.

You may have already been asked to obtain a license, but if not let’s do so now. This is a one-time setup step that you shouldn’t have to be repeated on the same machine. Click on the profile icon once more, then click Manage licenses.

![manage-licenses.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645994407373/FH37xGUib.png)

The preference dialog will appear with you navigated to the Licenses tab. Click Add in the top right corner and then choose to get a free personal license.

![free-license.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645994440846/QYgfESSpB.png)

# Create a New Project
Now we can create a new Unity project for our game. Navigate to the Projects tab of Unity Hub, then click New project in the top right corner.

You’ll see a new dialog with many templates to choose from.  We want a Core template, so click the Core tab. Notice that there are multiple versions of the 2D and 3D templates.

![new-project.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645994504865/E5QYOAPIo.png)

A deep-dive into scriptable rendering pipelines is a bit too much for a beginner tutorial series, but just know that Unity has a built-in renderer and scriptable renderers that give you more control of the rendering pipeline, should your future projects require that for higher-fidelity graphics or targeting a performance benchmark for a particular platform.

Our game will start out as a 2.5D prototype and later update the art to be 2D, so the 3D core template using the built-in pipeline is perfect for our needs. Select the 3D template and provide a name and location for the project. The name of the game we’re building in this tutorial is called Akema’s Home, so I’ll name the project “akemas-home”.

Finally, click Create project and wait while the project files are created and the Unity Editor window is launched.

![editor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645994556754/dsh6_0PIK.png)

# Version Control
Now that our project is created, we should create a local Git repository and push it to a remote repository hosted on GitHub (or any similar service you prefer).

Open a terminal session and change directory to the root of your project (in my case, the `akemas-home` folder). Create a new local Git repository in this folder with `init`.
```
git init
```

Before we make our first commit, we should tell Git about files and directories we want it to ignore. Unity needs only a subset of the project folders, as it will generate other metadata files that it needs. We can save space in our repository by excluding these unnecessary files.

The way I typically do this is by using a service at [gitignore.io](https://gitignore.io). In the search field, type Unity and select it from the list, then click Create. You'll be taken to a page with the contents of the gitignore file. Select all the text, copy it and paste it into a new file in your project directory called `.gitignore`.
```
touch .gitignore
pbpaste > .gitignore
```

Now if we check git status we can see the files and directories that will be in our first commit.
```
git log

On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.gitignore
	Assets/
	Packages/
	ProjectSettings/
```

Stage all changes and make your first commit called "Initial commit".
```
git add .
git commit -m "Initial commit"
```

Great, we now have our first commit to the project. Now let's create a remote repository to push it to in GitHub. We can also do this easily from the terminal using the GitHub CLI.

# GitHub Command Line Interface
The GitHub CLI is a very helpful tool to stay productive at the terminal instead of having to go between the terminal and the GitHub website.
![Screen Shot 2022-02-27 at 5.13.14 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646000091910/wtv2mRNfj.png)

You can install this using Winget on Windows or Homebrew on macOS. We've done this many times throughout the series so far, so I'll just provide the commands below.
### Winget
```
winget install -e --id GitHub.cli
```
### Homebrew
```
brew install gh
```

## Authentication
Now we need to authenticate with the GitHub CLI. The command to do this is gh auth login.
```
gh auth login
```
Go through the steps to authenticate via the browser. Now we're ready to create a repo from our project.

## Create Repository
Navigate to the root project folder and run the following command.
```
gh repo create
```
This will initiate a wizard. I'll walk you through each step.
1.  Select "Push an existing local repository to GitHub"
2. Press Return/Enter to use the current directory (make sure you've navigated to the project directory)
3. Press Return/Enter to use the default repository name, or type another name and continue.
4. Provide a description for the GitHub repository, if you want to. Otherwise, just continue.
5. Choose the visibility for the project.
6. Type "Y" to add a remote. This will add the newly created GitHub repository as the remote to our local repository. This allows us to push our changes to the remote.
7. Press Return/Enter to accept the default remote name as "origin"
8. Type "Y" to push our initial commit to the remote repository.

You're done! We now have a repository with our initial commit on GitHub, and we never left the terminal. You can confirm this by navigating to your project in the browser using the following command.
```
gh repo view --web
```

![Screen Shot 2022-02-27 at 5.26.36 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646000974338/99FOrMOKX.png)


# Summary
Now you should have a Unity ID, be signed into Unity Hub, and have created the project we’ll use throughout the rest of the series! Stay tuned for the next article where we’ll walk through the primary windows of the editor and I’ll provide you with my custom layout that I’ve been using for years.

Take care.  
Stay awesome
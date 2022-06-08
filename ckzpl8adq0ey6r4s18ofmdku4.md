## Installing Unity on macOS and Windows

After the [obligatory introduction post](https://blog.justinhhorner.com/lets-make-a-game-in-unity) to the series, I suppose it’s time we set up our development environment with all the tools we’ll need. First up, let’s install our game engine: Unity.

# Installing Unity Hub
I recommend you obtain Unity via Unity Hub. “Sure, but what is the difference between Unity and Unity Hub?” I hear you say. I’m glad you asked, let me explain. 

As the name suggests, it’s the hub for several things related to Unity, but it is not the Unity Editor itself (where we’ll create our game). It gives us a convenient way to create new projects, manage multiple installs of the Unity Editor, manage licenses, learn with microgame projects, and find community resources. Thankfully the team at Unity Technologies has done a great job with the UI/UX to make navigating Unity Hub quick and easy. Let’s get it installed.

# Package Managers
The first option to obtain Unity Hub is via a package manager. If you’re unfamiliar, a package manager is a tool that simplifies the process of installing software (along with its dependencies) via the terminal.

If you're on Windows, follow along in the [Winget](#heading-winget) section below. If you're on macOS, you can skip down to [Homebrew](#heading-homebrew).

## Winget (Windows)
To install Unity Hub via the terminal, I’ll use a package manager for Windows called [winget](https://github.com/microsoft/winget-cli). 
There’s a good chance that winget is already installed on your machine if you’re running Windows 10 1809 (build 17763) or later. Otherwise, I recommended following [README on GitHub](https://github.com/microsoft/winget-cli) to install it.

You can find out if it's installed by opening a new terminal session and entering the command `winget`, which should display a list of available commands.

You can install a plethora of software packages with winget, but how do I know Unity Hub is one of those? I used the `search` command like this:

```bash
winget search "unity hub"
```

Finally, let’s install Unity Hub using the following command.

```bash
winget install -e --id UnityTechnologies.UnityHub
```

Once it’s finished, launch Unity Hub and navigate through the first-time setup to sign in and obtain a license to use. Now you're ready to [checkout Unity Hub](#heading-unity-hub).

## Homebrew (macOS)
To install Unity Hub via the terminal, I’ll use a package manager for macOS called [Homebrew](https://brew.sh). Homebrew is easy to install using the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once the installation is finished, we need to add Homebrew to our `$PATH` so we can execute it in the terminal. There's a `Next steps` section of the brew installation that will give you a couple of commands to do this, so run those commands before moving on.

Now let's open a new terminal session and type `brew`, which should display a list of available commands. Success!

You can install a plethora of software packages with Homebrew, but how do I know Unity Hub is one of those? I used the `search` command like this:

```bash
brew search unity-hub
```

Another way is to search from the website. If I search for Unity Hub with the search field located at the top of the site, I get a result that navigates to [https://formulae.brew.sh/cask/unity-hub](https://formulae.brew.sh/cask/unity-hub).

Finally, let’s install Unity Hub using the following command.

```bash
brew install --cask unity-hub
```

# Download From the Unity Website
If you prefer to download directly from the website instead of using a package manager, navigate to the [downloads](https://unity.com/download) page and download the version for your OS.

# Unity Hub
Once installation is finished, launch Unity Hub and navigate through the first-time setup to sign in and obtain a license to use. After the wizard is complete, you’ll see this window.

![unity-hub-projects.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645016726942/UUOfimLg9.png)

Navigating the menu on the left will guide you through what Unity Hub offers. You can read more about it in detail [here](https://unity.com/unity-hub).

# Install Unity Editor
Finally, we’re going to install the Unity Editor. Navigate to the `Installs` option in the left menu and then click the `Install Editor` button in the top right corner of the window. This will open a dialog to select the version of the Unity Editor you want to install.

![unity-hub-editor-install.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645016915231/14fxiT6kE.png)

I recommend installing an LTS version, which stands for Long Term Support. LTS releases are intended to be the most stable versions - exactly what you want when you’re just starting because you don’t want a fancy new (but buggy) feature of the editor to cause confusion when debugging.

Another consideration is if you are on a mac: choosing between an Intel or Apple Silicon version of the editor. If your Mac has an M1, M1 Pro, or M1 Max chip, then scroll down to the `Other Versions` section and install the version labeled Apple Silicon.

Click the Install button for the version you want and you’ll then see another dialog to choose any additional modules. For this series, I’m going to uncheck all the modules so that we install only the base editor for now.

Unity is not a lightweight tool, so unfortunately it's around 6GB to download for the editor alone, and once the download is complete the installation will begin. This would be a good time to fix some coffee and fix something to eat. Let me know when you’re back. I’ll wait.

# First Time Launch
Welcome back! Now that the editor is installed, let’s create a temporary project and open it to launch the editor for the first time. With any luck, the installation was successful and we’ll see an empty project with no errors.

First, navigate to `Projects` and click the New project button in the top right corner. A dialog will appear with different types of project templates you can choose from. Since this is just a temporary project, we’ll navigate to `Core` and select the 2D template. I’ll leave the defaults, but feel free to change the name and location of the project if you prefer, then click Create project.

![unity-hub-new-project.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645017036801/tLw9HGsd1.png)

Once the project is created, the Unity Editor will launch and you’ll be greeted with a window like this using the default layout. We’ll cover the different windows and buttons of the editor later. You can close the editor and delete the temporary project now if you’d like.

![unity-hub-first-launch.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645016962501/g4DNyArxD.png)

# Summary
You made it through the first part of our development environment setup. Congrats! Hopefully, this was a smooth path to follow to get Unity Hub and a version of the Unity Editor installed. If you encounter any issues, feel free to reach out and I’ll do my best to help.

In the next article, we’ll continue our environment setup by installing Git.
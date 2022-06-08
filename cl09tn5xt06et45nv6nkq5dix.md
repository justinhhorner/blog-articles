## Installing VS Code on macOS and Windows

Continuing our task of setting up a development environment, we now need to decide on and download a code editor to use. As you can probably imagine, there are many choices available to us, many of which are fantastic.

For this tutorial series, I’ll be using [Visual Studio Code](http://code.visualstudio.com/)(VS Code) for a few reasons. VS Code is a free, open-source, and cross-platform code editor that has captured the hearts of many developers for everything from assembly language to game development with C#, C++, Lua, and many other languages.

![vscode-window.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645939556320/8wV7S-1BR.png)

If you’ve been following the series from the beginning, you know the drill to install software via the terminal; so this will be quick and easy to install and set up.

# Winget (Windows)

Install VS Code via winget with the following command.

```bash
winget install -e --id Microsoft.VisualStudioCode
```

# Homebrew (macOS)

Install VS Code via Homebrew with the following command.

```bash
brew install --cask visual-studio-code
```

# Omnisharp
Omnisharp is a tool that provides code completion, sometimes called intellisense, while writing C# VS Code. You don't need to install Omnisharp yourself, consider it built-in to VS Code. However, it has dependencies that we need to install in order for it to work. Let's take care of this now.

On macOS, we need to install the Mono Framework and set [Omnisharp](http://www.omnisharp.net) to use our globally installed Mono Framework. You can download it from [the website](https://www.mono-project.com/download/stable/). Once installed, open the command palette (Cmd+Shift+P) and search for settings (JSON). With the settings file open, copy and paste the following.

```bash
{
    "omnisharp.useGlobalMono": "always",
}
```

For Windows, at the time of this writing, you will need to download and install the [.NET Framework 4.7.1 Developer Pack](https://dotnet.microsoft.com/en-us/download/dotnet-framework/thank-you/net471-developer-pack-offline-installer). I'm sure this will eventually be out-of-date and another version will be required, so please check the Unity documentation or ask on [Unity Answers](https://answers.unity.com/index.html) site if you have any issues later in the series when we create our first script.

With these steps complete, Omnisharp will be able to load our project and provide code completion once we begin scripting.


# Customization

VS Code can be extended with the many extensions available in the marketplace. Since we are going to be coding in C#, we’ll install the C# extension and I’ll also list some recommendations based on my current setup.

## Extensions

You can access your installed extensions and search the marketplace from the extensions menu. Click on this icon in the left-side activity bar.

![Extensions Icon](https://code.visualstudio.com/assets/docs/editor/extension-marketplace/extensions-view-icon.png)

In the top bar, search for C# and download the [C# extension from Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).

You may also want to download the [Debugger for Unity](https://marketplace.visualstudio.com/items?itemName=Unity.unity-debug) extension in case you want to step through code to debug issues. Simply search for it in the extensions panel and install it.

## Theme
There are many themes you can find in the marketplace, but I’ll share what I’m using in case you want to try it. It’s called [Catppuccin Noctis](https://marketplace.visualstudio.com/items?itemName=AlexDauenhauer.catppuccin-noctis).

## Font
I use a font called Fira Code, which is open-source and available [on GitHub](https://github.com/tonsky/FiraCode).

![Fira Code](https://github.com/tonsky/FiraCode/raw/master/extras/logo.svg)

# Summary

We now have our code editor installed and we're ready to start coding! If you have any questions or issues going through this process, feel free to reach out and I’ll do my best to help.

Take care.  
Stay awesome.
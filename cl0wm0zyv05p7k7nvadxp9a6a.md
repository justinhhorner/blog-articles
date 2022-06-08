## Introduction to Scripting in Unity

It’s time we finally start building our prototype! In order to do so, we need to learn about scripting so that we can add behavior to the GameObjects we add to the scene.

This article will be an introduction to Scripting in Unity using the C# (C Sharp) programming language. We’re going to take our time and work through each new concept together. Throughout the series, we will return to these concepts to expand on them when necessary.

If you’ve never written a line of code before, you’re in the right place!

# What is C#?

Let’s first explain what C# is. C# is a general-purpose programming language developed by Microsoft that can be used to build practically anything you can imagine. It’s used to everything from web and native mobile apps to games! Now with the latest versions of .NET, C# can be used cross-platform on macOS, Windows, and Linux.

I’ve been using C# to develop tools and services for years, so excuse my bias when I say Unity made a great choice when they decided on C# as the primary programming language for scripting in the engine.

Want to learn more? Watch [this video](https://youtu.be/BM4CHBmAPh4) where Scott Hanselman and Kendra Havens answer this exact question.

[![csharp-101-video.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647619185206/HjeTC6LtX.png)](https://youtu.be/BM4CHBmAPh4)
# Unity Scenes

We’ve talked about the scene window, but not about scene files. If you look at the project window, you’ll see we have one scene by default called `SampleScene`. For now, think of scenes like different screens of your game. You could have a scene for your title screen, main gameplay screen, story, credits, etc. We will end up with several screens for our game, so it’s will be good practice learning how to create them.

Right-click on the SameplScene and select `Delete` to delete it. Now, right-click on the `Scenes` folder, hover over `Create`, and then click `Scene`. Name the new scene `Game`, since we’re starting with the core game loop for our prototype.

Double click the Game scene file to open it. Don’t save your changes to the current scene if you're prompted to do so.

# Aspect Ratio

We’re going to use the Game window as the preview of what our build will produce. We want our game to target a 16:9 aspect ratio, which we can preview in the game window using the aspect ratio dropdown selection.

![aspect-ratio.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646961984025/9oCk8Rjve.gif)

# Create the Player
Let’s create a primitive representation of our player in the world. You may think we need to download a 3D modeling tool like Blender to make 3D primitives, but no! Unity comes with several models out-of-the-box for us so we can quickly build our prototype within Unity. 

There are several ways to create primitives. The way I prefer is by right-clicking in the hierarchy, hover over  `3D Object`, and select the object you want to create. For our player, let’s create a Cube.

![create-player-cube.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646889254929/Lg1rf8ndz.gif)

We certainly don’t want this to be called Cube, so select the cube and change the name to `Player` in the inspector window. You can also rename it in the hierarchy via right-click and press `Return` while the item is selected (on macOS, at least).

There are some visual changes I’d like to make before we move on. Let’s change the background to black and the color of our player cube to blue.

# Background Color

By default, the background will set to a Skybox on the Main Camera. Skyboxes are outside the scope of this series since we won’t be using a solid color instead.

Select the Main Camera and look under the Camera component for the Clear Flags property. Click the dropdown and select `Solid Color` and then click on the color rectangle for the Background property and set it to black.

Okay, I know this isn’t a very interesting background at the moment, but fear not because we will improve this later.

![background-color.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646962125838/uw-3LbJn7.gif)

# Creating Materials

In order to change the color of the Player cube, we need to introduce the concept of materials. We won’t go into detail about shaders here, but know that a material contains a reference to a shader that can define material properties like colors, which is what we want to change for the player.

Let’s create our first material now. First, right-click the Assets folder in your Project window, and then hover over Create, then click Material. Feel free to name this whatever you want, I’ll name it `Player__mat`.

With the new material selected, go over to the inspector window and click the white box next to the “Albedo” property under `Main Maps`. You should now see a color picker where we can select or input values to choose a color. I’m going to pick a shade of blue and then close the color picker.

We’ve selected a color, but the color is still not applied to the player. We’ve only modified the material, which is not yet being used. We need to assign this material to the player GameObject!

Select the player GameObject in the hierarchy window, and in the inspector look for the Mesh Renderer component. At the top of the component, you’ll see a `Materials` property (if it’s not expanded, click the triangle icon on the left side to expand the properties.

Now you can drag the material from the project window and drop it onto the Element 0 field. Another way to do this quickly, now that you understand how materials are referenced by the mesh renderer, is to drag and drop the material onto the object you want to assign it to in the scene window.

![drop-material.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646962277384/Zs3cHsWgz.gif)

# Player Script

For the rest of this article, we’re going to focus on creating our first script that will reset the player to the center of the scene when the game starts. I know, that’s not very exciting. However, it gives us the foundation to understand the basics of C# classes and how our scripts become components for GameObjects.

As we did with materials, let’s create a new folder called Scripts. Right-click on the Scripts folder, hover over Create, then click New C# Script. Make sure to change the name to Player (or any name you prefer) before pressing Enter to commit the name. Unity may take a second or so to compile the new script.

We have a script file created, but how is it going to know how to operate on the player GameObject in the hierarchy? Exactly, as of right now, it can't because there's no relationship between the two.

To add our script as a component of the player GameObject, you can drag it from the project window onto the Player GameObject in the hierarchy, or you can use the Add Component button in the inspector window.

![add-component.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646962894651/hesh3qx3W.gif)

## External Tools

Before we open the new script, let’s make sure that it will open in VS Code (or whatever code editor you prefer). Go to Edit and click Preferences in the Unity menu, then navigate to the `External Tools` section. You'll see a property called External Script Editor that you can use to set to the editor you want to use. When you're done, double-click the script file to open it.

![external-tools.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646962329810/ounEJtGJm.png)

# Script Walkthrough

Let’s step through each line of the C# file generated by Unity.

## Using Directive

The first 3 lines are using what’s called a using directive. Using directives allows us to use types from other namespaces without the need to use a fully qualified name. Basically, this allows us to write just type names instead of having to prefix them with their namespace.

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
```

The next line of code is on line 5 where we begin our definition of a class called Player, which matches our script name. You’ll also see that our Player class is related to something called a MonoBehavior. That colon tells C# that our Player class inherits from the MonoBehavior class built into Unity.

MonoBehavior is one of the most important aspects to understand at the moment because it is what allows our script to be part of the entity component system in Unity. Any class that inherits from MonoBehavior can be attached to any GameObject and gains the benefits of being part of the overall component model of Unity.

```csharp
public class Player : MonoBehaviour
{
    ...
}
```

The last lines to cover are the Start and Update methods. Methods are blocks of code that can be called by us or, in the case of Start and Update, by Unity itself as part of the component lifecycle. We'll wait to talk about the Update method in the next article. Let's focus on the Start method for now.

```csharp
// Start is called before the first frame update
void Start()
{

}
```

Every class that inherits from MonoBehavior has special methods that Unity will call at certain times in a component’s lifecycle. The Start method is called before the first frame update, which means it will be called before the first call to the Update method. This is a good method to use for caching resources or performing any work that needs to be done once for the setup of the component.

Method signatures are composed of an accessibility modifier, a return type, method name, and any parameters the method accepts. 

Accessibility modifiers indicate where the method can be accessed (private, public, protected, internal, etc.). If there’s no explicit modifier, then it is private by default. Therefore, our Start and Update methods are currently marked as private because we don’t want them to be accessed by other scripts.

We have yet to cover C# data types, but it’s important to know that methods require us to specify what it returns. You can check out the available built-in C# types [in the documentation](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types). Some examples are integers (whole numbers), float (decimal numbers), boolean (true or false values), and strings (text). The Start and Update methods use void as the return type, which indicates that these methods do not return a value.

We’ll talk about method parameters in future articles. That’s all we need to know right now to write our first lines of code to reset the player position.

# Reset Player Position

With a basic overview out of the way, let’s finally talk about how to manipulate GameObjects. To reset the player position, we need to understand how the position is set to start with.

The inspector makes it easy for us to access the Unity documentation for a particular component. Select the player once again and in the inspector you’ll see a question mark icon to the right of each component header; click it so we can read about Transform.

![Screen Shot 2022-03-10 at 8.32.59 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646962440232/xo8PxanAV.png)

We need to adjust the position, but how? How is the position represented? Click “Switch to Scripting” near the top of the page so we learn how to interact with transforms via script.

Scroll down to properties, and click on position. You’ll see that a position is represented via a Unity custom data structure called [Vector3](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/Vector3.html), which stores data for the x, y, and z components of a 3D vector along with some helpers for common use cases like right, left, up, down, etc.

![Screen Shot 2022-03-10 at 8.35.08 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646962532694/ZTPt1fQRU.png)

With that knowledge, the following code should make sense. We only need to reset the position once before the first frame update, so Start is a perfect place to do so.

```csharp
void Start()
{
    // Assign the current position to 0, 0, 0
    transform.position = new Vector3(0, 0, 0);
}
```

We can directly access the transform that we see in the inspector and thus access the position property. What about the `new` operator? What’s that for? Because Vector3 is a structure, we can’t simply set a property on it (like position.x = 3). We have to create a new structure with the properties we want to be set and then assign that value to the position property.

Remember we talked about Vector3 having some nice helpers. We can actually use one of those even in this simple case! Because we’re setting all three values to 0, we can use [Vector3.zero](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/Vector3-zero.html) which is identical to what we’ve done by writing `new Vector3(0, 0, 0)`.

```csharp
void Start()
{
    // Assign the current position to 0, 0, 0
    transform.position = Vector3.zero;
}
```

Notice we don’t have to use the `new` operator now because zero is a static property that creates the Vector3 and returns it to us.

Okay, I know that was a lot. Let’s test to make sure it works. In the scene view, use the move tool to shift it anywhere away from the center. Now click the play button in Unity and notice that once the game starts, the player is centered!

![center-position.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646963002535/F942L9RaQ.gif)


# Summary

There’s no easy way to introduce someone to programming, but I’ve done my best to provide an introduction that covers just what we need at the moment. We will be writing a lot of code throughout the series, and while doing so we will revisit and expand on every concept mentioned here.

If there are aspects that don’t make sense, that’s okay (and expected)! This will take time, don’t expect to understand every concept as it’s introduced. Give yourself some time and work through the rest of the series.

Take care.  
Stay awesome.
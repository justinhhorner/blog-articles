## An Overview of the Unity Editor

We’ve created our Unity project and now we’re staring at the Unity editor, which can be a daunting experience at first glance. Let’s take a tour around the editor interface and learn a bit about each window and how they relate to each other.

![overview-small.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646192224993/OyVLpllWA.png)

# Main Windows

## Scene

We’ll start with the Scene window because this is where you will spend a large portion of time. The scene is the interactive view into the world of your game, and the game’s user interface. In the next section, I’ll go over the different ways in which you can navigate the scene view.

![overview-scene.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646192846432/hMnwGknGG.png)

## Hierarchy

The hierarchy window is a representation of everything that makes up the Scene. The Hierarchy and the Scene windows are connected such that a GameObject selected in one view will display the select in the other. By the way, everything in these two windows is considered a GameObject, which we’ll get into more in a future article.

You can test this now by selecting one of the default GameObjects in the hierarchy. Click the Main camera, and in the Scene window, you’ll see the outline of the camera’s viewport. If you click the Directional Light, you’ll see the gizmo (that icon that looks like light shining down) selected in the Scene! As mentioned, you can also select these items in the Scene to select them in the hierarchy. Pretty neat!

![overview-hierarchy.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646192629383/VdHAxmXw5.png)

## Game

The game window is where the rendered output for the game is displayed from the camera’s point of view. We’ll use this window often since it is what we use to test our game in the editor during development. Short of building and running the game, this is the best representation of what the game will look and play like when the game is built to run on the target device.

![overview-game.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646192926535/eUOpcZldT.png)

## Inspector

The inspector window displays all of the components and configurations that are set on the GameObject you have selected in the Scene/Hierarchy. It’s the heart of all configurations for your GameObjects. For example, every GameObject by default has a [Transform](https://docs.unity3d.com/2021.2/Documentation/Manual/class-Transform.html) component that contains the position, scale, and rotation of the object. Select the Main Camera and view the inspector to see the Transform and Camera components along with their properties.


![overview-inspector.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193088324/tRmqKrD1I.png)

## Project

The project window is where all of our source files and assets live. It’s a representation of what is in our project folder, with some objects hidden (metafiles that Unity uses - we don’t need to modify these). Here is where you’ll find your sprites, images, audio, video, models, etc. You will also notice there's a packages folder that contains files for packages you download from the package manager. Our default project comes with quite a few already.

![overview-project.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193146140/D_Yw-asQ4.png)

## Console

The console window is where we will see output from our C# scripts. We can log messages to the console to output data for testing, assertions, or whatever purpose we deem necessary. This is also where you’ll see unhandled errors that can arise for many reasons: missing scripts, exceptions, compile errors, etc.

![overview-console.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193214506/jh9j8ULQD.png)

# Navigating the Scene

## Pan & Rotate

Panning in the Scene can be done by holding Option+Cmd and the left mouse button while moving the mouse. You can also use the hand tool in the UI, which is also accessible via the keyboard shortcut `q`.

![overview-pan.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646192179404/3Fgz7xGvU.gif)

You can rotate your view in the Scene by holding the right mouse button and moving the mouse around.

![overview-rotate.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193329918/Bw5rCmrrj.gif)

## Free Roam

While the right mouse button is held down, you can move closer or further away using W and S respectively. You can also move left to right with A and S. This is often referred to as FPS mode since it uses the common first-person shooter movement controls WASD. Scrolling the mouse wheel while in this mode will change the speed of movement.

![overview-fps.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193512819/-UypXveL4.gif)

## Zoom

You can zoom in and out of the Scene using the mouse wheel. This can also be done in Free Roam mode.

# Transforming GameObjects

Let’s manipulate a GameObject to get some practice using tools in the Scene and in the Inspector. We’ll be making changes to the GameObject’s Transform component, so select the Main Camera or Directional Light before moving forward.

## Position

Let’s first change the position of the selected GameObject. Most of the time large adjustments will be made from the Scene, where you can see exactly where the GameObject will be located. You can follow this up with minor changes in the Inspector view.

I’ll select the Main Camera from the hierarchy and then select the Move Tool (shortcut: w). You can see we have an interactive tool with arrows for X, Y, and Z that we can use to move the object around in the Scene.

![overview-position.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193612476/5alCSX4QL.gif)

Now over to the Inspector, you can see the values updating in real-time as you move the object around. Of course, you can also update these values manually and see the result in the Scene.

## Rotation

With the same GameObject selected, I’ll switch to the Rotate tool (shortcut: e). Just like when we changed the position, you can use the Scene by clicking the line axis that you want to rotate on or input the values manually in the Inspector.

![overview-rotate.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193718155/eN-G1J_Vs.gif)

## Scale

Finally, we have the Scale tool (shortcut: r). In the Scene, you can click and drag the box for the individual axis you want to scale on, or use the center box to scale on X, Y, and Z at the same time. You can manually change the scale properties in the Inspector as well. At the moment, we don't have a GameObject that displays scale in the scene, but you can see how an object would scale using the tool.

![overview-scale.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646193801754/_C4mEzrkB.gif)

# Summary

While there are many windows in Unity, this covers the basics that you will use most during the development of our game. I hope you found this overview helpful and are ready to move to the next article coming soon!

Take care.  
Stay awesome
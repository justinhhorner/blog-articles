## Implementing The HUD

In the last article, we went through the UI design process in Photoshop. Today we will implement that design in Unity.

We'll create a UI in Unity using the Canvas, Image, and TextMeshPro UI components. We'll make sure that the UI looks correct under several aspect ratios as well. If you're unfamiliar with TextMeshPro, read more about it [here](https://docs.unity3d.com/Packages/com.unity.textmeshpro@3.0/manual/index.html).

As a reminder, here's our final design (including the guides).

![UI Final PS](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921718293/U7vZwS8Xa.png)

# UI Parent Setup
Let's start with creating the UI components we need. I'll create a new parent GameObject named `UI` where the rest of our UI child components will live. I'll also add a UI Manager script to update the UI later as well (we'll talk about the UI Manager in the next post).

Now let's add a Canvas via Right Click on the UI GameObject and selecting UI -> Canvas. The canvas will act as a host for our other components. Before we add those, let's set a few important settings on the Canvas.

# Canvas Scaler
Unity takes care of a lot of issues we no longer have to be concerned about, thanks to the [Canvas Scaler](https://docs.unity3d.com/2020.3/Documentation/Manual/script-CanvasScaler.html). This component is responsible for controlling the scale and pixel density of child UI elements, which includes font sizes and image borders. We definitely want this! Doing this work manually is tedious and time-consuming.

By default, the scale mode will be set to Constant Pixel Size, which means nothing on the canvas will scale with screen size. I'll switch to the Scale With Screen Size mode, which will make UI elements larger for larger screen sizes. I'll set the reference resolution to 1920x1080 and let the other settings to their defaults.

Now, we can finally begin adding the UI elements.

# Lives Images
First I'll add ad new Lives parent GameObject anchored to the top left of the screen, and then add a child image to represent a player's life. In the Image component, I'll check `Preserve Aspect` and click the `Set Native Size` button, and then resize manually to taste. I'll then duplicate this image two times so we can represent three lives total for our player.
![screenshot-production-adding-ui-lives.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921539420/Tz0o30THN.png)

# Fuel Bar
Next, I'll add a Boost parent GameObject, also anchored to the top left, and then add two images and follow the same routine as I did for the lives image. The fuel itself I'll place behind the container and change the `Image Type` to Filled and set `Fill Method` to Vertical. We will later programmatically adjust this value when the player is using the speed boost pickup.

![UI fuel](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921560038/JoHWALMsU.png)

# Shields
Following suit, I'll create the parent Shields GameObject first, then add an Image and TextMeshPro component. I'm using a custom font (you can create TextMeshPro font assets via Window -> TextMeshPro -> Font Asset Creator). TextMeshPro components contain many settings. I won't waste your time going through all of them, but you can see the result of my tweaks.
![UI shields](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921589087/u5RpeGfQw.png)

# Stars
I won't waste time explaining the stars setup, since it is practically identical of what we did for shields. Duplicate that and update the image and change the default text to `00/00`. I've got the parent anchored to the top right.

![UI stars](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921280972/OX3PoPFrO.png)

# Message Panel
After creating a panel parent object and anchoring it to the bottom, I'll add an image to be the background of the message and a TextMeshPro component that's centered for the text. I tweaked the settings for the look I want, and here's the result.

![UI message](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921655470/lgKDRAOJR.png)

# Summary
Our new UI is now in place, and soon we'll be updating it programmatically!

![UI final](https://cdn.hashnode.com/res/hashnode/image/upload/v1648921685626/HGXeeKeVE.png)

Take care.  
Stay awesome.
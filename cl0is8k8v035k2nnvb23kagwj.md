## Custom Layouts in Unity

We've covered the basics of the Unity editor in the last article, now I want to share a custom layout that I've been using for years. Practically every view in Unity can be dragged and rearranged or dragged out to create a new window. I created this custom layout because I find that it's the most productive for my workflow, but this is entirely optional.

# Rearranging Windows
You can always find available windows via the Window menu, with the "General" section containing the mainstays. When I reference opening a Window, this is the menu I'm referring to. You can build your own custom layout by clicking and dragging window handles practically anywhere you want, and then save your layout; even as an external file, you can back up if you'd like.

# My Custom Layout
The following screenshot identifies four groups of windows and the inspector to the far right. Let's go into detail on how I made this layout. If you're new to Unity, this is an excellent opportunity to get comfortable moving windows around and forming the layout.

![screenshot-unity-layout-groups.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646197098469/BeI8Lf1kn.png)

# Group 1
You should already have the Scene window visible from the default layout, so open the "Animator" window and drag it beside the Scene tab to dock them together.
I prefer this because it can be helpful to have a lot of space for both the Scene and Animator. I rarely need anything else to take up this much space.

![gif-unity-layout-group1.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646197275828/37Xb5KfAa.gif)

# Group 2
The focus of this group is to visualize and test the game using the Game window. The other windows I've placed in this group are "Animation" and "Audio Mixer."
This setup has worked well for me because the Game window is just below the Scene window, and Animation and Audio Mixer are close by without needing to take up a lot of vertical space.

![gif-unity-layout-group2.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646197286271/HyAoqFfz8.gif)

# Group 3
This group has proved to be a significant productivity boost from the default layout.
First, get the Project and Hierarchy windows together side-by-side, like this:

![gif-unity-layout-group3.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646197303742/iez7yjVuH.gif)

By default, the Project window will be in a two-column layout, which takes up too much space for my liking. Click the small ellipsis button near the lock icon in the tab well and then select "One Column Layout."

Ah, much better.

# Group 4
The final group of windows is the Console and Test Runner. The Console window provides logs, warnings, and errors that will be helpful during the development of your games. You can write logs directly to this window programmatically to reveal the game state or practically anything else you find valuable.

The Test Runner gets us into the topic of automated tests. Once we have written tests, the test runner window is what we use to run them and see what passed and failed.

![gif-unity-layout-group4.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1646197364349/jlpbAcU9q.gif)

# Inspector
Finally, we have the all mighty inspector window to the far right. I leave quite a bit of space for this window because it displays dynamic user interfaces based on what's selected in the Project and Hierarchy windows.

# Saving Layouts
We made it to the end of creating a custom layout. Now let's save it so we can recall it later. Go to the Window menu item once more, then hover over "Layouts" and click "Save Layout". Give it a name, and click "Save."

You can also access layouts quickly by using the dropdown on the top right side of the editor that has the current layout name selected. If you'd like to save your layout as a file to back up yourself or share with others, choose "Save Layout to File," and you'll be prompted with a save dialog to choose where you want to save it.

# Summary
You now have a custom layout that you can modify as you work more with Unity and gather your own preferences based on your workflow!

Take care.  
Stay awesome.

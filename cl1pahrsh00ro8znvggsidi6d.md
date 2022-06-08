## Adding New Enemy Art

In this article, we're going to change the enemy from a cube to a sprite! We've done this several times already, so this will be another short post to show the progress of our game transitioning from 3D to 2D.

Let's get started.

## New Enemy Art
We're going to follow the same steps as before to switch to 2D. I'll replace the 3D components with a trigger `CapsuleCollider2D`, and a `Rigidbody2D`. Here are the components we have for the enemy prefab after making these changes.

![enemy inspector window](https://cdn.hashnode.com/res/hashnode/image/upload/v1648918830602/91VG651pb.png)

I'll also update the enemy script to use `OnTriggerEnter2D`.

Here's the result.
![enemy art demo](https://cdn.hashnode.com/res/hashnode/image/upload/v1648918853187/zmYdMYvAg.gif)

## Summary
That's all we need to switch out for our enemy. Stay tuned.

Take care.  
Stay awesome.
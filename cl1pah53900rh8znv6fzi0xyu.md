## Adding Art for the Projectile

I have a very short article for today. Our player art looks great, but not paired with that ugly capsule projectile. In this article, we'll update the projectile art in much the same way we did when upgrading the player art.

Let's get started.

# New Projectile Art
As we did when updating the player art, we will drag and drop the sprite we want to use for the projectile into the hierarchy and start to start with a new GameObject. I'll add a `Rigidbody2D`, a `CapsuleCollider2D` trigger, and the `Projectile` components.

![projectile art inspector](https://cdn.hashnode.com/res/hashnode/image/upload/v1648918188204/7XO33oqT1.png)

We may want to change the art later, which is as easy as updating the Sprite property in the inspector for the SpriteRenderer.

With this GameObject set, we can now delete the original Projectile prefab and create a new one to assign to our player script via the editor.

Here's the result.
![gif-production-projectile-art.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648918317564/HW32gsIXh.gif)

# Summary
We now have a 2D sprite for our projectile, which pairs very well with the new player art. Stay tuned.

Take care.  
Stay awesome.
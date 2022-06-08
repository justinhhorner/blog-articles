## Adding Art for the Player

We've made our exciting first change toward the look of our game by switching the background from a solid color to beautiful, hand-drawn art. In this article, we're going to change from a cube to a sprite for our player!

(Oh, by the way, I changed the background art to one I like a bit better)

## New Player Art
The quickest way for us to switch to a 2D sprite for the player, in this case, is drag-and-drop the art we want to use for the player into the hierarchy. This will create a new GameObject with a `SpriteRenderer` already configured correctly.

Since we would need to remove the `Rigidbody` and `Collider` components and add the 2D equivalents, this gives us a fresh start to add what we need.

Here you can see I've done just that.
![player art inspector](https://cdn.hashnode.com/res/hashnode/image/upload/v1648916614736/LJy9DIPA5.png)

Now let's add the `Rigidbody2D`, `CapsuleCollider2D` and `Player` components.
![player art inspector with all components](https://cdn.hashnode.com/res/hashnode/image/upload/v1648916637262/JY2kJlwb8.png)

Now let's see how it looks. I think we're in for a big surprise.
![large player](https://cdn.hashnode.com/res/hashnode/image/upload/v1648916663992/iGGv-Pqh7.gif)

Yeah, our player ship is gigantic. There are several ways to resolve this. For now, I'm going to scale the image down in the transform of the inspector.
![player art inspector resize](https://cdn.hashnode.com/res/hashnode/image/upload/v1648916684007/U6detOst5M.png)

That's better.
![normal size player](https://cdn.hashnode.com/res/hashnode/image/upload/v1648916704692/pN-OVpOYK.gif)

## Summary
Our hand-drawn look is coming to life! As you'll see throughout the rest of the series, I'm going for a Yoshi's Island look and feel for the game.

Take care.  
Stay awesome.

## Trigger and Collision Methods in Unity

It's time to take a short break from the main game for a bit of a side-quest.

I've talked about using colliders with triggers when I wrote about enemy collision. In this article, I want to briefly talk about the different method signatures for triggers and collisions.

## Collision Methods
To be notified of a non-trigger collision between two GameObjects, we use the [OnCollisionEnter](https://docs.unity3d.com/ScriptReference/Collider.OnCollisionEnter.html) method. This means that we want the physics to simulate two objects hitting each other without pass through. The full signature is:

```csharp
private void OnCollisionEnter(Collision collision)
```

One important differentiation in this signature compared to trigger methods, other than the name, is the type of the argument that is passed by Unity. We are given an argument of type [Collision](https://docs.unity3d.com/ScriptReference/Collision.html) instead of Collider.

The Collision type provides additional information like the contact points that initiated the collision and the impact velocity. You could imagine ways to use this data, like determining what sound to play based on impact, or taking some action for every contact point.

The 2D equivalent of this method is [OnCollisionEnter2D](https://docs.unity3d.com/ScriptReference/Collider2D.OnCollisionEnter2D.html).

## Trigger Methods
If you want to be notified when two GameObject's colliders pass through each other, use the OnTriggerEnter method. An example of using a trigger would be if you want the player to pick up an item, which would allow the player to pass through the item instead of knocking it away with a physics collision.

The full signature is:

```csharp
private void OnTriggerEnter(Collider other)
```

In this case, Unity provides an argument of type [Collider](https://docs.unity3d.com/ScriptReference/Collider.html), which we can use to discover more information about the other GameObject that caused the trigger method to be invoked.

We've already used this to detect what passes through our Enemy prefab. In our prototype, we're comparing the `other` collider tag to see if it's the Player or a Projectile to know what to do.

The 2D equivalent of this method is [OnCollisionEnter2D](https://docs.unity3d.com/ScriptReference/Collider2D.OnTriggerEnter2D.html).

## Summary
If you ever run into a situation where your collision/trigger methods are not being called, always reference the [Collision Action Matrix](https://docs.unity3d.com/Manual/CollidersOverview.html). Most likely, you're GameObjects are not configured in such a way that Unity will invoke the method.

![Collision Matrix Documentation](https://cdn.hashnode.com/res/hashnode/image/upload/v1648434228809/zDtHyiOqu.png)

Be mindful of what physics components you have on the GameObjects you want to detect collision for. The matrix has come in handy for me several times over the years.

Take care.  
Stay awesome.
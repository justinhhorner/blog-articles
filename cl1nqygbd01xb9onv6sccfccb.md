## Creating Enemy Behavior and Collision

Floating around on the screen without an enemy to shoot isn't going to be fun for long (in fact, I'm already over it: 1/10). We're going to fix that in this article by creating our first enemy and giving it some basic behavior.

We'll also introduce collision detection using Unity's physics components so that our projectile will destroy the enemy. A good place to begin is a quick overview of said components, and then we'll apply them to our GameObjects.

For the enemy, I'll create another cube and material with a red color. I'll place it above the player cube and scale it down to about 0.7. We'll need to add behavior as well, so I'll create an Enemy script in the `Scripts` folder.

Let's talk about colliders.

## Collider Components

Collider components provide GameObjects with a defined shape for physical collisions. They are invisible to the player and do not need to match the exact shape of a GameObject's mesh. The more detailed and precise the collider is, based on the mesh, the more processor-intensive they become.

The least processor-intensive colliders are primitive collider types, like [Box Collider](https://docs.unity3d.com/Manual/class-BoxCollider.html). Sphere Collider, Capsule Collider for 3D and their 2D equivalents like Box Collider 2D and Circle Collider 2D.

There's a lot more to know about colliders, but we need to move on to triggers for our purposes.

##Triggers

We don't want our projectile and enemy GameObjects to cause a hard collision that blocks their paths. We want them to be able to pass through each other, and when they do, notify us so we can respond.

Indicating that a collider is a trigger will do just that; it will use the physics system in Unity to simply detect when one collider enters the space of another without creating a collision. Perfect!

Setting a collider as a trigger is done via the `Trigger` property in the inspector.

![screenshot-is-trigger-collider-inspector.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648431486213/vj27YzYGr.png)

The next physics component we need to discuss is the Rigidbody.

## Rigidbody

The [Rigidbody](https://docs.unity3d.com/ScriptReference/Rigidbody.html) component puts the attached GameObject's motion under control of the Unity physics engine. Simply adding a Rigidbody or Rigidbody2D to a component will cause it to be pulled by gravity and cause it to react to collisions with other GameObject's that have a collider.

## Enemy Projectile Trigger

Let's put the theory to practice. Since our projectile is using a capsule primitive, it was created with a Capsule Collider already attached. All we need to do is check the `Trigger` property.

I'll add a Rigidbody component to the projectile prefab. We don't want gravity to be applied to our projectiles, so uncheck "Use Gravity" in the inspector.

The enemy is a cube primitive, so it already has a Box Collider component. Still, we need to make sure it is set as a Trigger collider for the Capsule Collider on our Projectile prefab.

## On Trigger Enter

Unity will invoke a method called [OnTriggerEnter](https://docs.unity3d.com/ScriptReference/Collider.OnTriggerEnter.html), providing an argument of type Collider that will give you information about what collided with our GameObject. 

There's a helpful [collision action matrix](https://docs.unity3d.com/Manual/CollidersOverview.html) at the bottom of the colliders overview to help you know under what scenarios Unity will invoke collision methods.

For us to detect what collided with the enemy, we can use tags in Unity. I'll create a new tag, `Projectile,` and assign it to the Projectile prefab. There should already be a `Player` tag provided by Unity, and I'll assign that to our Player GameObject.

Now, here's our OnTriggerEnter method in the Enemy script.

```csharp
void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("Player"))
    {
        // TODO: Damage the player
    }

    if (other.CompareTag("Projectile"))
    {
        Destroy(other.gameObject);
    }

    Destroy(gameObject);
}
```

And here's the result!

![Enemy Collision](https://cdn.hashnode.com/res/hashnode/image/upload/v1648432028814/ifJthHVVR.gif)

## Summary

With our new collision detection knowledge, we now destroy the enemy when it collides with a projectile or our player. Later, we'll come back to implement player lives and damage.


Take care.  
Stay awesome.
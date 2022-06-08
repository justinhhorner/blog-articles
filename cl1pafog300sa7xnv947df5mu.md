## Adding a Shield Pickup

We have a speed boost powerup created in the last article, and I think our player would also benefit from a shield powerup. In this article, we'll create a new shield powerup prefab, based on the work we've already done for the speed boost.

Let's get started.

# The Prefab
We'll need a way to represent this new type, so I'll add it to the `CollectableType` enumeration.

```csharp
public enum CollectableType
{
    Boost,
    Shield,
}
```

I'll duplicate the powerup prefab and update the type to `Shield`. For now, I'll leave the effect duration as is.

# Absorbing Damage
We now need to decide how the shield will work for our prototype. I want a way for designers (well, just myself for this project) to be able to quickly and easily update the shield strength.

In the player script, I'll add a new Serialize Field called `shieldsRemaining`, which will be initialized to 0 by default.
```csharp
public class Player : MonoBehaviour
{
    ...

    private int lives = 3;
    private int shieldsRemaining = 0;

    ...
}
```

Because the shield powerup is tagged as `Collectable`, we don't need to do anything inside of the `OnTriggerEnter` method. We can make our changes inside of `ActivateCollectable` instead. Here we will add a switch section to account for the shield, where we will assign a constant shield strength value to our `shieldsRemaining` field.

```csharp
private void ActivateCollectable(Collectable collectable)
{
    Destroy(collectable.gameObject);

    switch (collectable.Type)
    {
        case CollectableType.Boost:
            speed *= Constants.Collectable.BoostMultiplier;
            StartCoroutine(CollectablePowerdownRoutine(collectable.Duration, UndoBoost));
            break;
        case CollectableType.Shield:
            shieldsRemaining = Constants.Collectable.ShieldStrength;
            break;
        default:
            break;
    }
}
```

I have that constant currently set to 3.
```csharp
public static class Collectable
{
    public static int ShieldStrength = 3;
    public static float BoostMultiplier = 2;
}
```

Here's the result. After picking up the shield powerup, it now takes 6 hits before our player is destroyed.
![shield demonstration](https://justinhhornerdotcom.files.wordpress.com/2021/06/gif-prototype-shield-powerup-1.gif)

# Summary
I believe that's all the powerups we need for now. If we have another idea for one, it will be quick and easy to add it with this small system in place. If our needs require a bit more complexity, we can expand what we have to meet that need. 

Keep your systems as simple as possible until you absolutely need to add more abstraction and complexity.


Take care.  
Stay awesome.
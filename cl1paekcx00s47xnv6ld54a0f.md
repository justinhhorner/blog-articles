## Add a Speed Boost Pickup

In the last post, we added a small collectible system that will allow us to quickly prototype some ideas. 

In this article, we'll create a collectible prefab that will change the player's movement speed for a short duration, and then reset back to the initial speed.

# The Prefab
I'll base the Boost Powerup on our Collectable prefab by duplicating it and renaming it to `Boost Prefab`. Now, I want to set the Collectable Type of this prefab to Boost, which we currently don't have. Let's update the enums from our last post.

```csharp
public enum CollectableType
{
    Boost,
}
```

Now I'll set the type property in the inspector.

![screenshot-prototype-boost-type-inspector.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648781159979/NLFXeAe6W.png)

# Speed Boost
Inside the Player script, I'll check against the collectible type and implement a speed boost. I'll create a separate private method that will activate all future collectibles to isolate the behavior from `OnTriggerEnter`, as a personal preference to keep the message method clean and simple.

I made sure that the prefab had a tag set to `Collectable` to identify it. I prefer to create constant strings, so you'll notice the use of my static Constants.cs class to access `Tag.Collectable`, which simply holds the string value of the tag name "Collectable".

```csharp
private void OnTriggerEnter(Collider other)
{
    if (other.CompareTag(Constants.Tag.Collectable))
    {
        ActivateCollectable(other.GetComponent<Collectable>());
    }
}
```

The `ActivateCollectable` method takes the collectible object that the player collided with and applies the effects to the player. For now, we just have a boost, which increases the speed by value from the constants file `Collectable.BoostAmount`.

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
        default:
            break;
    }
}
```

# Power Down
This accomplishes the goal to boost speed, but we also need a way to undo or power down the effect. To do this, I'll pass an anonymous method for the coroutine to execute once the wait time has elapsed.

First, we need to add a duration for the effect. I'll do that by adding a field and public get accessor to Collectable.cs. If you're unfamiliar with the read-only property syntax, see [expression-bodied members](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/expression-bodied-members).

```csharp
public class Collectable : MonoBehaviour
{
    [SerializeField] private float speed = 5;
    [SerializeField] private float duration = 5;
    [SerializeField] private CollectableType type;

    public float Duration => duration;
    public CollectableType Type => type;

    ...
}
```

Now I'll add the coroutine to power down the effects based on this duration.

```csharp
private IEnumerator CollectablePowerdownRoutine(float duration, Action resetDelegate)
{
    yield return new WaitForSeconds(duration);
    resetDelegate?.Invoke();
}
```

Here's the result
![gif-prototype-boost-demo.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648781245226/mVlOOxDBb.gif)

# Summary
We now have a boost powerup the player can collect with a duration that can be easily set by designers.

Take care.  
Stay awesome.
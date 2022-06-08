## Preparing For Collectible Items

You thought we were going to make a game without collectibles, didn't you? Oh no, there will be collectibles, and in this article, we're going to implement the groundwork so that as soon as ideas arise, we can quickly implement them to playtest.

We'll create a simple collectible system where the player can cause a trigger collision and identify what type of collectible caused the trigger. For now, we'll simply log the type to the console.

## Collectible Prefab
Let's create the prefab first. I'll create a new Sphere and create a new Material to add some color. I'll also create a new tag called `Collectible` and assign it to the GameObject, then make sure the collider is set to be a trigger, finally drag and drop it to the Prefabs folder to create a new prefab.

![screenshot-prototype-collectible-prefab.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648778168493/B9zLDtBL9.png)

Next, I'll create a new script called "Collectible" and add it to the scripts folder. Inside the script, I'll add movement just like we did in the enemy script. I'll add a variable speed and destroy the collectible when it goes off-screen.

```csharp
using UnityEngine;

public class Collectible : MonoBehaviour
{
    [SerializeField] float speed = 5.0f;

    void Update()
    {
        transform.Translate(speed * Time.deltaTime * Vector3.down);
    }
}
```

## Collectible Type
On to the more interesting bit, let's create a way to make each collectible distinguishable. Again, I'm going to do this in a way that's fast for us to prototype ideas.

For now, I'll identify collectibles by assigning an enum value. I'll create a separate file in the `Scripts` folder named `CollectibleType` and add some placeholder types we can change later.

```csharp
public enum CollectibleType
{
    TypeA,
    TypeB,
    TypeC
}
```

Back in our collectible script, I'll add a private field for `CollectibleType` named `type` with the `SerializeField` attribute. Switching back to Unity, we can see that now we can easily select what type of collectible we want an instance to represent.

![gif-prototype-pu-type.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648778517611/A_ZDLFlDA.gif)

We will need to access this value from the Player script, so let's make a get accessor.

```csharp
public class collectible : MonoBehaviour
{
    [SerializeField] float speed = 5.0f;
    [SerializeField] CollectibleType type;

    public CollectibleType Type { get { return type; } private set; }

    void Update()
    {
        transform.Translate(speed * Time.deltaTime * Vector3.down);
    }
}
```

To make it easy to apply collectables to the player, I'll add a `Rigidbody` component (no gravity), then inside the Player script add an `OnTriggerEnter` method. Now, when the `Player` collides with a Collectable, we will log the type of Collectable to the console.

Here's the updated `Player` script:

```csharp
public class Player : MonoBehaviour
{
    ...
    
    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("collectible"))
        {
            var collectible = other.GetComponent<collectible>();
            Destroy(other.gameObject);
            Debug.Log(collectible.Type);
        }
    }
}
```

![gif-prototype-collectable-log.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648778912354/y0fcFTMD-.gif)

## Summary
Now we have a way to quickly set up new types of collectibles during the prototype phase. This can certainly be improved later, but it will serve us well for quick iteration during playtesting.

Take care.  
Stay awesome.
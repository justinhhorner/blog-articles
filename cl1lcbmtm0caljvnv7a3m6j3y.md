## Creating a Spawn Point

We now have the player shooting a projectile, but something about the feel of the mechanic isn't quite right to me. Did you come to the same conclusion? If so, what do you think is causing it?

For me, there's too much time between pressing the `Space` key and the time I first see the projectile on screen. That's because we are instantiating the projectile prefabs from the center of the player cube when we use `transform.position`.

In this article, we're going to create a spawn point for the projectile that, once we've implemented it, we can move around in the scene while playtesting to find the perfect position to spawn projectiles.

## Nested Game Objects
In order to understand how this will work, you need to know about nesting game objects. We need a new GameObject in the scene that we can use as the starting position, and as the player moves, we want this transform to move with the player so we can guarantee it will also be in the same position relative to the player GameObject.

Child game objects do just that! If we create the spawn point as a child of the player GameObject, it will always move relative to the player. To create an empty GameObject, right-click on the player in the hierarchy and then select "Create Empty". Rename it to "Projectile Spawn".

All we need is the transform, so no need to add any additional components. We want an easy way to see where the center of the transform is. Unity has a feature called icons that we can use for this purpose.

With the spawn GameObject selected in the hierarchy, go to the inspector and click on the top left cube icon. That will open a new window where you can select the icon you want to use. I'm going to choose this one.

![Spawn Point Icon](https://cdn.hashnode.com/res/hashnode/image/upload/v1648402078886/FZkD-9jwc.png)

You may not be able to see it in the scene window because the spawn child object was created at the center of the parent player. Select the spawn object and use the move tool to pull the spawn point upward until you can see the circle icon you chose.

![gif-spawn-pull.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648402111306/Njgeg_05k.gif)
 
Once we're done, we will be able to change the position of spawned projectiles simply by moving this GameObject in the scene without changing any of our code!

## Referencing GameObjects in the Edtior
In order to use the position of the spawn transform, the player script will need to get access to it. There are several ways to achieve this, but I'm going to take this opportunity to show you how to drag and drop to create references from the Unity Editor.

First, we need a variable to store the transform, then we need to pass its position vector to the `Instantiate` call. Let's take care of that now. I'll omit code in the script that's not relevant.

```csharp
public class Player : MonoBehaviour
{
    ...
    [SerializeField] private Transform projectileSpawnPoint;
    ...
    
    private void RespondToFire()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Instantiate(projectilePrefab, projectileSpawnPoint.position, Quaternion.identity);
        }
    }
}
```

That's it for code changes. Now, how exactly are we going to set that variable to the spawn GameObject? Let's head back to Unity and let it compile. Once it's complete, select the player and look at the inspector to find our new Projectile Spawn Point property.

![Spawn Point Null](https://cdn.hashnode.com/res/hashnode/image/upload/v1648402143714/ziyc3pBMg.png)

Now, drag and drop the Projectile prefab from the Project window to the inspector where it says None (Transform). This has exactly the same result as using the small asset selector button in the right side of the field (the way we assigned the projectile in the last article).

Now that the reference has been made, you can playtest and find a position that you like. I decided on 0.9 on the Y-axis.

![Spawn Point Shooting](https://cdn.hashnode.com/res/hashnode/image/upload/v1648402171413/8XM-uScwY.gif)

## Code Only Solution
If you would rather accomplish this with code only, you can create an offset vector that you can add to the current player position during instantiation. When the two vectors are added, each respective element from the vector is operated on. 

For example, if you create an offset vector of X=0, Y=-2, Z=0, then when the sum of the two vectors will result in the current player position minus 2 on the Y-axis.

## Summary
We now have a projectile spawn point that anyone on our team can modify without the need to call us to do tedious position changes over and over again. Quickly find what feels good to you, set it, and forget it!

Take care.  
Stay awesome.
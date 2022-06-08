## Adding Shield Art

In the last article, we updated the enemy from a capsule to sprite art. In this article, we'll add art for our shield powerup.

# Add SpriteRenderer
I'll add a child GameObject to the Player called Shield and add a SpriteRenderer component with the new shield sprite.

![player shield inspector](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919321364/GvLIfU-_y.png)

Since we need to activate and deactivate the shield GameObject, I'll reference it in the Player script where we are handling powerup activation. Then, I'll assign the shield GameObject in the inspector.

```csharp
public class Player : MonoBehaviour
{
    ...

    [SerializeField] private GameObject shieldPrefab;

    ...
}
```

In a previous post, we added the `shieldsRemaining` variable which we can reuse here to know whether or not the shield should be active. I'll create a new method called `HandleShieldDisplay` that we'll call from the `Update` method.

```csharp
private void HandleShieldDisplay()
{
    if (shieldsRemaining > 0 && !shieldPrefab.activeSelf)
    {
        shieldPrefab.SetActive(true);
    }
}
```

```csharp
private void Update()
{
    RespondToMovement();
    RespondToAttack();
    HandleShieldDisplay();
}
```

In the `ProtectedByShield` method, we'll call `SetActive(false)` if we no longer have shields remaining.

```csharp
private bool ProtectedByShield()
{
    if (shieldsRemaining > 0)
    {
        shieldsRemaining--;
        return true;
    }
    else
    {
        shieldPrefab.SetActive(false);
    }

    return false;
}
```

Here's the result.
![screenshot-production-shield-art.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919405586/9J_8dmKlS.png)

# Summary
We're done! We'll add more polish to the shield later, but for now, it's functional and we can finally visualize the shield when the powerup is activated.

Take care.  
Stay awesome.
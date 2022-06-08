## Creating a Shooting Projectile

Alright, I know you've all been waiting to add shooting projectiles to the game. Well, the wait is over because that's what we're going to do in this article. We've got a lot to cover to get a simple projectile to shoot from the player to the top of the screen, so let's get started.

## Creating The Projectile
For the prototype, let's use a simple 3D capsule to represent the Projectile.

As we did for the player cube, right-click in the hierarchy, and go to 3D Object -> Capsule. Rename the GameObject to Projectile and change the scale to 0.2 for X, Y and Z. Move the player cube down and out of the way, then center the capsule.

I'm going to give this capsule a blue color by creating a material in the Materials folder, and naming it "Projectile_mat". I'll give the new material an albedo color of `#67F3F3` and set it on the Mesh Renderer of the Projectile.

![screenshot-capsule-projectile-scene.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648361166980/NMbdqHRlv.png)

### Prefabs
To instantiate new projectiles at runtime, we need to make a [Prefab](https://docs.unity3d.com/Manual/Prefabs.html) from our Projectile GameObject. Create a new Prefabs folder, then drag-and-drop the Projectile GameObject into the folder to create a Prefab. Prefabs are indicated by a blue cube in the project and hierarchy windows.

![screenshot-player-attack-prefab.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648361252303/BKCYwhDhn.png)

## Instantiating Projectiles
As the Player, we need to know:
- What GameObject we should instantiate
- Under what condition we should instantiate it
- Where it should be positioned upon instantiation

Let's tackle these one at a time.

Firstly, we need to make the Player script aware of the existence of a projectile prefab. To do this, I'll create a private GameObject variable that will hold a reference to the prefab. I'll add a SerializeField attribute so we can assign it from the inspector.

```csharp
[SerializeField] private GameObject projectilePrefab;
```

Now back in Unity, wait for the compilation to complete, and then click the target button beside the "Projectile Prefab" field in the inspector and select our Projectile Prefab. Now that the reference has been made, the Player script will have a value set for this field at runtime. You could optionally add a conditional in the Player Start method to check for null, but I won't be bothered to do that everywhere for our prototype.

Back in the Player script, I'm going to add a conditional statement for the [Input.GetKeyDown](https://docs.unity3d.com/2021.1/Documentation/ScriptReference/Input.GetKeyDown.html) method and provide [KeyCode.Space](https://docs.unity3d.com/ScriptReference/KeyCode.html) as an argument to see if the space key is down during the current frame.

```csharp
void Update()
{
    RespondToMovement();

    if (Input.GetKeyDown(KeyCode.Space))
    {
        //TODO: Instantiate projectile
    }
}
```

Here's where we will invoke the Instantiate method to create a new prefab instance. We'll provide the following arguments:

- The object to instantiate ([Object](https://docs.unity3d.com/ScriptReference/Object.html))
- The initial position ([Transform](https://docs.unity3d.com/ScriptReference/Transform.html))
- The rotation ([Quaternion](https://docs.unity3d.com/ScriptReference/Quaternion.html))

```csharp
void Update()
{
    RespondToMovement();

    if (Input.GetKeyDown(KeyCode.Space))
    {
        Instantiate(projectilePrefab, transform.position, Quaternion.identity);
    }
}
```

Let's head back to Unity and test it out!

![gif-player-attack-static-projectiles.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648361672423/mGD3h6HHB.gif)

Technically, everything is working, which is excellent! However, our projectiles don't move once they've been instantiated.

# Adding Movement
Let's add behavior to the Projectile prefab. I'll create a new Projectile script in our Scripts folder and add a speed field with the SerializeAttribute and initialize it to 8.0f.

Next, I'll add the following code so that the Projectile translates upward when they are instantiated.

```csharp
void Update()
{
    transform.Translate(speed * Time.deltaTime * Vector3.up);
}
```

Now, if we playtest back in Unity, you'll see that we have shooting projectiles!

![gif-player-attack-shooting-projectiles.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648361831097/IYl9FruGW.gif)

Great, but what happens once the projectiles move off-screen? If you look in the hierarchy window, you'll see that every projectile prefab instance created stays alive and continues to move upward to infinity.

Yikes! That's certainly going to waste memory and hinder our performance if this continues to happen while playing the game. 

## Destroying Off-Screen Projectiles
Inside our Projectile `Update` method, we need to check to see if the projectile is off-screen, and destroy it as soon as we can.

Below the `transform.Translate` line, I'll add a condition to check for the `y` position, and if it is greater than or equal to 7.25, I'll invoke the [Destroy](https://docs.unity3d.com/ScriptReference/Object.Destroy.html) method providing the projectile instance `gameObject` as the argument.

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Projectile : MonoBehaviour
{

    [SerializeField] float speed = 8.0f;
    [SerializeField] float boundaryYMax = 7.25f;

    // Update is called once per frame
    void Update()
    {
        transform.Translate(speed * Time.deltaTime * Vector3.up);

        if (transform.position.y >= boundaryYMax)
        {
            Destroy(gameObject);
        }
    }
}

```

As we did with the movement logic, we can create a new method to isolate the projectile code. I'll create a new method called `RespondToFire` and call it in the `Update` method.

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
    [SerializeField] private float speed = 5.0f;
    [SerializeField] private float boundaryYMin = -3.50f;
    [SerializeField] private float boundaryYMax = 0f;
    [SerializeField] private float boundaryXMin = -8.7f;
    [SerializeField] private float boundaryXMax = 8.7f;
    [SerializeField] private GameObject projectilePrefab;
    [SerializeField] private Transform projectileSpawnPoint;

    // Start is called before the first frame update
    void Start()
    {
        // Assign the current position to 0, 0, 0
        transform.position = Vector3.zero;
    }

    // Update is called once per frame
    void Update()
    {
        RespondToMovement();
        RespondToFire();
    }

    private void RespondToFire()
    {
        if (Input.GetKeyDown(KeyCode.Space))
        {
            Instantiate(projectilePrefab, projectileSpawnPoint.position, Quaternion.identity);
        }
    }

    private void RespondToMovement()
    {
        float horizontalInput = Input.GetAxis("Horizontal");
        float verticalInput = Input.GetAxis("Vertical");
        Vector3 direction = new Vector3(horizontalInput, verticalInput);

        transform.Translate(speed * Time.deltaTime * direction);

        direction.x = Mathf.Clamp(transform.position.x, boundaryXMin, boundaryXMax);
        direction.y = Mathf.Clamp(transform.position.y, boundaryYMin, boundaryYMax);
        transform.position = direction;
    }
}

```

Head back to Unity and play the game. Shoot a few projectiles and notice that the projectile clones are removed from the hierarchy as they travel off-screen.

![gif-player-attack-destroy-projectiles.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648362246908/9DVtwtJhj.gif)

# Summary
You accomplished quite a bit in this article. Now our player can shoot projectiles and we're ensuring they don't travel on for eternity while our game is playing. Stay tuned.

Take care.  
Stay awesome.
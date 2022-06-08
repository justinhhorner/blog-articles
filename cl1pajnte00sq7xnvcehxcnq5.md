## Spawning Enemies Using Coroutines

We've made a lot of progress on the prototype; congrats on making it this far! Now, let's add a spawn manager to will spawn enemies over time.

## The Spawn Manager
First, we need a host GameObject for the spawn manager script. You know how to do that by now, so go ahead and create it and also create a new script named `SpawnManager` in the scripts folder, and add it as a component.

In the spawn manager script, I'll add a field named `enemyPrefab` and make it configurable via the inspector with the SerializeField attribute. To keep our hierarchy clean, I'll also create an `enemyContainer` field to be the parent for our enemy prefab instances.

I don't need the Update method, so I'll remove it and in it's place I'll add a [Coroutine](https://docs.unity3d.com/Manual/Coroutines.html) method. I will have an upcoming article to talk about Coroutines in more detail. For now, just know that this will allow us to continually spawn enemy instances.

I want to spawn a new enemy every 5 seconds as a default, but also allow for this to be adjusted via the inspector. The coroutine itself is a simple loop that yields for a provided amount of seconds, and then instantiates a new enemy instance at a random horizontal location.

```csharp
public class SpawnManager : MonoBehaviour
{
    [SerializeField] float spawnInterval = 5.0f;
    [SerializeField] GameObject enemyPrefab;
    [SerializeField] Transform enemyContainer;

    bool isStopped;
    Enemy enemy = null;

    // Start is called before the first frame update
    void Start()
    {
        enemy = enemyPrefab.GetComponent<Enemy>();
        StartCoroutine(SpawnRoutine());
    }

   ...
}
```

I've assigned the `enemyPrefab` and the `enemyContainer` references from the editor. We've already created variables in the enemy script that define the min and max X and Y values that we will want to use when spawning a new enemy, so in `Start` I am using the `GetComponent` method to get the Enemy component.

The min and max X and Y variables on the Enemy class are private, so we need to make read-only public accessors so we can use the values, but not be able to change them. I'll add the properties just beneath the variables in `Enemy.cs`.

```csharp
public float BoundaryYMax { get { return boundarYMax; } }
public float BoundaryXMin { get { return boundaryXMin; } }
public float BoundaryXMax { get { return boundaryXMax; } }
```

And here's the spawn coroutine:

```csharp
IEnumerator SpawnRoutine()
{
    while (!isStopped)
    {
        float randomXPosition = Random.Range(enemy.BoundaryXMin, enemy.BoundaryXMax);
        Vector3 spawnPosition = new Vector3(randomXPosition, enemy.BoundaryYMax);

        Instantiate(enemyPrefab, spawnPosition, Quaternion.identity, enemyContainer);
        yield return new WaitForSeconds(spawnInterval);
    }
}
```

Here you can see we are creating a new random position for newly spawned enemies and waiting for the time set in our `spawnInterval`. After playing the game for a bit, you'll end up with lots of enemies on screen!


![Spawning Enemies](https://cdn.hashnode.com/res/hashnode/image/upload/v1649292198260/rFR3J3cJ6.gif)

## Summary
We now have a spawn manager that we can build upon as our prototype evolves. 

Take care.  
Stay awesome.
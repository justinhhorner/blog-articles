## Adding a Player Attack Cooldown

Have you ever played a game that used a cooldown system that caused you to wait a certain amount of time before being able to attack, or use a spell? Game designers use this technique to create balance in the game, otherwise it will be to easy and there would be no challenge (how boring).

It turns out we're in the same situation with our player's projectile attack. There's nothing in our code to stop the player from shooting a projectile as quickly as they can hit the spacebar.

Yeah, we need to fix that. In this article, I'll cover just one way to make a cooldown system.

## Time. Time. Who has the time?
My approach is to create two variables; one that defines the interval the player has to wait until shooting (I'll add the SerializeField attribute), and another to store the future time in seconds to wait, which is a sum of the current time and the wait interval after the player fires. Let's create the new variables in the Player class.

```sharp
public class Player : MonoBehaviour
{
    ...
    [SerializeField] float fireCooldownInterval = 0.5f;
    float fireCooldownDelay = -1;

    ....
}
```
I set the interval to 0.5 as a place to start. The delay is set to -1 initially because the first to ensure the first shot happens without a delay.


## Tracking Time Elapsed
In our fire condition, we'll only instantiate a projectile if the current time is greater than our delay time. Once the player shoots a projectile, we then want to assign the current time in seconds plus the interval to our delay.

```csharp
void RespondToFire()
{
    if (Input.GetKeyDown(KeyCode.Space) && Time.time > fireCooldownDelay)
    {
        Instantiate(projectilePrefab, projectileSpawnPoint.position, Quaternion.identity);
        fireCooldownDelay = Time.time + fireCooldownInterval;
    }
}
```

I'll set the delay to one second so it's easy to see the effect. Now when I try to spam projectiles with the spacebar, I can only fire every second.

![Cooldown Projectile](https://cdn.hashnode.com/res/hashnode/image/upload/v1648419913905/tQwcFRUCi.gif)

## Summary
We now have an attack cooldown mechanic that can easily be modified by anybody on the team with no coding required. This is a pattern we can reuse throughout our game anytime we need a cooldown.

Take care.  
Stay awesome.
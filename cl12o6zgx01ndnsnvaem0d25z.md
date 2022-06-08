## Player Movement using Translate

In the last article, I gave you a short introduction to scripting in Unity. Now let’s take that a bit further by making our player move when the game begins! We’ll discuss vectors, translations, and framerate independence.

## Translating Game Objects
First I’ll take you through the steps to move our player automatically, and then we will break down how it works. To get started, let’s take a look at the Unity transform documentation. Remember, you can quickly access contextual documentation from the inspector by clicking the question button.

![xo8PxanAV.png.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1647738749564/O5F4fn6Nt.jpeg)

Now click the “Switch to Scripting” button near the top. Now scroll down and take a look at the public methods available to us on the transform. We want to move the player GameObject along the X and Y axis. Let’s check out the details of the `Translate` method.

![translate-method.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647738873888/E-3ED5Lqn.png)

The docs say translate `Moves the transform in the direction and distance of translation` which is precisely what we want. Since we want the player to move every frame, we need to use the `Update` method, which is called every frame of the game loop (typically 30 or 60 frames per second). First, let’s have the player move toward the right of the screen. 

Open the `Player.cs` file in your favorite code editor and add a call to Translate from the transform, providing a Vector with the value of X as 1 (0 for Y and Z.

```csharp
// Update is called once per frame
void Update()
{
    transform.Translate(new Vector3(1, 0, 0));
}
```

Remember, the Vector class also has several static members that we can use for common scenarios such as this. Let’s change this to use Vector3.right instead.

```csharp
// Update is called once per frame
void Update()
{
    transform.Translate(Vector3.right);
}
```

Now let’s see what happens when we start the game in Unity.


![wo-deltatime.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647739080558/YX6LtXKd3.gif)

Whoa, that was fast! Our player cube should have moved automatically to the right and off the screen. Congrats on creating movement in your first game!

It seems like magic for one line of code to accomplish movement like this. You might be wondering exactly what is this line doing; how does it work? Let’s break it down.

### How Translation Works

To reiterate, we do not call the Update method ourselves; it is called by Unity (the engine) for every frame of our game. This is import to grasp, because it means any code we place inside the Update method will be executed 30, 60 or more times every second.

Through Vector3.right, we’re providing the translate method the values 1 for X, and 0 for Y and Z. For every call to Update, we are telling the transform to translate from it’s current position, to 1 on X axis, and 0 on the Y and Z axes.

What does a value of 1 represent in this context though? By default in Unity 1 unit is a meter. That’s what the Translate method does - it translates the GameObject/transform by the Vector you provide, which gives it the direction and distance to move.

How then would we move to the left? Of course, we could use Vector3.left instead of Vector3.right, but why does that translation work? Exactly! Moving left would be we have a vector with an X value of -1, which would subtract 1 from the X position.

Wait, if the player is suppose to be moving 1 unit or meter every second, why did the player move so fast? It’s time we talk about framerate independence.

## Framerate Independence

For you, the player may have move off screen in less than a second after starting the game. If we were to play on a slower machine, each frame would take longer to execute, thus slow down the speed of the player.

Yikes! We don’t want the speed of our game object’s movement to differ based on the speed of the machine the game is running on. What a terrible experience that would be, especially for multiplayer games! The problem is our code is currently framerate dependent. We’re not taking into account the time it takes for each frame to complete.

If we had the difference in time since the last frame, we could multiply our vector to adjust the X value of the Vector by that difference to get a consistent movement speed across machines, regardless of their potential speed.

As it turns out, we do have access to that delta! It’s called Delta Time and it’s a static variable that’s available on Unity’s Time class. Let’s check out the [docs](https://docs.unity3d.com/ScriptReference/Time-deltaTime.html).

![docs-deltatime.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647739182860/rG_bNNW_6.png)

The docs say delta time is “the interval in seconds from the last frame to the current one”. That’s exactly what we need. We don’t need to import a new namespace to use the Time class because it’s part of UnityEngine, which we already have a using directive for on line 3.

```csharp
// Update is called once per frame
void Update()
{
    transform.Translate(Vector3.right * Time.deltaTime);
}
```

Here’s the result.

![with-deltatime.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647739260464/hp8zKXrFp.gif)

Not as exciting as the cube racing off the screen, sure, but now we have framerate independence!

## Multiplying Vectors

Let’s talk about some simple math that’s involved in this operation. What happens when we multiply a vector with another number?

Each component of the vector is multiplied by the number. The product of vector (1, 0, 0) and 0.5 would be 0.5, 0, and 0 because 0.5 * 1 is 0.5 and any number multiplied by zero equals zero.

## Variable Speed
We want the player to move a bit faster for our prototype, so let's create an easy way for us to add variable speed that can be adjusted easily as we playtest the game and try different speed values.

This is an important concept that we will reiterate several times through this series. When you think about working with other people on a team outside of the engineering team, you want them to be able to playtest the game and make adjustments without contacting you every time they want to try to speed something up or slow it down.

Unity has a mechanism to support editing variables in the editor, even while the game is running! We'll get into that soon. First, let's hard code a value to adjust the speed to get started.

Let's go 5 times the speed. In order to do that, we need to add a multiplier like this.
```csharp
// Update is called once per frame
void Update()
{
    transform.Translate(Time.deltaTime * 5 * Vector3.right);
}
```
Thanks to the commutative property of multiplication, we can rearrange the order of the numbers being multiplied and get the same result. I moved Time.deltaTime and our speed multiplier before Vector3.right. The reason is because it requires less multiplication calls overall when ordered this way, since we'll end up with a single number to multiple across the vector's components (x,yz).

Right now, we've hard coded the speed multiplier, which means over time if we ever need to change the value we'll have to find this exact location and change it here. That should feel bad. Our literal value of 5 does not express the intent either. This is what we call a magic number.

We are not just writing code for the computer; we are writing it for ourselves and our teammates. Therefore, I recommend writing code that expresses your intent to the best of your ability. Let's give this lonely number a name to express our intent.

Scroll to the top of the file and add a public speed field of type float to the Player class.
```csharp
public class Player : MonoBehaviour
{
    public float speed = 5.0f;

    ...
}
```

This creates a field that belongs to our Player class. It is public, which means that any other script in our game can access and modify the speed variable, which we don't want. We'll change the access modifier soon.

We're using the data type float, which allows us to represent floating-point decimal numbers because we want to have floating-point precision for specifying values for our speed.

Finally, we set the value to 5.0f, which might seem strange at first. Why do we suffix the literal value with an `f`? If you remove the f and go back to the Unity editor, you'll see It causes a compiler error with this message.

```
readonly struct System.Double
Literal of type double cannot be implicitly converted to type 'float'; use an 'F' suffix to create a literal of this type
```
This is telling us that the compiler doesn't know if you intended for the value to resolve as a double or a float. So we add the `f` suffix to tell the compiler we intend for the value to be a float. 

Without going into a ton of detail about the double data type, just know that it is double the size of a float, which allows us to store a more precise number with more places after the decimal. You can read more about floating-point types in [the docs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types).

Now let's replace that 5 with our new `speed` variable.
```csharp
// Update is called once per frame
void Update()
{
    transform.Translate(Time.deltaTime * speed * Vector3.right);
}
```

Now for the real magic! Let's go back to the Unity editor and select the player in the hierarchy. Look at the inspector for the speed variable that we set to 5. 

![Screen Shot 2022-03-20 at 12.22.51 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647750283439/qwoHL4sBx.png)

Now you and other members of your team can change this value and it will override what we set in code! However, the value will not persist if you change it while the game is running. If you change the value while the game is running, remember the value you want to keep and set it once you've stopped playing.

![change-speed.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1647750438680/tA9SGhL7U.gif)

I said we would change the accessor for the speed variable, so let's do that now. I'm going to remove the `public` accessor, as it will be private by default. Now we're going to have a problem. Since the field is private, no one else can access it, which means the Unity editor will not be able to allow us to change it from the inspector.

Fear not, Unity knew they would need a solution to this and they have provided it in the form of an attribute. In short, an attribute in C# is basically a way of describing some meta detail about the data we've applied the attribute to.

The attribute we want to use above the `speed` field is called `SerializeField`, and it looks like this.
```csharp
public class Player : MonoBehaviour
{
    [SerializeField]
    float speed = 5.0f;

    ...
}
```

With the speed variable now private, we've ensured that the data is encapsulated and controlled solely by the Player class and using the SerializeField attribute, we've let Unity know that we want our field to be Serialized so the inspector has access to the variable.

I'm going to leave the value at 5 for now, but feel free to experiment with the value for practice.

## Summary
Now we have our player moving when the game starts using framerate independence with delta time! It may not seem like much, but this is a lot to take in when you’re just getting started. 

Make sure you understand what we’ve covered here and follow along for the next article where we’ll continue to build on these concepts.

Take care.  
Stay awesome.
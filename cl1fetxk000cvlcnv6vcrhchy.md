## Player Movement with Keyboard

Now that we know how to move the player using translate, it’s time we control the movement ourselves with keyboard input. Thankfully, Unity comes bundled with some input configuration that will be useful for our game.

## The Input Manager UI

First, let’s talk about how input is managed in Unity. Unity uses an input manager UI that allows us to define input axes, and combined with the Input API, we are able to query for the input state and act upon it.

Open the [Input Manager](https://docs.unity3d.com/2021.2/Documentation/Manual/class-InputManager.html) UI by going to Edit → Project Settings, and then click Input Manager from the right-side navigation. You’ll see the default axes Unity has added. Expand the `Horizontal` axes to view the available properties.

![input-manager.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648324883065/ply-lmqld.png)

You can learn about these properties from the input manager [documentation](https://docs.unity3d.com/2021.2/Documentation/Manual/class-InputManager.html). For our horizontal and vertical input, we want a float value that ranges from left to right, 0 to 1, which is already defined by default. The `positive button` is the `d` key, which will increase from the current axes value to 1 when pressed, and the `negative button` does the opposite to decrease the axes value until it reaches -1.

If you expand the `Vertical` axes, you’ll see it is already set up to use `s` and `w`, just what we need. Also, notice that the WASD keys are set as the alternative position and negative buttons, so the primary positive and negative buttons work as well (arrow keys: up, down, left, and right).

![input-manager-zoom.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648324958111/bH9kpik7P.png)

## The Input API

We know the input axes are configured for our needs, but how do we access the values from the input manager? The [input API](https://docs.unity3d.com/2021.2/Documentation/ScriptReference/Input.html) of course!

To get the current value of the horizontal and vertical axes, we can use the GetAxis static method on the Input class and provide it with the axis name.

```csharp
// Update is called once per frame
void Update()
{
    float horizontalInput = Input.GetAxis("Horizontal");
    float verticalInput = Input.GetAxis("Vertical");

		transform.Translate(speed * Time.deltaTime * Vector3.right);
}
```

With both input float variables, now we need to pass this data to the translate method as a Vector. Let’s create a new vector called direction replace our Vector3.right with the direction Vector.

```csharp
// Update is called once per frame
void Update()
{
	float horizontalInput = Input.GetAxis("Horizontal");
	float verticalInput = Input.GetAxis("Vertical");
	Vector3 direction = new Vector3(horizontalInput, verticalInput);
        
	transform.Translate(speed * Time.deltaTime * direction);
}
```

Head back to Unity and start the game. Now, using the WASD keys, we can move the player!

![keyboard_movement.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648324970597/zqH6KQlM6.gif)

When we’re not pressing a movement key, GetAxis returns 0, which is why we don’t move; the multiplication will always produce a product of 0 until we press a key that causes the input values to change toward 1 or -1.

## Creating Boundaries
It's always good to create boundaries for yourself in life; but that's not what we're talking about here. No, we just want to create a bounding box for our player so that we can't move off the screen horizontally and all the way to the top of the screen.

Once we've translated the GameObject, we can reset the position if it goes near the boundaries. You could use if statements to check for the x and y position, but I'll use [Mathf.Clamp](https://docs.unity3d.com/ScriptReference/Mathf.Clamp.html) instead to make the code more concise.

We're going to handle the boundaries differently once we switch to 2D, but for now let's make it easy on ourselves and others by making the horizontal and vertical boundary variables available in the inspector window. I found these values by moving the player GameObject around the scene until it was in the positions I wanted to use as the boundary. I'm using a fixed aspect ratio, so this will work for my needs. I'll put the new variables directly beneath `speed`.

```csharp
[SerializeField] private float boundaryYMin = -3.50f;
[SerializeField] private float boundaryYMax = 0f;
[SerializeField] private float boundaryXMin = -8.7f;
[SerializeField] private float boundaryXMax = 8.7f;
```

With these variables defined, let's use them to clamp the position. Below you'll see that I've reused the direction vector by updating its `x` and `y` properties using the Clamp function, which will ensure the provided value does not go below the minimum or above the maximum.

```csharp
// Update is called once per frame
void Update()
{
    float horizontalInput = Input.GetAxis("Horizontal");
    float verticalInput = Input.GetAxis("Vertical");
    Vector3 direction = new Vector3(horizontalInput, verticalInput);

    transform.Translate(speed * Time.deltaTime * direction);

    direction.x = Mathf.Clamp(transform.position.x, boundaryXMin, boundaryXMax);
    direction.y = Mathf.Clamp(transform.position.y, boundaryYMin, boundaryYMax);
    transform.position = direction;
}
```

Here's the result.

![gif-boundary.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1648345433169/fhYUXc9tl.gif)

## Summary

Now we have both movement and a variable speed for our player, along with a boundary to keep the play on screen. Feel free to adjust the speed and boundary variables to your liking after a bit of playtesting. 

If you’re following along with the series, consider sharing your progress on Twitter on LinkedIn. Let me know if you have any questions, and spend some time with the documentation for the Input Manager to learn more ahead of the series.

Take care.  
Stay awesome.
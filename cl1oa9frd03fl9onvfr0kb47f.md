## What Are Coroutines in Unity?

Time for a quick break from our game. In this article, I want to talk about coroutines in Unity. What are they, and why use them?

# Coroutines
First, I should cover why coroutines exist as a tool for you to use, with a few examples of why you might want to use it. Coroutines are simply methods that take advantage of iterators using yield and the IEnumerator interface.

Code that is executed per frame is done so without scaling across subsequent frames. Meaning, the code in your methods must happen within a single frame update. If you attempt to procedurally animate or change a value over time, you may be surprised by the outcome. Using the example from the Unity manual, if you were to execute the following method, what do you think would happen?

```csharp
void Fade()
{
    for (float ft = 1f; ft >= 0; ft -= 0.1f)
    {
        Color c = renderer.material.color;
        c.a = ft;
        renderer.material.color = c;
    }
}
```

If you guessed that the renderer would be invisible immediately, you're correct! Again, think of this loop happening in the context of a single frame. If we go from 1 to 0 in a single frame, the player will never see the animation, it will be invisible immediately in the next frame!

However, what if we could scale the material color change across multiple frames, until it was invisible? Then the player could see every change we made, for as many frames as it takes to get from 1 to 0. That is exactly what coroutines allow us to do.

By setting our Coroutine as an iterator with IEnumerator, we are stating that we will yield back control to the caller and continue our work on the next frame (or delay using classes like [WaitForSeconds](https://docs.unity3d.com/ScriptReference/WaitForSeconds.html)).

We've established that a Coroutine is a method with a signature that has a return type of `IEnumerator` and the definition must use the yield statement to indicate that the method is an iterator. Here's an example of a coroutine from the Unity manual:

```csharp
IEnumerator Fade()
{
    for (float ft = 1f; ft >= 0; ft -= 0.1f)
    {
        Color c = renderer.material.color;
        c.a = ft;
        renderer.material.color = c;
        yield return null;
    }
}
```

The execution of this method, when invoked by calling [StartCoroutine](), will be scaled across multiple frames. The yield statement causes the execution to be paused until the next frame.

It's important to note that Coroutines execute on the main thread; they are **not** `threads`!

# Summary
I hope this info on coroutines has been helpful. If you have questions, please feel free to ask. I'd be happy to answer them. Stay tuned.

Take care.  
Stay awesome.

## Introduction to Pseudocode

I'm tossing in an extra article this week. I know, I know, it's not building on our game necessarily, but I want to introduce you to the concept of writing pseudocode; what it is, and how/when I use it (the right answer is whenever you want to 😉).

# What is Pseudocode?
Pseudocode is a form of planning and documenting your thoughts; step by step. It's the written steps of an algorithm or breakdown set of tasks written in a way that makes it easy for you to reason about the actual code you plan to write.

The goal is to avoid syntactical details of programming languages and focus on getting the idea from your head to the screen as quickly as possible to document the steps of an algorithm.

In music, this would be the equivalent of recording a scratch track of an idea as soon as the inspiration and melody come to mind. Later, it can be a reference as you build on the scratch track for a complete song.

# How I Write It
I use pseudocode anytime there's a new algorithm or a variation that I need to plan. I go through these stages:

```
Pseudocode > Replace > Refactor
```

Let's use a simple contrived example for the sake of this post. What if we want to use pseudocode to plan a merchant display inventory and ask the player to buy?

We can break that down into three high-level steps: get the inventory items, display them, and pose the question to the player. There would undoubtedly be a lot more involved here in an actual game, but again, let's keep it simple for demonstration.

```csharp
private void DisplayAvailableInventory()
{
    // Get store inventory from the repository
    // Loop through each item and display it in the console
    // Ask the player if they would like to buy an item
}
```

Now we can begin implementation for each line of pseudocode.

```csharp
private void DisplayAvailableInventory()
{
    // Get store inventory from the repository
    var availableInventory = repository.GetAvailableInventory();

    // Loop through each item and display it in the console
    foreach (var item in availableInventory)
    {
        Console.WriteLine($"{item.Name}----${item.Price}");
  
    }

    // Ask the player if they would like to buy an item
    Console.WriteLine("See anything you like?");
}

```

Finally, we can remove the pseudo comments and refactor the code as necessary to ensure the correct level of abstraction and separation of concerns.

# Summary
That's how and when I write pseudocode. It's a great tool to use when you're solving problems. Stay tuned.

Take care.
Stay awesome.
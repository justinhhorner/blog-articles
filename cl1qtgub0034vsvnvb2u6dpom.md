## Learning Level Design with Unity

I've been programming for many years, and because that's been my main focus, I've done little outside of that when making games. Sure, I've made some passable level designs for [game jams](https://justinhhorner.itch.io/akemas-home), but I've never spent a considerable amount of time and effort getting better at it.

That's why I've decided to take a short break from programming to become more knowledgeable on the topic and gain practical experience in designing levels in Unity. Ultimately, I aim to learn more about the different rendering pipelines supported by Unity, but for now, I'm starting with the default to make my first building level.

Here are a few things I've learned so far through the process.

## Disclaimer
I'm using assets from a paid Unity package called [Filebase](http://filebase.gamedevhq.com) that gives me quick access to hundreds (maybe thousands?) of assets that are highly efficient and ready to use. Since this will be a sci-fi building, I've picked out some floor assets to fit that style.

![Filebase Sci-fi Floors](https://cdn.hashnode.com/res/hashnode/image/upload/v1649375340722/Cz2iJ7LWR.png)

## Avoiding Repetition
With the assets imported, I then created the first iteration of the floor. The first iteration was very repetitive since I started building by repeatedly using a single floor asset.

Yeah, the asset looks great, but it's boring to see throughout an entire floor.

![Floor Asset Reuse](https://cdn.hashnode.com/res/hashnode/image/upload/v1649377153368/QzKc8D7Ht.png)

On the next iteration, I made a few asset swaps to add some variety to the floor design in the center of the room. We still want some consistency, but this is enough variation to draw attention to the center of the room as the player is walking through the hallway.

![Floor Final](https://cdn.hashnode.com/res/hashnode/image/upload/v1649376005921/ZvSlVC_Bp.png)

I also went through this process for the outside yellow parts of the floor to make it more interesting.

![Outside Floor Variation](https://cdn.hashnode.com/res/hashnode/image/upload/v1649376940351/-u6EIz2t5.png)

## Swapping Assets In-Place
I learned a shortcut to quickly swap assets in-place. If you know of an easier way, please share!

If you add the new asset as a child of the current GameObject, it will take the transform position of the parent, which is exactly what we want. Then, unparent the new child GameObject by dragging it above the parent.

The new asset has now taken the place of the original, so you can delete it and now you have the new asset swapped in place with the original.

![Swap Asset Hierarchy](https://cdn.hashnode.com/res/hashnode/image/upload/v1649376667259/6v4b7mu_3.gif)
![Swap Asset Hierarchy](https://cdn.hashnode.com/res/hashnode/image/upload/v1649376674267/WlUOoSagF.gif)

## Summary
I need to finish the walls and add some columns to the building, which I'll talk about in the next article.

Take care.  
Stay awesome.
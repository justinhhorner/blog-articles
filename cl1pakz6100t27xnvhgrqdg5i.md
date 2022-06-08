## HUD UI Design

I must admit, I'm pretty excited to finally be writing this guide on UI design! Our HUD, or heads-up display, needs to account for the items, player score, and text we'll display throughout the game. Prepare yourself for a lot of images ahead. 

Let's get started.

## New File
First, we'll create a new Photoshop file. I'm going to make an image at 1126x634.
![UI new dialog](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919768735/EnZbBrR_u.png)

Now I'll bring in our new background image in a new layer and lock it, so we don't accidentally move it around as we're working on the design.

![UI background](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919802849/05EFQZ6lJ.png)

Another step I take before diving into the design is to set margin guides along the sides of the image to ensure that It's clear that the items I am adding are inset the same amount. This is done by creating rectangles with the width and height I want UI items to be away from the sides of the screen. I use #4fe897 as the background color.

![UI guides](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919854282/L27SHCQuR.png)

Then, I'll select the layers and group them (Ctrl + G on Windows) and name the group `Guides`. Then I'll set the opacity for the group to 20% to blend into the background. I keep this as a top-most layer so that it's clear if an element is too close to the edges.

![guides opacity](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919910191/Y2VI-Ro3P.png)

Let's also add our player sprite for reference. I'll position it using the bottom guide.

![player sprite](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919932282/HnA0fXJRb.png)

With that done, we're ready to begin working on the  UI design. Ideally, once we are at this stage of development, it would be nice if our GDD (Game Design Document) was complete enough that we didn't have to worry about doing redesign work, but alas, that is not how it typically goes.

Always expect there to be changes, especially at the eleventh hour.

So although I make some definite statements here on what the design should account for, there's a good chance I'll change my mind as new ideas surface or the story slightly changes. This is not a game I've pre-built for this guide series; I am building it as we go.

With all that out of the way, let's move on.

## Lives
In my game, the player will have three lives, and we could represent that quite easily by having three player sprites next to each other at the top left of the screen. To illustrate the lives remaining vs. lost, I'm lowering the opacity of the sprite. I believe this will serve well to see how many lives are left at-a-glance.

Our guides make it easy to place this at the top left side of the screen.
![UI lives](https://cdn.hashnode.com/res/hashnode/image/upload/v1648919988518/nruAEn72I.png)

## Boost
Our boost powerup will allow the user to move faster while they have enough boost remaining. To represent that, we can use a meter that will start filled and slowly go down anytime the player activates the boost.

Since we are already representing lives in the top left of the screen, it seems natural to also have this meter in the same area. It would like this:
![UI boost](https://cdn.hashnode.com/res/hashnode/image/upload/v1648920180552/k0t3zRZXP.png)

## Shields
I'd like to have the ability for the player to stack up shields to a max of 3 or more. To represent this in the UI, we could place a small shield sprite next to a number, like `x1`, to show the player how many hits they can take without losing a life.

Again I will place this on the left side just below the boost bar.
![UI shields](https://cdn.hashnode.com/res/hashnode/image/upload/v1648920200275/EzlrPt10_.png)

## Stars
Stars play into the game's story, and we need to show how many stars the player has out of the amount remaining. We'll use a similar pattern as the shield but with the start sprite.

![UI stars](https://cdn.hashnode.com/res/hashnode/image/upload/v1648920222896/vc_hAx0vW.png)

## Messages
Finally, let's add a place for large text that will communicate the current wave or state of the game. It could be for displaying "Game Over" or "Wave 1", for example. The design will probably change, but I've placed a surface in the center of the screen for two lines of text for now.

![UI message](https://cdn.hashnode.com/res/hashnode/image/upload/v1648920241813/A1r4EUoBk.png)

## Summary
Phew, that was a lot of screenshots. I hope you enjoyed going through this with me as I iterate on ideas for the UI. Stay tuned.

Take care.  
Stay awesome.
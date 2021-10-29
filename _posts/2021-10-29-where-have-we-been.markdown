---
layout: post
title: "Where have we been, and what are we doing?"
---

##### Written by Creeper Host

# We almost haven't been doing nothing!

The last blog post was over a year ago, and is now... outdated. We actually aren't using WorldEdit any more. We aren't even using *bukkit*.

We've moved over to [Minestom](https://github.com/Minestom/Minestom) which is a [re-implementation of the Minecraft server](https://wiki.vg). So let's get into what's been happening.

## How we solved the server reopening

```
instance = new Instance();
loadWorld(instance);
...
delete instance;
```

# We got a lot of work done for our server.

With over 200 commits under our belt, we have basically re-implemented Murder Mystery, with some implementation details laying about for TinyGames. *There are bugs, but there's also another map!* Designed by KingLambChops, this map has at least 2 secrets. Gather your hat in the closet, and ~~vanish into the shadows~~. You cannot vanish into the shadows.

The server code will be open sourced once we've ironed out some more bugs and cleaned up our code, but here's a brief explanation of how it works:

There are several `Game`s. These dictate the rules of the game, and are written in pretty simple code. You can add events or make custom rules for game starting. These are the bulk of the code.

```kt
val WorldGame = game {
	setup {
		"cool_schems/pig.schem"
	}
}
```

> Minestom has *instances*, which are basically just it's worlds.

When the server starts, the server loads a schematic for the lobby and puts it into the main/spawning instance.

> I designed our own code for loading schematics. Our team hates me.

Then, when a player joins a game *either with compass or with the command*, it spins up a `GameImpl`. The `GameImpl` just runs functions from the `Game` when it needs to, then the server sends the player to the `GameImpl`'s instance, and you get to play.

## Tiny Games

Tiny Games is weird and I will not explain it.

# We got work done on other things, too!

TheThwomp's worked on their own game recently, here's an interview. You can find it on our Discord.

> C: Hello!
> 
> T: Hi
> 
> C: So, you made the square game, righ-
> 
> T: Dice Battles the Resurgance?
> 
> C: Yeah-
> 
> T: You dare insult my game? I'll ??? contact ???
> 
> C: Uhm
> 
> T: You made a mistake.
> 
> C: o-ok thank yo-
> 
> T: I will be getting the lawyers after the basement.

I've been working on my own game, too. Though currently it's literally just yellow. Eventually it'll be a sandbox-survival game that heavily focuses on multiplayer.

Finally, KingLambChops has been working on a cube-marcher for Godot. So far, it's pretty much working.

# What's next

We're going to work on fixing any bugs in Murder Mystery, and then the server *should* open and the project *should* open-source. Then we'll start working on Tiny Games.

Come back sometime for some more articles, and [follow us on twitter](https://www.twitter.com/games_rabid).

##### Written by Creeper Host

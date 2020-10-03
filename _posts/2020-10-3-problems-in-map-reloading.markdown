---
layout: post
title: "Problems in map reloading"
---

##### **Written by Creeper Host**

# Why is map reloading a problem?

In order for a game like potatowars to work, players have to be able to build blocks.

> So then, why not just give players survival, and allow them to place and break?

This is how we do it, [to an extent](https://gist.github.com/ThatCreeper/7c60186372ac643b917008a9b221dadf).

But the problem comes when you try to play again.

The map will already be filled in with blocks, and for example with potatowars, some potatos might be already destroyed,
preventing players from dying, and the map might have already dissapeared.

Oh, and the spawn room is gone.

> So how do you fix it?

Currently we actually have a really good solution to this, but I'll start by talking about the old ones.

## Solutions

# 1. Multiverse

##### This was the first solution created, on an old server that ran potatowars.

[Multiverse](https://dev.bukkit.org/projects/multiverse-core) is a bukkit plugin that allows you to create multiple worlds for your players to play in.

Like a creative world for building/testing, and a survival world for fighting mobs and bragging about resources.

Now how can you exploit this to reset a map? Good question.

The way that I came up with was to have two worlds, `pw_map` and `pw_game`.

Then, when the map was supposed to reset, something like this was run: (pseudo-code) (Also not using the Multiverse API, which  I later did.)
```java
public void resetPotatoWars() {
    Bukkit.runCommand(Bukkit.getConsoleSender(), "mv delete " + this.gameName);
    Bukkit.runCommand(Bukkit.getConsoleSender(), "mv confirm");
    Bukkit.runCommand(Bukkit.getConsoleSender(), "mv clone " + this.mapName + " " + this.gameName);
    ...
```

And it worked. Kinda.

While the map *did* reset, it lagged the server because all of the chunks and entities had to be unloaded and then reloaded.

But it still did work, so it was used through most of the development.

# 2. Server Restarting

I don't know why I chose to do this.

Imagine the problems of map reloading, *but then applied to an entire server*.

It also meant that we needed a proxy. (which we probably would still want anyway)

Using a batch file that looks like this, the servers would automatically turn back on.
```batch
for %%I in (.) do title %%~nxI
@FOR /L %%N IN () DO @(
	@java -jar server.jar nogui
)
```

(Don't actually run that, it'll put it in an infinite loop)

But this caused wait times, and *intense* server lag.

> Wait a minute, how, in Hypixel, do the maps reset in duels, while you're *still* in the game.

That was a question I asked myself. And I think I found the answer, or at least a similar one.

# 3. WorldEdit

[WorldEdit](https://enginehub.org/worldedit/) is a plugin/mod for Minecraft. It's used on most servers, as it's free and very versitile.

But one feature is *very* nice for what we're trying to do.

**Schematics**.

A schematic is a file that contains blocks, and the data of those blocks. WorldEdit can then load and paste those blocks anywhere, almost instantly.

The only real time when it's not that fast, is when we're changing millions of blocks in Tiny Games while players are still on the server. And even then it takes less time then server restarting.

Right now, I'm using a library called TerrainManager, which allows us to feed it a file and location, and it places the blocks for us.

Current usage is something like: (pseudo-code)
```java
File schematic = new File(getDataFolder(), "schematic.schematic");
terrainManager.loadSchematic(schematic, 0, 0, 0);
```

And it works well, which is nice.

##### **Written by Creeper Host**
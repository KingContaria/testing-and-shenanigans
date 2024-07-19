SeedQueue has a config built with [SpeedrunAPI](https://github.com/KingContaria/SpeedrunAPI).

You can access it by clicking "Options" on the Minecraft Title Screen, then clicking the "Mod Configs" button, identifiable by its Book & Quill texture.
This takes you to SpeedrunAPI's Mod Config Screen, where you can select the "SeedQueue" mod entry to get to the config menu.

_Please note that SeedQueue CAN'T be configured while it is active, please open the Title Screen when you want to configure something!_


## [Queue Settings](#queue-settings)

Queue Settings control how many seeds should be generated at any given time.

### Max Queued Seeds

Max Queued Seeds controls the maximum number of seeds that can be queued. Once the queue reaches this limit, SeedQueue will stop generating in the background.
When a seed is removed from the queue, either by loading into it or by resetting it on the Wall Screen, SeedQueue will resume generating.

Each Queued seed takes up memory, around 250MB per seed, so please make sure to increase the amount of RAM allocated to your Minecraft instance accordingly:
- If you're on MultiMC: Go to Settings > Java and increase your Maximum memory allocation.
- If you're on the official Minecraft launcher: Go to Installations > "..." for the installation you're using > Edit > More options and in the JVM arguments text field, find -Xmx2G and replace the 2G with however much RAM you want to allocate. G stands for gigabytes, if you want to set it in megabytes instead use something like 2500MB.

If you experience crashes because your Minecraft ran out of memory or lag spikes every time the RAM usage shown in your F3 screen goes down, you might have to increase your RAM allocation (or decrease Max Queued Seeds).

![img.png](memory_usage_f3.png)

When allocating a lot of memory with SeedQueue, it is recommended to use the ZGC garbage collector for java:
- If you're on MultiMC: Go to Settings > Java and set your JVM arguments to -XX:+UseZGC.
- If you're on the official Minecraft launcher: Go to Installations > "..." for the installation you're using > Edit > More options and in the JVM arguments text field, find and replace -XX:+UseG1GC with -XX:+UseZGC.

_Please also consider that the more seeds you queue, the more it will impact your performance because of the added memory footprint, often times the best solution is to not go overboard with your Max Queued Seeds!_

### Max Generating Seeds

Max Generating Seeds controls the maximum number of seeds that can be generating at the same time. When a seed finishes generating, a new one will be started.
If you experience excessive lag while in a world with more seeds generating in the background, you should consider reducing this option.

### Max Generating Seeds (Wall)

Max Generating Seeds (Wall) controls the maximum number of seeds generating at the same time while on the Wall Screen. This value will be used in place of Max Generating Seeds when you are resetting on the Wall Screen and will automatically switch back when you enter a seed.
It is recommended to set this option to something higher than your Max Generating Seeds option to maximize your resetting speeds, however you should not set this option any higher than your CPU's logical processors.

### Max World Generation %

Max World Generation % stops seeds from generating any further than the configured limit until you decide to load them.

_Please note that seeds will always generate until they have found a valid spawnpoint for WorldPreview to use during rendering of the preview, so don't wonder if seeds sometimes exceed this limit!_

## [Chunkmap Settings](#chunkmap-settings)

Chunkmap Settings control the rendering of the Chunkmap Overlay while in a world with SeedQueue generating seeds in the background.

### SeedQueue Chunkmaps

SeedQueue Chunkmaps controls if and how the Chunkmap Overlay is rendered. It has three modes you can configure it to use:

- Show - Render the overlay normally.
- Transparent - Render a transparent overlay to allow for better visibility.
- Hide - Do not render the overlay.

As long as you use the SpeedrunIGT and Atum mods and show the F3 screen before leaving the world, showing Chunkmaps is no longer required for verification. (see [here](https://www.speedrun.com/mc/news/8xw1rm3v))
It is highly recommended you follow these instructions as the Chunkmap Overlay may stutter if your game lags or during any part of loading, potentially leading to your run being unverifiable!

### Chunkmap Scale

Chunkmap Scale controls the size of the Chunkmap Overlay compared to the rest of your GUI. This means it will additionally still be affected by GUI Scale!

## [Wall Screen Settings](#wall-screen-settings)

Wall Screen Settings control the layout and functionality of the Wall Screen.

The Wall Screen is a screen that opens when a world is reset.
It shows previews of multiple worlds generating in the background at the same time and lets you reset them early or select ones you want to play.

### Use Wall Screen

Use Wall Screen enables resetting with the Wall Screen.

### Rows & Columns

Rows and Columns sets the default layout in which previews will be rendered on the Wall Screen.

### Simulated Window Size

Simulated Window Size sets the resolution at which previews are rendered on the Wall Screen.
To increase your field of view on these previews try decreasing the Simulated Window Height, the format of the option widget is Width x Height.

_Please note that lowering this option will affect the scale at which GUI parts of the preview are rendered, lower resolution does not affect rendering speeds of worlds in any noticeable way!_

### Reset Cooldown

Reset Cooldown prevents you from resetting previews that have just loaded in to avoid accidental resets.
The cooldown starts when a preview is first rendered on the screen.

### Bypass Wall Screen

Bypass Wall Screen will skip going to the Wall Screen and instead put you directly into the next seed if you have a fully generated and locked seed in queue.

## Performance Settings

### Wall FPS

Wall FPS sets the frame rate limit while on the Wall Screen.
While it often makes sense to limit your frame rate, lowering this option also lowers the rate at which the Wall Screen updates previews, potentially causing slower reset times.

### Preview FPS

Preview FPS sets the frame rate previews are rendered at on the Wall Screen.
Previews will continue building chunks for rendering every frame, but they won't be rendered until the next frame the preview gets updated.

_Please note that this option is relative to Wall FPS and the frame rate the Wall Screen is actually Rendering at!
This means previews might update at a lower frame rate if your Wall Screens frame rate does not match the Wall FPS. Preview FPS may work unexpectedly when setting Wall FPS to Unlimited!_

### Background Previews

Background Previews prepares additional previews to be rendered on the Wall Screen before they start getting rendered in the main grid, reducing lag when loading them later.
If you experience lag spikes when pressing Reset All, setting this option to the same amount of previews shown on your main grid (Rows x Columns) may help reduce these spikes.

When using a custom layout, these previews will be shown in the "preparing" group.

### Freeze Locked Previews

Freeze Locked Previews will stop previews that have been locked from receiving any updates to help with performance on the Wall Screen.

### Smooth Chunk Building

Smooth Chunk Building reduces the amount of new chunks that are rendered on the preview each frame.
This can help reduce stutters on the Wall Screen.

### Reduce World List

Reduce World List hides worlds that have been reset on the Wall Screen or during the preview from the world list.
This reduces lag when opening the Minecraft world list after generating lots of seeds with SeedQueue.

### [Keybindings](#keybindings)

There is currently 10 different Wall Keybindings available in SeedQueue:

- Play Instance: Leaves the Wall Screen and puts you into the currently hovered instance.
- Lock Instance: Locks the currently hovered instance. This will prevent it from being reset using Reset All, Focus Reset, Reset Row or Reset Column.
- Reset Instance: Resets the currently hovered instance.
- Reset All: Resets all instances. If you are using a custom layout, only instances in the "main" group will be reset.
- Focus Reset: Plays or locks the currently hovered instance, then resets all other instances.
- Reset Row: Resets the currently hovered row of instances.
- Reset Column: Resets the currently hovered column of instances.
- Play Next Lock: If you have a locked instance that is ready to be played, leaves the Wall Screen and puts you into that instance.
- Start Benchmark: Starts a Benchmark, see also Benchmark Resets in Advanced Settings.
- Stop Benchmark: Stops the current benchmark early.

Each Keybinding has a main key, primary keys and blocking keys. For most use cases, only the primary key is important, and you can just set that to the key you want.

#### Secondary Keys

When the primary key is pressed, the game will check that all secondary keys are pressed too before the Keybinding is activated.
This can be used to set more complicated Keybindings like Shift + E.

#### Blocking Keys

When the primary key is pressed, the game will check that all blocking keys are **not** pressed before the Keybinding is activated.

## [Advanced Settings](#advanced-settings)

Enabling Show Advanced Settings will show additional advanced options for users to configure.
Please only use these options if you know what they do or if you've been instructed to do so by someone who does!

### [Threading Settings](#threading-settings)

Threading Settings control thread counts and priorities for different parts of SeedQueue.
If you do not know what threading is, please refrain from changing these options.

There is two different kinds of threading options, thread counts and thread priorities:
- Thread counts control how many threads are launched for the specified work.
- Thread priorities control the priority given to these threads. Priorities in Java are not binding, it's up to the JVM implementation to decide what to do with them, so they may work with differing levels of success.

### SeedQueue Thread Priority

SeedQueue Thread Priority controls the priority assigned to the SeedQueue Thread responsible for launching new worlds.
Before worlds start generating, their internal server gets created and started by the SeedQueue Thread.

### Server Thread Priority

Server Thread Priority controls the priority assigned to the Integrated Server Threads of seeds generating in the background, they will switch to the default thread once they are loaded by the player and become the active Integrated Server.

### Background Worker Threads

Background Worker Threads controls the amount of threads assigned to the Background Executor.
The Background Executor is used to multi-thread chunk generation of seeds generating in the background while the player is in a world.

You should not set this option any higher than your CPU's logical processors.

### Background Worker Priority

Background Worker Priority controls the priority assigned to threads of the Background Executor.

### Wall Worker Threads

Wall Worker Threads controls the amount of threads assigned to the Wall Executor.
The Background Executor is used to multi-thread chunk generation of seeds generating while on the Wall Screen.

You should not set this option any higher than your CPU's logical processors.

### Wall Worker Priority

Wall Worker Priority controls the priority assigned to threads of the Wall Executor.

### Sodium Update Threads

Sodium Update Threads controls the amount of chunk building threads created by Sodium for each preview on the Wall Screen.

### Sodium Update Priority

Sodium Update Priority controls the priority assigned to chunk building threads created by Sodium on the Wall Screen.

### [Experimental Settings](#experimental-settings)

not sure which of these options I will remove in the future and I will probably move the rest into performance settings

### [Debug Settings](#debug-settings)

Debug Settings are meant to help test performance and debug issues that may occur while using SeedQueue.

### Watchdog

Watchdog launches an additional thread at startup that print the Render Threads stacktrace to the log every 10 seconds.
This is used to diagnose deadlocking issues where the game freezes during resetting.

_Please note that the game needs to be restarted for this option to update!_

### Show Debug Menu

Show Debug Menu renders an FPS graph and a profiler on the Wall Screen.
This is used to diagnose performance issues during Wall Rendering.

Enabling this option also enables debugging keybinds, by pressing F3 on a preview it will print some information about the current state of that instance to the log.
Pressing Shift + F3 will print the current stacktrace of the server thread.

_Please note that any runs played with this option enabled will be invalidated!_

### Benchmark Resets

Benchmark Resets sets the default amount of resets done when a benchmark is started.
Benchmarks can also be stopped at any point before that using the designated keybinding, but they will automatically stop once this number is reached.
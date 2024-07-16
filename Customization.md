SeedQueues Wall Screen can be further customized through a resource pack.
It allows changing the layout, sounds and textures used when resetting on the wall.

## [Custom Layout](#custom-layout)

To change the layout of your wall, a custom layout has to be created in a `custom_layout.json` file that is put into the `assets/seedqueue/wall/` directory of your resource pack.
This will require some very basic knowledge of how JSON works, if you don't have that you can try modifying an existing layout or asking for help in the SeedQueue Discord.

### Groups

A layout is seperated into Groups. A Group can be created in two different ways:

Firstly as a grid:
````
{
  "rows": 2,
  "columns": 2,
  "x": 0,
  "y": 0,
  "width": 1.0,
  "height": 1.0,
  "instance_background": false,
  "cosmetic": false
}
````

Secondly as a collection of positions:
````
{
  "positions": [
    {
      "x": 0,
      "y": 0,
      "width": 0.5,
      "height": 0.5
    },
    {
      "x": 0.5,
      "y": 0,
      "width": 0.5,
      "height": 0.5
    },
    {
      "x": 0,
      "y": 0.5,
      "width": 0.5,
      "height": 0.5
    },
    {
      "x": 0.5,
      "y": 0.5,
      "width": 0.5,
      "height": 0.5
    }
  ],
  "instance_background": false,
  "cosmetic": false
}
````

The values x, y, width and height can either be specified as whole numbers (for example 0, 100, 1024) or as fractions (0.0, 0.65, 1.0)
A whole number will specify a size based on pixels, while fractions will be multiplied by the Minecraft window size, meaning they scale depending on window size and monitor resolution.
If you are just creating a layout for yourself, feel free to use whole numbers. They are easier to work with and unless you change your monitor you won't have any problems with them.

If you set instance_background to `true`, a position will be covered when no preview is currently being rendered there.
This is off by default, you only have to include it if you want it enabled.

If you set cosmetic to `true`, you won't be able to reset previews when they are in this group.
This is off by default, you only have to include it if you want it enabled.

### Layout

Using these Groups, a custom layout can be created like this:

````
{
  "main": ...,
  "preparing": [
    ...,
    ...,
    ...
  ],
  "locked": ...,
  "replaceLockedInstances": false
}
````

The Main Group is the group of previews that you are actively resetting.
When pressing Reset All, these are all the instances that will be reset.

The Preparing Groups are a collection of groups, but they basically act as one group.
Instances will be rendered here while they are preparing to go to the Main group.
You can leave this out of your json if you don't want to use it.

The Locked Group is the group of previews that you have locked.
After locking an instance, it will move into this group.
You can leave this out of your json if you don't want to use it.

If you set replaceLockedInstances to `true`, instances in the Main Group that are locked and moved into the Locked Group will be replaced instantly instead of after the next Reset All.
This is off by default, you only have to include it if you want it enabled.

## [Textures](#textures)

You can change or add textures on the wall screen by putting .png texture files into the `assets/seedqueue/textures/` directory of your resource pack.

### List Of Textures

- `background.png`: The Wall Screen's background, by default the Minecraft dirt texture is used.
- `overlay.png`: An overlay to be rendered on top of the Wall Screen.
- `instance_background.png`: Rendered on positions waiting for an instance to load, by default the Minecraft dirt texture is used. See also "instance_background" in Custom Layouts.
- `lock.png`: The Lock Image rendered on locked instances, by default the Minecraft barrier texture is used. Please read below for more information.

### Lock Image

When drawing a Lock Image, SeedQueue scales the image so that the image height lines up with the previews height.
This means you have to leave transparent pixels around your lock image if you don't want it to cover your instance completely.

If you want to use multiple lock images (from which SeedQueue will choose at random for each instance), you can add more lock images named `lock-1.png`, `lock-2.png`, ...

### Animated Textures

To animate a texture, you have to:

1. Put all the frames of your animation into one texture by stacking them on top of each-other.
2. Create an .mcmeta file (texture file name + .mcmeta) in the same directory as your texture.
3. Copy the following content and paste it into your .mcmeta file, you can open it through notepad:
````
{
  "animation": {
    "frames": [
    ],
    "frametime": 1
  }
}
````
4. Add your frames in the order you would like them to play in (frames are numbered from top to bottom of your texture file, starting at 1):
````
{
  "animation": {
    "frames": [
      1,
      2,
      3,
      4
    ],
    "frametime": 1
  }
}
````
5. Edit your frametime depending on how long you want each frame to last in ticks (1/20th of a second).

## [Sounds](#sounds)

You can either change existing or even add a few new sounds to your wall.

### Replace Existing Sounds

To replace existing sounds, you have to:

1. Create a new .ogg file using the new sound, you can convert any existing sound files using online converters.
2. Rename the file to the corresponding name.
3. Put the file into the `assets/seedqueue/sounds/` directory of your resource pack.

Existing sounds include Lock Instance (lock_instance.ogg) and Reset Instance (reset_instance.ogg).

### Add New Sounds

To add new sounds, you have to:

1. Create a file called sounds.json in the `assets/seedqueue/` directory of your resource pack.
2. Copy the following content and paste it into your file, you can open the `sounds.json` through notepad:
````
{
  "play_instance": {
    "sounds": [
    ]
  },
  "reset_all": {
    "sounds": [
    ]
  },
  "reset_column": {
    "sounds": [
    ]
  },
  "reset_row": {
    "sounds": [
    ]
  },
  "start_benchmark": {
    "sounds": [
    ]
  },
  "finish_benchmark": {
    "sounds": [
    ]
  }
}
````
3. Choose the sound you want to add, then add the file name for that sound (name + .ogg) in between the brackets after `"sound"` like so:
````
  "start_benchmark": {
    "sounds": [
      "start_benchmark.ogg"
    ]
  },
````
4. Now follow the instructions for replacing existing sounds using the filename you just added.
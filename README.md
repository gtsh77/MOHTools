# MOHTools (.map editor & BSP compiler for MOH:AA)

![screenshot_2017-12-11_17-16-49](https://user-images.githubusercontent.com/8376353/33835350-3e283820-de97-11e7-8073-424b792e7d5a.png)

### Includes:
1. MoHRadiant .map editor
2. Standart MP .map files (dm/mohdm1 - dm/mohdm7, obj_team1 - obj_team4) as they were released in 2005
3. Standart SP mission 4 .map + script files
4. BSP compiler
5. MAP tutorials https://github.com/gtsh77/MOHTools/wiki

### Requirements:
1. You need original MOH:AA .pk3 files (only for original models and textures usage)

### Installation on UNIX:
1. Install wine with 32-bit support
```sh
cd /usr/port/emulators/i386-wine && sudo make install clean
```
2. Clone repo
```sh
git@github.com:gtsh77/MOHTools.git mohtools
```

3. Copy entdefs.pk3 to your MOHAA/main directory
```sh
mv /path/to/mohtools/entdefs.pk3 /path/to/mohaa/main
```

4. Start
```sh
wine /path/to/mohtools/mohradiant.exe
```

5. Ensure that your paths (basepath, mapspath, autosave) in the project properly point to your MOHAA installation. This information is stored in the qe4 file.  You change settings anytime later from File->Project Settings

Working example:<br/>
![screenshot_2017-12-11_17-17-39](https://user-images.githubusercontent.com/8376353/33835449-89913f6e-de97-11e7-9345-7745b6626876.png)

6. Go to https://github.com/gtsh77/MOHTools/wiki to check some cool "my first room" tutorials

# Original "Getting Started" by EA

Getting Started With Basic Scripts for Allied Assault Levels

Setting up MOHRadiant

1. Start by extracting the tools to a directory of your choice. Place the file, entdefs.pk3 in your MOHAA\main folder.

2. Execute mohradiant.exe. Next setup your Project Settings, which is located File > Project Settings. Under this panel set your basepath, mapspath, and autosave path.

Basepath: Set this path to your MOHAA folder(ex. c:\program files\ea games\mohaa\)
Mapspath: Set this path to your MOHAA\maps folder (ex c:\program files\ea games\mohaa\maps)
Autosave: If autosaving is enabled, MOHRadiant will automatically save your map to the folder located under this path.

Leave the rest of paths as their default.

3. Setup your preferences, located Edit > Preferences.  For this tutorial we’ll be using the default preferences.

4. Close and reopen MOHRadiant.  This will load the game data into the editor.

Maps

Note: This tutorial only covers how to setup your map for basic singleplayer and multiplayer.

1. Start by reading over the Getting Started Tutorial provided, this will give you the basic understanding of creating rooms, and compiling your map.

2. Once you have planned out and created a good portion of your map it’s time to start adding entities.

3. Note: The filename of your level is important, when creating a singleplayer level you begin the filename like so: m1l1, m1l2, etc. If you don’t name it in this fashion the sounds for the level/game will not be used. When creating a multiplayer map, simply placing the files in the maps/dm or maps/obj will make sure the level loads sounds correctly.  To add additional sounds from singleplayer to multiplayer you’ll have to edit the ubersound.scr file from one of the game’s pak#.pk3 files to include the specific sound.

4. Place mymap.pk3 in MOHAA\main and extract it to a folder of your choice.  The files provided in this .pk3 file are the files we will be referencing with this tutorial.  You may also load m1l1_mymap.map and mymap.map in MOHRadiant.

Using .tik model files in your map

1. To add objects or models into your map, all you have to do is right click anywhere on the grid and select it.  To add a table for example, right click, and select Static > Simplerectable.  

2. If you need to add a model that’s not listed, you can right click and select Script > Model or Object, and input the correct path for the model file. 

3. To move a model, simply use the map grid, to change the angle of the model, Shift + Click the model and hit N, then one of the angle buttons labeled 130, 90, 45, etc.  You can also edit the angle manually by selecting angle in the properties list.  To can the scale of the model select either + or – sign under scale, or edit it manually by selecting scale in the properties list.  To change the testanim of the selecting the model, hit N, and select + or – under Anim, this will scroll through the animations of the model, most models only have an idle animation.

Singleplayer specific

1. The first entity to add will be info_player_start.  Right click anywhere on your map grid and select Info > Player > Start. This entity spawns your player.

2. Next add an enemy entity, right click anywhere on the grid and select AI > German > Wehrmact > Soldier.

3. Now you may add weapons, items, etc. to your map the same way you would add other entities.

4. The next part to creating your singleplayer level is the scripting.  Using notepad create a file named the same as your map but with a .scr extension.  Ex. M1L1_mymap.scr.  Through this script file we can add weapons for the player, level music, execute global scripts, and much more.

5. With our script, we’ll add a few weapons. Below is the basic script we’ll be using (ex. From m1l1_mymap.scr):
```
main:

level waittill prespawn

	$player item weapons/colt45.tik
	$player item weapons/m1_garand.tik
	$player item weapons/mp40.tik

level waittill spawn

end
```
6. After scripting, you must create a precache script, using notepad create a file called yourmap_precache.scr.  This script will tell the engine to precache certain items.  In our script we added a few weapons, they will have to be added to the precache like this:
```
cache weapons/colt45.tik
cache weapons/m1_garand.tik
cache weapons/mp40.tik
```
The above is taken from m1l1_mymap_precache.scr.  You’ll also have to precache the basic effects listed below the cache weapons in m1l1_mymap_precache.scr.

7. To get a better understanding of scripting, extract MOHAA pak#.pk3 archives to your MOHAA\main folder.

Multiplayer specific

1. The first entities to add when creating a multiplayer map, will be info_player_deathmatch, right click anywhere on the mapping grid and select Info > Player > Deathmatch.  In normal deathmatch gameplay mode, players will spawn in these entities.  When creating a team deathmatch map, you must add info_player_axis entities, and info_player_allied entities, you can add these entities the same way you added deathmatch entities.  If you add an info_player_start entity it will be used as the spectator start, where the player chooses his team.

2. The most important part to creating multiplayer levels is the scripting.  Below is the basic deathmatch script:
```
main:

// set scoreboard messages
setcvar "g_obj_alliedtext1" "My map!"
setcvar "g_obj_alliedtext2" ""
setcvar "g_obj_alliedtext3" ""
setcvar "g_obj_axistext1" ""
setcvar "g_obj_axistext2" ""
setcvar "g_obj_axistext3" ""
 
setcvar "g_scoreboardpic" "mymap"

	// call additional stuff for playing this map round based is needed
	if(level.roundbased)
		thread roundbasedthread
		
	level waittill prespawn

	//*** Precache Dm Stuff
	exec global/DMprecache.scr

	level.script = maps/dm/mymap.scr
	exec global/ambient.scr mymap

	level waittill spawn

end

//-----------------------------------------------------------------------------

roundbasedthread:

	// Can specify different scoreboard messages for round based games here.
	
	level waittill prespawn

	level waittill spawn

	// set the parameters for this round based match
	level.dmrespawning = 0 // 1 or 0
	level.dmroundlimit = 5 // round time limit in minutes
	level.clockside = kills // set to axis, allies, kills, or draw

	level waittill roundstart

end
```
3. Next you must create a precache file, named yourmap_precache.scr, but this time all you need to add is:
```
exec global/DMprecache.scr
```
4. To create a loading screen for your map, you must create a 512x512 32-bit .tga image named textures/mohmenu/dmloading/mymap.tga, you can do this in most any image editing software.  To make your map load this image, you must create a scripts/yourmap.shader file, and a ui/loading_yourmap.urc file.  Please see mymap.shader and loading_mymap.urc for examples of these files.  Note: If you see, setcvar "g_scoreboardpic" "mymap" from the deathmatch script, you’ll notice that it calls scoreboard picture from your .shader file, so remember to keep the names exactly the same.

5. Deathmatch maps must be placed in maps/dm folder, and deathmatch-objective maps must be placed in maps/obj folder. Place your .bsp, .scr and *_precache.scr files in these folders.


*Special Thanks to Ben Munroe for putting this doc together

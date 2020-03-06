---
title: Vertical's Titanfall 2 to Source Guide
layout: template
filename: vertical_titanfall_2_to_source
---
# This guide was recovered from a now deleted Facepunch forum post.
The source of this guide would be located [here](https://web.archive.org/web/20190217012514/https://forum.facepunch.com/f/fbx/bskox/Tutorial-Titanfall-2-to-Source-WARNING-LONG-OP-LOTS-OF-IMAGES/1/ ), however it was removed prior to being archived. While I could recover the text for the guide, it was unformatted and needed to be reformatted from scratch. Original credit goes to Facepunch user **Vertical**. I take no credit for the content of this page, other than the recovery of the text, editing text, formatting to make it readable, updating links and adding that Cra0kol's VPK tool actually *does* have a v3.4 not linked on the website.

----

# [Tutorial] Titanfall 2 to Source (WARNING: LONG OP + LOTS OF IMAGES)
 
This guide will cover porting Titanfall 2 models to SFM and Source on the whole. A lot of effort went into creating this guide, but that doesn't mean it's perfect. Still, it couldn't be as good as it is without the help of:

- **BlueFlytrap** for figuring out most of the workarounds that I used to get around Source's limitations.
- **Zeqmacaw** for creating Crowbar.
- **REDxEYE** for helping Zeq figure out Titanfall 2's v53 .mdl format.
- **Kuro** for figuring out a method for making colored specular/specularity masks work in Source.
- **Soul_** for antagonizing the people that I also antagonize.
- And a bunch of the other helpful (and helpfully bitter) folks in the OSFM Discord.

This guide does not cover porting to Garry's Mod per se, although it's pretty par the course for any Source game. You can post renders and workshop links to what you've done here, if you want.

### Requirements:
- 3ds Max, preferably 2014 or above. I don't use Blender, so you're on your own there.
- [Game Zombie's .smd plugin](https://knockout.chat/thread/806/1) Batch Import/Export script by Jos Balcaen Titanfall 2 - Try and guess why.

> *Editor's note - [Blender](https://www.blender.org/download/) has an addon called [Blender Source Tools](http://steamreview.org/BlenderSourceTools/). It's a must if you're working with Source `.smd` models. You really don't need 3ds Max or Maya. Blender is free, and can be downloaded through Steam if you want it to update automatically. You will still need to download Blender Source Tools on your own, however. I find it strange that there is no Workshop for automatic updating of Blender addons.*

- Also, you flat out can't get textures if you're using the trial version.

> *Editor's note - The game goes on sale for like $10CAD all the time, just buy it if you want the damn models. Alternatively if you really hate EA, get an empty reloadable debit card and start a free month trial of EA Access. That literally costs $0.*

- A very rough, working knowledge of the source engine. Search Google for a guide, I won't go very in-depth here.
- [GIMP 2.8](https://www.gimp.org/downloads/ ) for converting conventional images to .vtfs. (Adobe Photoshop is fine too. If all else fails, just use GIMP - it's free.)
- [.vtf plugin for GIMP.](https://github.com/Artfunkel/gimp-vtf/releases)

> *Editor's note - [Paint.NET](https://www.getpaint.net/download.html) has a [VTF plugin](http://nemesis.thewavelength.net/files/files/pdnvtfplugin111.zip) as well - Paint.NET supports importing DDS files too, should you ever choose to use them. [VTFEdit](http://nemesis.thewavelength.net/files/files/vtfedit133.zip) works just as well too when it comes to VTFs, as it's name would imply. It does not support DDS files, however. GIMP requires an [addon](https://code.google.com/archive/p/gimp-dds/downloads) to open DDS files. You will require that addon if you choose to use NinjaRipper, or export from Intel GPA to DDS.*

- [Crowbar - For decompiling v53 .mdls and recompiling later.](https://github.com/ZeqMacaw/Crowbar/releases/)
- [Cra0kalo's Titanfall .vpk Tool](https://github.com/mom-2236/titanfall_research/raw/master/storage/Titanfall_VPKTool3.4_Portable.zip)

> *Editor's note - Cra0kola's website no longer hosts this tool for some reason - both v3.3 and v3.4 produce file not found errors on my end in Waterfox. Luckily I had backups. I've mirrored v3.4 in my repo, which was newer than the version claimed to be the latest in the original post. v3.4 does not appear to have a changelog on CraOkola's website, so I'm not sure what has changed between the two.*
> *Version 3.4 is linked above, but 3.3, should it be required, can be downloaded [here](https://github.com/mom-2236/titanfall_research/raw/master/storage/Titanfall_VPKTool3.3_Portable.zip).*

- [Intel GPA](https://software.intel.com/en-us/gpa)

----

### Table of contents:
**Section 0 - Copyright disclaimer shit.**

**Section 1 - Acquiring rigged models.**

**Section 2 - Acquiring textures.**

**Section 3 - Preparing meshes.**

**Section 4 - Preparing textures.**

**Section 5 - Materials Method 1: Colored Specular** \*easier, generally recommended, but less accurate

**Section 6 - Materials Method 2: CustomHero [Coming soon]**



## [SECTION 0] Copyright Disclaimer
I DO NOT own IP rights to Titanfall 2. Titanfall, Titanfall 2, and all assets are property of Respawn Entertainment and EA. All assets in this tutorial are used without permission. If contacted and requested to do so, I will promptly remove this guide in it's entirety. I ask that all other readers observe and acknowledge the following, or stop reading the thread at once.

## [SECTION 1] Acquiring rigged models
**STEP 1.**) Open Cra0's .vpk tool.

![CraOkola's Titanfall VPK Tool](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/16e87745-0bae-40af-837f-c382056d22d2/image.png).

**STEP 2.**) Navigate to and open the .vpk of your choice. Choose a model, and extract wherever you'd like. If you haven't changed the game's install path, you'll find all the `.vpk`'s in `C:\Program Files (x86)\Origin Games\Titanfall2\vpk`. You might as well extract the entire models folder if you plan on porting more than one model. Do note that the majority of model textures are NOT stored in `.vpk`'s.

![Cra0kola's Titanfall VPK tool showing the model folder](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/8fe6bb27-889c-424f-9815-95318a72bad9/image.png)

Important note: Most multiplayer content is stored in `englishclient_mp_common.bsp.pak000_dir.vpk`.

> *Editor's note - The exact language depends on what you have installed. If you don't have "englishclient_" `_dir.vpk`'s, then use whatever other language is present. You're looking for a `_dir.vpk` file regardless of the language, for the `mp_common` set.

**STEP 3.**) Open Crowbar, and decompile your model into its component .smds. Unlike other Source games, Titanfall 2 .mdl files contain all necessary mesh and model information. For the sake of this tutorial, we'll be porting the model `robot_stalker.mdl`. Also check my workshop for other ports to base your work off of, if you so desire. Most models consist of a handful of meshes. Important note: Despite seemingly decompiling them, Crowbar 0.56 does not support Titanfall 2 animations, which are stored in `.mdl` files suffixed: `_core`, `_workspace`, _embark, etc. This DOES include ref animations, which can be very troublesome. More on that in Section 3.

![Stalker models collected in a directory](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/095253a3-1d9c-44b7-a1d3-0fc4f28626dd/image.png)

These are the files you should be left with. You can ignore/delete the LOD `.smd`'s and `.qc` files if you have no use for them. Neither will be relevant to this tutorial. You now have your meshes! Congrats. Now you need materials. Just a warning, this part fucking sucks.

## [SECTION 2] Acquiring Textures

**STEP 1.**) Open Intel GPA Graphics Monitor.

![Intel GPA Graphics Monitor](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/fca18166-5147-49bc-bc0b-1f27affd3279/image.png)

Setting up Intel GPA to extract shit from Titanfall 2 is finicky and inconsistent, but once you get it working once it should work fine every time afterwards. Keep this window open during the next steps.

**STEP 2.**) Open Origin, if it's not already open, and set it to Offline Mode.

![Origin in offline mode](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/91b92597-199e-4801-b7db-15fa98249745/image.png)

This is the most important step. GPA can't hook into Titanfall 2 without Origin being in offline mode.

**STEP 3.**) In your system tray, right click on the blue Intel GPA icon and select Preferences from the dropdown.

![Intel GPA tray options](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/c00bd1aa-636a-4dd5-96e2-a2346202bdff/image.png)

**STEP 4.**) Enable "Auto-detect launched applications".

![Intel GPA preferences page](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/f13ef0dc-f134-4219-8c88-1d3f7d5d8f1c/image.png)

Important note: You may have to disable safe boot in your BIOS settings in order for this setting to work. Also, it is not recommended to open any other programs while Auto-detect is enabled. Disable it ASAP once you've gotten the textures you want.

**STEP 5**.) Close the preferences window, and add `Titanfall2.exe` to the list of programs in the "Analyze Application" window if it does not show up by default.

**STEP 6.**) Run Titanfall 2 from the "Analyze Application" window. You should see this box in the corner of your screen if GPA has hooked-in correctly:

![Intel GPA popup overlay](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/cb2f6534-7d1b-4714-847f-92f4609cc07c/image.png)

 **STEP 7.**) You may now re-enable Online Mode in Origin. The steps prior to this need not be repeated on the next occasion that you're searching for models, other than Step 3. Always remember to re-disable Auto-detect when you are done.

**STEP 8**.) Go in-game and find the model that you are looking for... Yes, physically.

![Stalkers as seen in-game](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/6444d6cc-eff0-4675-ae2a-79ddcf203644/image.png)

 Your model must appear on screen in order to rip its textures. Stalkers appear in almost all campaign missions, but particularly in the mission "Blood and Rust." Once you've found your model, press CTRL+SHIFT+C to capture the frame. Tip: You can find weapon, titan, and player model textures in the multiplayer customization menu.

**STEP 9.**) You can now exit Titanfall 2 and turn off Auto-detect in GPA's preferences.

**STEP 10.**) Open Intel GPA graphics frame analyzer. Tip: You can quickly open it by right clicking the Intel GPA icon in your system tray.

![Intel GPA Analyze](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/1d201ee8-d091-4afe-b986-a839c829f0b0/image.png)

**STEP 11.**) Open the Graphics Frame that has your model in it.

![Intel GPA selected captured frame](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/b887d25d-ff8c-480a-8f96-a2acc584ade5/image.png)

This might take a minute or two, it's a huge file. The window will look like this.

**STEP 12.**) Once the frame opens, note this box on the middle-left of the window.

![Intel GPA frame note](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/2c3d419a-e995-4ef2-82d8-6f3becfd94a2/image.png)

Tick "Entire Frame" at the top.

**STEP 12.**) Direct your attention to this box, which will be on the right-hand side of your screen. Click the "Textures" tab, and scroll down until you find what you believe to be your textures.

![Intel GPA texture list](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/eec35293-38c5-42e1-8d5b-060253439c08/image.png)

There will be 6 or so textures for each material, and 1 to 3 materials depending on your model. The stalker has three materials with all of the maps listed below. Important Note: For this tutorial, you will need the following: 
- Albedo Normal map (yellow)
- Roughness map (red)
- Specularity/metalness map (typically greyscale, like any other spec map; may have muted versions of the basetexture's tones)
- Ambient Occlusion Emissive map (Also grayscale, but usually black with glowing highlights like eyes and thrusters masked in white)

**STEP 13.**) Right click the texture as it shows up in the viewport, and click save. You have the choice of `.dds`, `.bmp`, `.png`, and `.jpg`. ~~I recommend .bmp.~~

> *Editor's note - Please save yourself the space and use PNG. BMP does not support complex Alpha channels, and is much MUCH bigger than PNG. There is NO reason NOT to use the lossless compression format.*

You have to do this for each texture. One by one. Oh also, they're unnamed. It sucks. If you wanna try using Ninja Ripper, go for it, but it doesn't detect all of the maps, nor all of the right colours in the albedo. So fucking finally, you've got your model's textures. Relax, take a break. You've been through a lot, and you're pretty much through with the worst of it. I'm not being facetious either, the rest of this is pretty simple.

## [SECTION 3] Preparing Meshes

In the case of the Stalker model, not much needs to be changed. However, with heavier duty models like Titans and shit, consider the following: The `.smd` format has limits on how many vertices it can contain. To get around this, you may need to divide the meshes into smaller chunks. This is the case with the Titans, whose cockpits I just compiled as separate bonemerge-able `.mdls`. Some bones are going to be in the wrong resting position/bindpose. The only way to fix this, that I know of, is to compile it as is and change the bone positions in SFM to a more natural/correct position, save that animation as a `.dmx`, and recompiling with that `.dmx` set as your reference sequence. There's not a more-graceful workaround, at least that I know of. Anyways, on with this part of the tutorial. You will be creating duplicate meshes for use with Source's coloured specular workaround. Don't worry, it's not as confusing as it sounds. Actually it might be, I wrote this section at like 6:00 AM. Sorry.

> *Editor's note: Fixing this so far has been a pain because every image link needs to be fixed, the text was a single block with no newline characters, and you had 2 Step 4's in the last section!*

**STEP 1.**) Import your model into 3ds Max or Blender. In the case of the Stalker, it is comprised of multiple `.smds`. To import each `.smd` at once in 3ds Max, you can use the batch import script linked at the very top of the page. Note that you also need the `.smd` import script for this to work at all. Note: Your model may import flipped 90 degrees on the y axis. You can fix this in 3ds Max if you really want to, but I recommend just putting "$upaxis y" in your `.qc` later.

**STEP 2.**) Perform any necessary edits, apply materials, etc. I moved a handful of bones to what looks like the correct position by looking at references. I can't provide an exact tutorial for something like this - you just kind of need to "wing it." Materials, however, are easier to explain. Create and apply materials in 3ds Max as normal, but clone them all, adding the suffix `_cs` to the clones, and the suffix `_col` to the originals. It doesn't have to be exactly that, but you do need to know which is assigned to your coloured specular mesh, and which is applied to your albedo mesh. So keep that in mind.

**STEP 3.**) Duplicate your meshes as clones. Rename them based on if you're using the CustomHero or Coloured Specular method. *Note: You're using the coloured specular method because I haven't updated this guide with CustomHero instructions yet. Also, I'd recommend naming your meshes something simple, like adding the suffix `_cs` to the coloured specular meshes, and `_col` to the meshes that will have your albedo texture applied. Ensure the correct materials are applied to the correct meshes, and you should be good to go.*

> *Editor's note: No, I don't have the instructions for the CustomHero method either.*

**STEP 4.**) Re-export, and you're done with the mesh preparation.

## [SECTION 4] Preparing Textures

**STEP 1.**) Import your albedo, AO mask, and emissive mask into a single GIMP image. *Tip: If you want, you can store ALL of your textures in one `.xcf` via descriptive layer groups, rather than separate images.*

**STEP 2.**) Move your AO mask layer above your albedo layer, and set the blend mode of the AO map to "Multiply."

![GIMP Layers](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/32efdbd4-e4ab-4fc8-964d-6aed887d4f59/image.png)
Like so.

**STEP 3.**) Move your emissive mask layer above your AO mask layer, and set the blend mode of the emissive mask layer to "Addition." Merge all layers, and export as .vtf.

> *Editor's note - You can also export as PNG and convert to VTF with a different VTF editor of choice.*

![GIMP Export](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/b61ee40b-c9dc-4dbc-a3c0-40c99606fe74/image.png)

Like so. Important note: It's up to you to decide what compression flags you use - if you care enough about them, you'll know which ones do what.

> *Editor's note - DXT compression is the default that Titanfall uses, but it's lossy. See the [Valve Software Developer Wiki's page](https://developer.valvesoftware.com/wiki/Valve_Texture_Format#Image_data_formats "Valve Software Developer Wiki's page")  on VTF colour formats for more information on what each option means.*

**STEP 4.**) Import your normal map, invert its blue channel, and apply the roughness mask (the red one) as an alpha channel. Export as .vtf, making sure to check the "Bump" option in the export settings.

**STEP 5.**) Import your specularity mask, and export it as .vtf. Your materials are now set up. Obviously, they need to go wherever your `.smds` are expecting them to be.

## [SECTION 5] Materials Method 1: Colored Specular

While not all of the specular maps are colored, per se, model stacking is still necessary. There aren't going to be steps for this one, just examples of `.qc`'s and `.vmt`'s for you to roughly follow. The `.qc` is self explanatory, whereas `.vmt`'s are something that matter on a case by case basis; you'll just need to play around with the params.

**QC Sample** - (`robot_stalker.qc`)

```
$upaxis y $scale 1 $modelname "robots/stalker/robot_stalker.mdl" $mostlyopaque $bodygroup "red_box" { studio "red_box.smd" blank } $model stalker_body_col "stalker_body_col.smd" $model stalker_legs_col "stalker_legs_col.smd" $model stalker_arms_col "stalker_arms_col.smd" $model stalker_body_cs "stalker_body_cs.smd" $model stalker_legs_cs "stalker_legs_cs.smd" $model stalker_arms_cs "stalker_arms_cs.smd"
```

`$mostlyopaque` in particular is important for the workaround to actually work.

Note that the colored specular meshes are referenced AFTER the albedo-textured meshes. If you're familiar with colored specular, you'll know why this is. If you're not, you'll figure it out when you get to the `.vmt` section. 

```
$texturegroup "skinfamilies" {
	{ "rbt_stalker_upperbody_col" "rbt_stalker_lowerbody_col" "rbt_stalker_head_col" }
	{ "rbt_stalker_upperbody_red_col" "rbt_stalker_lowerbody_red_col" "rbt_stalker_head_red_col" }
	{ "rbt_stalker_upperbody_suicide_col" "rbt_stalker_lowerbody_suicide_col" "rbt_stalker_head_suicide_col" }
	{ "rbt_stalker_upperbody_suicide_red_col" "rbt_stalker_lowerbody_suicide_red_col" "rbt_stalker_head_suicide_red_col" }
}
$cdmaterials "models/robots/stalker" $sequence idle "stalker_ref_new.dmx"  activity ACT_IDLE -1 loop fps 30
```

> *Editor's note - I have no idea how this should be formatted, I'm just guessing by the brackets.*

Yep, that's it. You'll probably want to add `$attachments` and more bodygroup options, of course, especially for the stalker in particular. But for instructional purposes, this `.qc` structure is fine. If you peeked inside the `.qc` generated by Crowbar, you'll notice a *bunch* of different unnecessary commands.

**VMT Sample** - Colored Specular (`rbt_stalker_head.vmt`)

```
"VertexLitGeneric" {
	"$basetexture" "models\robots\stalker\rbt_stalker_head_s"
		// Note that this is the specularity texture, NOT the albedo
	"$bumpmap" "models\robots\stalker\rbt_stalker_head_n"
	"$color2" "[0.00 0.00 0.00]"
	"$additive" "1.00"
		// These two commands are what make this workaround work at all. If you've ever used additive for decals or something,
		// it's just a derivative of $translucent, but it applies an albedotinted "additive" blend effect to anything behind it.
		// Setting the $color2 to total black masks out everything except for the specular reflections.
	"$phong" "1.00"
	"$phongboost" "4.5334"
		// This is up to your discretion - just depends on how intense you want the specular reflection to be.
		// That's just a random decimal at the end, I didn't do any math or anything to come to that number in particular.
	"$phongexponent" "5.00" //generally doesn't need to exceed about 15 or 20, that I've seen.
	"$phongexponenttexture" "models/titans/buddy/phongexp_255"
		// Literally just a 32x32 texture with only a pure green channel. For fully-masking albedotint.
	"$phongfresnelranges" "[3.00 5.00 7.00]"
		// These are kind of old ranges, but they should work for what you're using them for.
	"$phongalbedotint" "1.00" //ALWAYS have this enabled for colored specular.
}
```

> *Editor's note - I do understand VMT files, however.*

So yeah that's that xD

Even though I never showed you the model or materials beforehand, this is the final result that I wound up with. I might clean this up when I'm less tired.

> *Editor's note - Yeah I've done most of that for you. A few years too late.*

For now, You've got the most documentation anyone's ever done on Titanfall 2 shit. Post any questions down below as long as it isn't asking me where to download a tool that I linked above or why you're having trouble getting models out of your pirated version of the game.

![Result](https://web.archive.org/web/https://files.facepunch.com/forum/upload/109991/82ed0a0d-c19a-4e15-b316-f584d331ad1c/image.png)
The descriptor file is easily the most important for any mod, as it is what defines where the mod is located in your directory, what it is called, what versions of the game it supports, what version the mod is in, what tags the mod has (mainly used for the steam workshop), what file paths get replaced in your mod, and what the thumbnail for your mod will be. That's a lot of stuff, a lot not necessarily important to the actual gameplay, but any good mod will require most of those things, and they thankfully are some of the most simple aspects of the Hearts of Iron IV modding experience.

At Duskfall we aim to provide a simple framework that allows you to simply add in, remove, or modify aspects of this template code to help ease the process of modding, as well as provide a simple run down of what each bit of code we write means and does.


Let's look at a simple bit of code for a common and simple mod:

version = "1.0"
tags = {
	"Fixes"
	"Utilities"
}
name = "Duskfall | Overhaul"
supported_version = "1.13.5"


And now let's look at code from a more complex mod:
[NOTE: credit goes to the Cold War Iron Curtain mod for this bit of code]

name="Cold War Iron Curtain: A World Divided"
tags={
	"Gameplay"
	"Military"
	"Historical"
	"Map"
}
picture="thumbnail.png"
version="1.13.*"
replace_path="events"
replace_path="common/decisions"
replace_path="common/national_focus"
replace_path="common/ideas"
replace_path="history/units"
replace_path="common/on_actions"
replace_path="common/bookmarks"
replace_path="map/strategicregions"
replace_path="map/supplyareas"
replace_path="common/on_actions"
replace_path="common/ai_equipment"
replace_path="common/units/names_ships"
replace_path="common/bookmarks"
replace_path="common/country_tags"
replace_path="common/units/names_divisions"
replace_path="common/units"
replace_path="common/scripted_diplomatic_actions"
replace_path="history/states"
replace_path="history/countries"
replace_path="common/ai_focuses"
replace_path="common/ai_strategy_plans"
supported_version="1.13.5"
remote_file_id="1458561226"


Now that probably didn't explain too much in regards to how a descriptor file works, so I'll break it down by each attribute.

"name" is simply just the name of the mod as shown in the Steam Workshop and Paradox Launcher. This name is what is used in dependencies attribute and must be unique from other mods.
"path" describes where the mod is located within a users' directory. For mods that were created locally on a computer, entering "path = mod/modname" as a shortened mod path will automatically add the user's directory location after opening the launcher. Any folder is able to be used to store a mod, however it is important to note that only ASCII characters can be used in a mod path, otherwise it will not work, and will not be loaded (this applies particularly for diacritics or non-Latin scripts). The file seperator in the path is strictly "/" and will not work otherwise. It is also important to note that this attribute should only be present in local files stored directly on your computer, as "remote_file_id" is used for non-local mods.
"picture" is the the attribute that describes the filename of the mod thumbnail. It will appear as the thumbnail for Steam and Paradox mods alike. The image must be contained within the root directory of the mod (which is defined via "path" or "remote_file_id") and must be less than 1MB in size. This attribute must be defined after the name attribute. Local mods with a correctly defined picture will not show up on the launcher.
"version" is just a string that defines what version the mod is in, it has no real impact on the game as it doesn't change anything, and any value is accepted.
"supported_version" on the other hand is the attribute with actual impact on the mod as it defines what version of the game the mod may properly run on, rather than acting as a cosmetic version number that helps keep larger mods a bit more organized. If this attribute is not updated to the most recent game version the mod will show up as outdated in the launcher. One important thing to note is that this attribute may have an "*" in place of an integer to make updating the mod as an update releases faster. However, it should be very important to note that only the last number may be replaced with an "*" rather than any number (ex. "1.*.*" is invalid, "*" is invalid, "*.13.5" is invalid, but "1.13.* is valid").
"tags" simply defines what tags will be applied to the mod within the Steam Workshop and Paradox Mods.
"remote_file_id" is used to attach a Steam Workshop or Paradox Mods item to the mod, so that any people with the mod installed outside of the local files on your computer may access the mod and receive mod updates.
"user_dir" is an attribute that changes where the game stores your save files. This prevents loading save files from base game and vice-versa, prevents saves from your mod being loaded in base game or mods that have a different "user_dir".
"dependencies" is an attribute that changes the order in which mods are loaded, which particularly results in this mod that has those dependencies to load after every mod listed in this attribute. This of course does not make the mod require the listed dependencies in order to work. Changing the load order will always ensure that "replace_path" within any dependency mod will not touch any files from this mod, and instead that this mod will replace any overlapping filenames with it's own files. This attribute is necessary for sub-mods to work properly.
"replace_path" is used in order to unload every previously-loaded file during the main menu loading within the specified folder. This only applies to files directly within that folder, any sub-folders will left untouched. This does not force the mod to replace the folder's contents: anything higher in the load order than the mod will be loaded in the exact same way, anything lower than the mod will first get loaded before getting unloaded (e.g. the error where a file will get loaded twice if there's one with a filename differing only by capitalisation will still be present even if one of the files is intended to be replaced with replace_path), anything loaded after the main menu will still get loaded from "replaced" folders. (To be honest the "replace_path" attribute is arguably the most confusing, and to keep this relatively short I will direct you to look at the paradox wiki for more info, and yes, I did just copy and paste from the wiki because I don't know how to paraphrase what I just read).


Now for an example template for a descriptor file in a mod:
[NOTE: It is advised you add, remove, or modify the values here to fit whatever your mod's needs are

name = "Duskfall | Test"
picture = "thumbnail.png"
version = "1.0.0"
supported_version = "1.13.*"
user_dir = "duskfall_hoi4"
path = "mod/duskfall"
dependencies = { "Cold War Iron Curtain: A World Divided" "Duskfall | Overhaul" }
tags = {
	"Alternative History"
	"Balance"
	"Events"
	"Fixes"
	"Gameplay"
	"Graphics"
	"Historical"
	"Ideologies"
	"Map"
	"Military"
	"National Focuses"
	"Sound"
	"Technologies"
	"Translation"
	"Utilities"
}
replace_path="common/decisions"
replace_path="common/national_focus"
replace_path="common/ideas"


Notice how I didn't include the "remote_file_id" attribute in there, that's because it is automatically added to your descriptor file once you upload it to the steam workshop, and won't work otherwise to just give it a number.

If you are particularly fanatical at optimizing your mod you could remove all whitespace and put every item on one line to minimize the file size (but that is a bit extreme, it is really unnecessary to optimize this file really).

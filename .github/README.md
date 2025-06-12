# LibKeystone

A library for transmitting your keystone information to other players, that developers can embed in their addons.

## How do I fetch it into my addon?

You will need to use the .pkgmeta file to automatically pull this library into your addon.
Your .pkgmeta file should include the following:

```
externals:
    Libs/LibKeystone: https://github.com/BigWigsMods/LibKeystone.git/LibKeystone
```

## How do I load it?

The same way you would any other file in your addon.
For example, in your .toc file you could define the following:

`Libs\LibKeystone\LibKeystone.lua`

## How do I use it (API)?

`LibKeystone.Register(myUniqueTable, function)`

myUniqueTable - A table that is unique to your addon, so that it can be identified if you ever want to unregister it.
function - A function reference, this will run when receiving keystone information from users.

`LibKeystone.Unregister(myUniqueTable, function)`

myUniqueTable - The table unique to your addon that you provided when registering.

`LibKeystone.Request(channel)`

channel - A string, either "PARTY" or "GUILD" depending on which users you want keystone information from.

## Example code:

```
local LibKeystone = LibStub("LibKeystone")
local myUniqueTable = {}

-- keyLevel=Number, keyMap=Number, playerRating=Number, playerName=String, channel=String
LibKeystone.Register(myUniqueTable, function(keyLevel, keyMap, playerRating, playerName, channel)
	print(string.format("User %q has a %q keystone that's level %d and a rating of %d.", sender, GetRealZoneText(keyMap), keyLevel, playerRating))
end)

-- Attach these to something the user interacts with, like a button
LibKeystone.Request("PARTY")
--LibKeystone.Request("GUILD")
```

## Download

* <https://www.curseforge.com/wow/addons/libkeystone>

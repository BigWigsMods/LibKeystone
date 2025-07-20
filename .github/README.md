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

`LibKeystone.Unregister(myUniqueTable)`

myUniqueTable - The table unique to your addon that you provided when registering.

`LibKeystone.Request(channel)`

channel - A string, either "PARTY" or "GUILD" depending on which users you want keystone information from.

## Example code:

```
local LibKeystone = LibStub("LibKeystone")
local myUniqueTable = {}

-- keyLevel=Number, the level of the keystone
-- keyMapID=Number, the challenge map ID of the keystone
-- playerRating=Number, the Mythic+ rating of the player
-- playerName=String, the name of the player
-- channel=String, the channel the data was received from (PARTY or GUILD)
LibKeystone.Register(myUniqueTable, function(keyLevel, keyMapID, playerRating, playerName, channel)
	-- You can use C_ChallengeMode.GetMapUIInfo(keyMapID) to get info like the map name
	local challengeMapName = C_ChallengeMode.GetMapUIInfo(keyMapID)
	print(string.format("%s has a %q keystone that's level %d and has a rating of %d.", playerName, challengeMapName, keyLevel, playerRating))
end)

-- Attach this to something the user interacts with, like a button click
LibKeystone.Request("PARTY")
```

## Download

* <https://www.curseforge.com/wow/addons/libkeystone>

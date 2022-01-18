---
title: Packet Structure
parent: Networking
nav_order: 1
---

# Terraria Packet Structure
All packets in the latest Terraria release.

## Basic Structure

| Size | Type | Description            |
|:-----|:-----|:-----------------------|
| 2    | U16  | Packet Length In Bytes |
| 1    | U8   | Packet ID              |
| ?    | ?    | Packet Data            |


## Connect Request [1]
Server
{: .label }


| Size | Type   | Description     | Notes                                                        |
|:-----|:-------|:----------------|:-------------------------------------------------------------|
| ?    | String | Release Version | Formatted as so: `Terraria[ReleaseNum]`, e.g. `Terraria244`. |


## Disconnect [2]
Client
{: .label }


| Size | Type   | Description       | Notes |
|:-----|:-------|:------------------|:------|
| ?    | String | Disconnect Reason | -     |


## Continue Connecting/Set User Slot [3]
Client
{: .label }


| Size | Type | Description | Notes                                                                                                         |
|:-----|:-----|:------------|:--------------------------------------------------------------------------------------------------------------|
| 1    | U8   | Player ID   | Unfortunately since the type of this is a byte, there can only be a maximum of 255 players connected at once. |


## Player Info [4]
Both
{: .label }

| Size | Type   | Description      | Notes                                                                                                                                             |
|:-----|:-------|:-----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | U8     | Player ID        | -                                                                                                                                                 |
| 1    | U8     | Skin Variant     | -                                                                                                                                                 |
| 1    | U8     | Hair             | -                                                                                                                                                 |
| ?    | String | Player Name      | -                                                                                                                                                 |
| 1    | U8     | Hair Dye         | -                                                                                                                                                 |
| 1    | U8     | Hide Visuals     | Not sure what this does                                                                                                                           |
| 1    | U8     | Hide Visuals 2   | Not sure what this does                                                                                                                           |
| 1    | U8     | Hide Misc        | -                                                                                                                                                 |
| 3    | Color  | Hair Color       | -                                                                                                                                                 |
| 3    | Color  | Skin Color       | -                                                                                                                                                 |
| 3    | Color  | Eye Color        | -                                                                                                                                                 |
| 3    | Color  | Shirt Color      | -                                                                                                                                                 |
| 3    | Color  | Undershirt Color | -                                                                                                                                                 |
| 3    | Color  | Pants Color      | -                                                                                                                                                 |
| 3    | Color  | Shoe Color       | -                                                                                                                                                 |
| 1    | U8     | Difficulty Flags | Bits: 1: Softcore, 2: Mediumcore, 3: Hardcore, 4: Extra Accessory, 5: Creative (Journey) <br> <br> Only one of the first 3 bits should be active. |
| 3    | U8     | Torch Flags      | Bits: 1: Using Biome Torches, 2: Happy Fun Torch Time, 3: Unlocked Biome Torches.                                                                 |


## Set Player Inventory Slot [5]
Both
{: .label }

| Size | Type | Description | Notes                                 |
|:-----|:-----|:------------|:--------------------------------------|
| 1    | U8   | Player ID   | -                                     |
| 2    | S16  | Slot ID     | -                                     |
| 2    | S16  | Stack Size  | Should never be below 1 or above 999. |
| 1    | U8   | Item Prefix | Examples: Broken, Godly, Legendary.   |
| 2    | S16  | Item ID     |                                       |


## Request World Info [6]
Server
{: .label }
Requests that <a href="#world-info-7">World Info</a> be sent.

| Size | Type | Description | Notes |
|:-----|:-----|:------------|:------|
|      |      |             |       |


## World Info [7]
Server
{: .label }
Sends a lot of information about the world and its current state.

| Size | Type            | Description                 | Notes                                                                                                                                                         |
|:-----|:----------------|:----------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 4    | S32             | Time                        | -                                                                                                                                                             |
| 1    | U8              | Day and Moon Flags          | Bits: 1: Day Time, 2: Blood Moon, 3: Eclipse.                                                                                                                 |
| 1    | U8              | Moon Phase                  | -                                                                                                                                                             |
| 2    | S16             | Max Tiles X (World Width)   | -                                                                                                                                                             |
| 2    | S16             | Max Tiles Y (World Height)  | -                                                                                                                                                             |
| 2    | S16             | Spawn X                     | -                                                                                                                                                             |
| 2    | S16             | Spawn Y                     | -                                                                                                                                                             |
| 2    | S16             | Surface layer               | Y Coordinate of the world's surface layer.                                                                                                                    |
| 2    | S16             | Rock Layer                  | Y Coordinate of the world's rock layer.                                                                                                                       |
| 4    | S32             | World ID                    | -                                                                                                                                                             |
| ?    | String          | World Name                  | -                                                                                                                                                             |
| 1    | U8              | Difficulty                  | 1: Normal, 2: Expert, 3: Master, 4: Creative (Journey).                                                                                                       |
| 1    | UUID (U8 Array) | World UUID                  | -                                                                                                                                                             |
| 1    | U64             | World Generator Version     | -                                                                                                                                                             |
| 1    | U8              | Moon Type                   | -                                                                                                                                                             |
| 1    | U8              | Tree Background 1           | -                                                                                                                                                             |
| 1    | U8              | Corruption Background       | -                                                                                                                                                             |
| 1    | U8              | Jungle Background           | -                                                                                                                                                             |
| 1    | U8              | Snow Background             | -                                                                                                                                                             |
| 1    | U8              | Hallow Background           | -                                                                                                                                                             |
| 1    | U8              | Crimson Background          | -                                                                                                                                                             |
| 1    | U8              | Desert Background           | -                                                                                                                                                             |
| 1    | U8              | Ocean Background            | -                                                                                                                                                             |
| 1    | U8              | Mushroom Background         | -                                                                                                                                                             |
| 1    | U8              | Underworld Background       | -                                                                                                                                                             |
| 1    | U8              | Tree Background 2           | -                                                                                                                                                             |
| 1    | U8              | Tree Background 3           | -                                                                                                                                                             |
| 1    | U8              | Tree Background 4           | -                                                                                                                                                             |
| 1    | U8              | Ice Back Style              | -                                                                                                                                                             |
| 1    | U8              | Jungle Back Style           | -                                                                                                                                                             |
| 1    | U8              | Hell Back Style             | -                                                                                                                                                             |
| 4    | Float           | Wind Speed Target           | -                                                                                                                                                             |
| 1    | U8              | Cloud Count                 | -                                                                                                                                                             |
| 4    | S32             | Tree X 1                    | -                                                                                                                                                             |
| 4    | S32             | Tree X 2                    | -                                                                                                                                                             |
| 4    | S32             | Tree X 3                    | -                                                                                                                                                             |
| 1    | U8              | Tree Style 1                | -                                                                                                                                                             |
| 1    | U8              | Tree Style 2                | -                                                                                                                                                             |
| 1    | U8              | Tree Style 3                | -                                                                                                                                                             |
| 1    | U8              | Tree Style 4                | -                                                                                                                                                             |
| 4    | S32             | Cave Back X 1               | -                                                                                                                                                             |
| 4    | S32             | Cave Back X 2               | -                                                                                                                                                             |
| 4    | S32             | Cave Back X 3               | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 1           | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 2           | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 3           | -                                                                                                                                                             |
| 1    | U8              | Cave Back Style 4           | -                                                                                                                                                             |
| 1    | U8              | Forest 1 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Forest 2 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Forest 3 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Forest 4 Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Corruption Tree Top Style   | -                                                                                                                                                             |
| 1    | U8              | Jungle Tree Top Style       | -                                                                                                                                                             |
| 1    | U8              | Snow Tree Top Style         | -                                                                                                                                                             |
| 1    | U8              | Hallow Tree Top Style       | -                                                                                                                                                             |
| 1    | U8              | Crimson Tree Top Style      | -                                                                                                                                                             |
| 1    | U8              | Desert Tree Top Style       | -                                                                                                                                                             |
| 1    | U8              | Ocean Tree Top Style        | -                                                                                                                                                             |
| 1    | U8              | Mushroom Tree Top Style     | -                                                                                                                                                             |
| 1    | U8              | Underworld Tree Top Style   | -                                                                                                                                                             |
| 4    | Float           | Max Rain                    | -                                                                                                                                                             |
| 1    | U8              | Event Info 1                | Bits: 1: Shadow Orb Smashed, 2: Downed Boss 1, 3: Downed Boss 2, 4: Downed Boss 3, 5: Hardmode, 6: Downed Clown, 7: Server Side Character, 8: Downed Plantera |
| 1    | U8              | Event Info 2                | -                                                                                                                                                             |
| 1    | U8              | Event Info 3                | -                                                                                                                                                             |
| 1    | U8              | Event Info 4                | -                                                                                                                                                             |
| 1    | U8              | Event Info 5                | -                                                                                                                                                             |
| 1    | U8              | Event Info 6                | -                                                                                                                                                             |
| 1    | U8              | Event Info 7                | -                                                                                                                                                             |
| 2    | S16             | Copper/Tin Ore Tier         | Block ID 7 (Copper) or 166 (Tin).                                                                                                                             |
| 2    | S16             | Iron/Lead Ore Tier          | Block ID 6 (Iron) or 167 (Lead).                                                                                                                              |
| 2    | S16             | Silver/Tungsten Ore Tier    | Block ID 9 (Silver) 168 (Tungsten).                                                                                                                           |
| 2    | S16             | Gold/Platinum Ore Tier      | Block ID 8 (Gold) or 169 (Platinum).                                                                                                                          |
| 2    | S16             | Cobalt/Palladium Ore Tier   | Block ID 107 (Cobalt) or 221 (Palladium).                                                                                                                     |
| 2    | S16             | Mythril/Orichalcum Ore Tier | Block ID 108 (Mythril) or 222 (Orichalcum).                                                                                                                   |
| 2    | S16             | Adamantite/Titanium         | Block ID 111 (Adamantite) or 223 (Titanium).                                                                                                                  |
| 1    | S8              | Invasion Type               | -                                                                                                                                                             |
| 8    | U64             | Lobby ID                    | Always 0, except if using the Steam Social API.                                                                                                               |
| 4    | Float           | Sandstorm Severity          | -                                                                                                                                                             |
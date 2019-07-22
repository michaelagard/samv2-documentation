# SAMv2 | Sam's Autopilot Manager Version 2 Unnoficial Documentation

SAMv2 is an autopilot navagation manager that allows your ships to dock to multiple docks with a press of a button.

## Installation:

### List of components:
| Ship Component | Description |
| :--- | :--- |
| Remote Controller   | This will allow SAM to control your ship during an auto-docking proceedure. |
| Camera              | The cameras will aid in your ship automatically navigating obsitacls. Ideally you will have 3: one facing UP, FRONT & DOWN. Avoid that they are obstructed by other blocks in the ship. |
| LCD Panel           | The screen is primarily used for the sys log to get your ship SAM ready. The screen is not required once you've configured everything. |
| Programmable block  | The programmable block is used to hold the SAMv2 script. Stored variables are able to be edited here. More on that later. |
| Connector			      | The ship will require one for docking to take place. You can have multiple though with advanced configurations. |
| Antenna 			      | Important as this allows the ship to learn about Connectors in other grids. |

| Station Component | Description |
| :--- | :--- |
| Programmable block	| The programmable block is used to hold the SAMv2 script. Stored variables are able to be edited here. More on that later. |
| Connector 			    | The station will require one for docking to take place. You can have multiple though with advanced configurations. |
| Antenna 				    | Important as this allows the Station to advertise its connectors to other grids. However this block does not need to be tagged. Make sure it has enable broadcast set. |

## Tagging blocks

SAMv2 supports two methods for tagging a block.

### Custom Data
This allows the blocks to be tagged without polluting the block name, good for antennas. Example, add the following to the Custom Data of an LCD pannel:
```
SAM.
SAM.Log
```
The initial `SAM.` is important to the tagging process because this makes SAM look for this specific block.

### Block Name

This allows tagging the block using the block name. Example for an LCD Pannel:

```
Wide LCD Panel [SAM LOG]
```

## Usage
Tag all required blocks above with `SAM.` or adding `[SAM]` in the block name.

More specifically:

1. For Station `Programmable blocks`: add the tag "advertise". Example: `[SAM ADVERTISE]`

1. For Station Programmable blocks: override the grid name (no spaces). Example: `[SAM ADVERTISE Name=NewGridName]`

1. For Station Connectors: override the block name (no spaces). Example: `[SAM Name=NewConnectorName]`
 or use custom data
```
SAM.
SAM.Name=NewConnectorName
```
1. For Ships Wide LCD Pannels: add the tag "log" for seeing the Syslog. Example: `[SAM LOG]` or use custom data
```
SAM.
SAM.LOG
```

1. For Ships Programmable blocks: override the default speed. Example: [SAM Speed=50]

1. For Ships Programmable blocks: use continuous docking to docking navigation by defining wait times in seconds. Example: `[SAM Wait=10]`

## Ship Commands

To use these commands, run the Programmable block SAMv2 script with these arguments:
### Menu
| Command | Description |
| :--- | :--- |
| `PREV`                  | Previous item. |
| `NEXT`                  | Next item. |
| `SELECT`                | Select the existing item (for Configuration screen). |
| `SCREEN`                | Changes back and forth between Navigation and Configuration screens. | 

### Waypoint
| Command | Description |
| :--- | :--- |
| `ADD`                   | Adds the present ship position as an entry. Good as a Waypoint. |
| `ADD STANCE`            | Adds the present ship position and orientation as an entry. |
| `REMOVE`                | Removes entries added with the ADD command and old docks that have stopped being advertised (have a ? before them) |

### Auto Navigation
| Command | Description |
| :--- | :--- |
| `START`                 | Starts navigation to the selected dock in the Navigation screen. |
| `START PREV`            | Selects the previous dock in the Navigation screen and Starts navigation. |
| `START NEXT`            | Selects the next dock in the Navigation screen and Starts navigation. |
| `START (GPS Coordinate)`| Starts navigation to the GPS coordinate copied from the GPS screen. |
| `STOP`                  | Immediately stops navigation. |
| `TOGGLE`                | Toggle between START/STOP. |
| `GO (Connector Name)`   | Will immediately start navigating to the Connector Name. The connector name must be the one given with the TAG Name. |

### Maintenance
| Command | Description |
| :--- | :--- |
| `CLEARSTORAGE` | Clears storage, requires the program block to recompile. |
| `CLEARLOG` | Clears the Log. |

## Text Pannels
Text panels can be used for viewing the log, navigation, and configuration screen. To access these screens, use either one of the following block name or custom data tags.
| Block name TAG | Custom data TAG | Description |
| :--- | :--- | :--- |
| `[SAM LOG]`   | `SAM.LOG`   | Shows the log. |
| `[SAM NAV]`   | `SAM.NAV`   | Shows the NAV screen. |
| `[SAM CONF]`  | `SAM.CONF`  | Shows the configuration screen. |
| `[SAM OVR]`   | `SAM.OVR`   | Allows you to override the font size and style. |


## Path docking
You can use LCD screens with an attribute named "Name" with the same value as the one your Dock has. The LCDs are sorted by distance to the Dock, and the the ship will follow them all the way. This can be used to avoid colisions or when your dock is inside some building. See the video for more details.

## Timer Notifications
Notifications can be sent to timer blocks when certain actions are accomplished. Tag your timers with:

| Block name TAG | Description |
| :--- | :--- |
| `[SAM DOCKED]`    | Starts the timer when the ship docks. |
| `[SAM NAVIGATED]` | Starts the timer when the ship finishes navigation. |

### to be tested
custom data tags

## When something does not work

1. Do you own all blocks in the grid? You should.
1. Does your ship have enough power/hydrogen? It must.
1. Does your ship have enough Thrust power in every direction? Including UP. It must.
1. Do your Antennas have enough range to cover each other and are they enabled to broadcast? They should.
1. Are all your blocks in the same main grid? They should.

Things are still wrong? Leave a comment with a link to the game file to the link below.
https://steamcommunity.com/sharedfiles/filedetails/?id=1653875433
To see how to write flags, check the _syntax_ page!


Flags are used to change what happens when a drop is dropped or how it acts. The are multiple kinds of flags, the main ones are:

* General Flag: Will always be executed
* Player Flag: Will only execute if there is a player attached to the drops
* Item Flag: Will only executed if the drop is an item
* Entity Flag: Will only execute if the drop is an entity
* Condition Flag: Drops won't be selected if any of their condition flags return false

Additionally, all flags are bound to a trigger, by default the trigger is on spawn, the trigger list is:

* onPreSpawn: Runs before the loot is dropped, won't execute item/entity flags
* onSpawn: Runs when the item is spawned
* onPickUp: Runs when the item is picked up
* onLand: Runs when the item touches the ground
* onOpen: Runs when a lootbag is opened
* onRoll: Runs every time a lootbag is rolled by the _roll_ flag


# Flag Compendium
## General Flags

### Broadcast
Sends a message to everyone in the server
```yml
# Example use: Tell the whole server the player got a rare drop
- diamond{broadcast=%player.name% looted a rare diamond from a field boss!}
```

### Command
Runs a command as console
```yml
# Example use: Make the player progress in a quest
- mythicmobs:MoonTotem{onpickup=[command=questplugin stage:moonBoos setProgress:3 for:%player%]}
# Made up command
```

### Delay
Causes this and all following drops to have X ticks of delay
```yml
# Example use: First drop the common items then the rare ones
- coal
- copper
- iron_ingot{delay=10}
- gold_ingot
- diamond{delay=20}
- emerald
```

### Discord
Uses [DiscordSRV](https://www.spigotmc.org/resources/discordsrv.18494/) to send messages/embeds to a discord server

| Attribute | Default | Description |
| ------- | ----- | ------------- |
| Embed | true | If the message should be embed |
| Title | - | The title of the embed |
| Color | - | The color of the embed, accepts RGB |
| Thumbnail | - | The thumbnail of the embed, has to be an image link |
| Author | - | The author of the embed |
| Footer | - | The footer of the embed |
| Image | - | The image of the embed, has to be an image link |
| Avatar | - | If it should show the player head as the thumbnail |
| Channel | - | The channel where the message should be send |

```yml
# Example usage: Send an embed when a player is dropped a rare item
- diamond{discord=%player% got an ultra rare sword! <channel=710138582853091371;color=#bdca24;thumbnail=https://cdn.discordapp.com/attachments/710138582853091371/878539180219723786/unknown.png;footer=Chance of drop: 0.1%;author=%player%>}
```

### Skill ( MythicMobs Skill )
Runs a skill from MythicMobs, with the base mob as target, player as caster and mob location as origin
```yml
- diamond_block{skill=TestSkill}

TestSkill:
  Skills:
  - SetBlockType{material=DIAMOND_BLOCK} @target # Places diamond block at mob location
  - SetBlockType{material=GOLD_BLOCK} # Places gold block at player location
  - message{m=hello} # Sends message to player
```

### Stop
Once a drop with this flag is dropped, it stops all the other drops intended for this player
```yml
# Example Usage: When a rare item drops, don't drop more items
- coal
- diamond{stop=true} 0.5
- iron_ingot # 50% Chance for this and the drops below to not be dropped
- copper_ingot
- emerald{stop=true}
- gold_ingot # Will never be dropped
```
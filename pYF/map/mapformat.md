# Map format

A map is a folder containing a JSON file and two other folders:
- `config.json`
- `map.json`
- `player.json`
- `actors`
- `items`


## Layout

### `config.json`

The `config.json` file is for setting miscellanious settings such as default descriptions.

### `map.json`

The `map.json` file includes the map — which consists of a number of connected rooms — and its contents, the aformentioned items and actors.

### `player.json`

The `player.json` file dictates where the player starts the game and what they start it with.

### `actors`

The `actors` folder looks like this:
- `conversations`
- `_actors.json`
- `bob.json`
- `villager1.json`
- `guard.json`

The `_actors.json` file is special; it contains basic info on all the items in the game. It's loaded on start.

The other JSON files contain the specific definitions of the actors and are loaded as needed.

The `conversations` folder looks like this:
- `bob-info.json`
- `bob-quests.json`
- `guard-rejected.json`
- `guard-accepted.json`
- `villager-generic.json`

Conversations are explained elsewhere.

### `items`

The `items` folder looks something like this:
- `_items.json`
- `hat.json`
- `arrow.json`
- `apple.json`

The `_items.json` file is like the `_actors.json` file. It contains simple descriptions of the actors and is loaded on game start.

The other JSON files contain the specific definitions of the items and are loaded as needed.

## `config.json` format

The `config.json` file includes default values and rules.

```json
{
  "rules": {
    "include_items": True, // Include items in short descriptions
  },
  "defaults": { // What values will default to if not specified
    "immovable": "You couldn't move the [item_description] even if you wanted to.",
    "inedible": "The [item_description] doesn't look very tasty to you.",
    "no_conversation": "[actor_name] isn't very talkative right now.",
  }
}
```

## `map.json` format

Rooms are the building blocks of a map. Every map consists of a number of rooms that have connections, items, and actors in them.

The `map.json` file is formatted like so:

```json
{
  "crossroads": {
    "name": "Crossroads",
    "short_description": "The intersection of a north-south and northwest-east road.",
    "description": "The intersection of two roads.\nOne road goes north-south, with the dark forest to the south and a town to the north a ways.\nThe other goes northwest and bends east...",
    "connected": {
      "northwest": "mount_foothills",
      "north": "city_gates",
      "east": "valley_trail",
      "south": "forest_exit"
    },
    "items": ["bench"],
    "actors": ["bob"],
  },
}
```

### `player.json` format

```json
{
  "name": "", // Name will be decided by player
  "location": "crossroads",
  "inventory": {
    "hat": 1, 
    "apple": 1, 
    "arrow": 5
  }
}
```

### `_actors.json` format

```json
{
  "bob": {
    "name": "Bob",
    "description": "A dark-haired, bearded man, who simultaneously looks tired and oddly regal. He is sitting on a wooden bench and watching you, as if he were waiting for you."
  }
}
```

### `actor.json` format

```json
// bob.json
{
  "fullname": "Bob Puriraksasa Mbretimadh të Pavelló XIV The Conquerer, Great Arch-baron of Àite-air-an-robh-craobh-fionnar-oirre",
  "conversation": "bob-info"
  "hp": 15
  "inventory": {
    "greatsword": 1
    "entry_pass": 1
  }
}
```

### `conversation.json` format

This will be explained in the future, in a different file.

### `_items.json` format

```json
{
  hat: {
    "name": "hat",
    "short_description": "brown leather cowboy hat"
    "grabbable": True,
    "grab_description": "",
  }
}
```

### `item.json` format

```json
// hat.json
{
  "detailed_description": "The cowboy hat is well-tailored and made of fine brown leather. Despite being a bit tattered and muddy, it's still apparent it was made with skill. You keep it with you on your adventures as a souvenier of your past."
  "flags": {
    "wearable": True,
    "edible": False,
    "weapon": False,
    "...": "..."
  }
  "descriptions": {
    "don_description": "You don your trusty cowboy hat.",
    "doff_description": "", // Use default
    "edible_description": "It's just an expression. You don't actually have to do it.",
    "weapon_description": "",
    "throw_description": "You toss the hat [direction]. It spins and flies through the air for a bit before landing with a quiet thump.",
    "...": "..."
  }
}
```

## Future Projects
- Special descriptions when entering a room from a specific other room. These descriptions would be included in the `connected` section of the rooms.
- Support for translations
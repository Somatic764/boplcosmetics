# Bopl Cosmetics online list

The list of personal cosmetics for the Bopl Cosmetics mod. Every copy of the mod downloads
`cosmetics.json` and its pictures from this repository when the game starts, so a change here
reaches everyone the next time they start the game. No mod update is needed.

This repository must stay **public**, or the mod can't download it.

## Giving someone a hat

Add their Steam ID to the hat's `owners`. A Steam ID is the 17-digit number in a Steam profile
link (`steamcommunity.com/profiles/76561199438881251`). If someone has a custom profile link
(`steamcommunity.com/id/name`), look their number up on a site such as steamid.io.

```json
"owners": [
    "76561199438881251",
    "76561198000000000"
]
```

To take a hat away, remove their ID. `"owners": ["*"]` gives a hat to everyone.

## Adding a hat

1. Put the picture in `hats/`, for example `hats/crown.png`. It should be a PNG with a see-through
   background, facing right (the way the slime looks), at most 1024 pixels each way and 1 MB, cut
   tightly around the hat.
2. Add an item to `items` in `cosmetics.json` (commas between items):

```json
{
    "id": "crown",
    "type": "hat",
    "name": "Golden Crown",
    "picture": "hats/crown.png",
    "width": 0.8,
    "sink": 0.4,
    "shift": 0,
    "runTilt": 0,
    "runSink": 0,
    "owners": ["76561199438881251"]
}
```

| Field | What it does |
| --- | --- |
| `id` | A short name: small letters, digits and dashes, never changed once people wear it. |
| `type` | `hat` (later versions of the mod will add more types). |
| `name` | What the hat grid shows. |
| `picture` | The picture's path in this repository. |
| `width` | The hat's width as a share of the slime's width (Christmas Hat 0.82, Traffic Cone 0.8, Propeller Cap 0.95). |
| `sink` | How much of the hat's height sits below the top of the head (0 = on top, 0.5 = half pulled down). |
| `shift` | How far it sits ahead of the eyes' middle, as a share of its own width (below 0 = towards the back). |
| `runTilt` | Degrees the hat leans while the slime runs: above 0 tips it back to follow the running body, below 0 tips it forward, 0 (or left out) keeps it level. Needs Bopl Cosmetics 1.2.2 or newer; older versions keep it level. |
| `runSink` | How much lower the hat sits while the slime runs, as a share of its height (the running head is lower under the hat; the Christmas Hat uses 0.2 with its 20° lean). Needs Bopl Cosmetics 1.2.3 or newer. |
| `owners` | Who can wear it: Steam IDs, or `"*"` for everyone. |

## Notes

- Only the owners can pick a hat, and everyone else's game only shows it on its owners, so
  nobody can show off someone else's hat by editing their settings.
- Anyone can read this repository, including the owners' Steam IDs.
- GitHub can take a few minutes to serve a changed file, so a change may need a second game start.
- If the list has a mistake, the mod leaves out the broken item and says why in its log
  (`BepInEx\LogOutput.log`, lines starting with "Online cosmetics list").

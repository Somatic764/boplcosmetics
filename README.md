# Bopl Cosmetics online list

The list of personal cosmetics for the Bopl Cosmetics mod. Every copy of the mod downloads
`cosmetics.json` and its pictures from this repository when the game starts, so a change here
reaches everyone the next time they start the game. No mod update is needed.

This repository must stay **public**, or the mod can't download it.

## Giving someone a hat or colour

Add their Steam ID to the item's `owners`. A Steam ID is the 17-digit number in a Steam profile
link (`steamcommunity.com/profiles/76561199438881251`). If someone has a custom profile link
(`steamcommunity.com/id/name`), look their number up on a site such as steamid.io.

```json
"owners": [
    "76561199438881251",
    "76561198000000000"
]
```

To take it away, remove their ID. `"owners": ["*"]` gives it to everyone, and
`"owners": []` to nobody (it stays in the list, ready to give out again).

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
| `type` | `hat` (or `glasses` or `color`, see below). |
| `name` | What the hat grid shows. |
| `picture` | The picture's path in this repository. |
| `width` | The hat's width as a share of the slime's width (Christmas Hat 0.82, Traffic Cone 0.8, Propeller Cap 0.95). |
| `sink` | How much of the hat's height sits below the top of the head (0 = on top, 0.5 = half pulled down). |
| `shift` | How far it sits ahead of the eyes' middle, as a share of its own width (below 0 = towards the back). |
| `runTilt` | Degrees the hat leans while the slime runs: above 0 tips it back to follow the running body, below 0 tips it forward, 0 (or left out) keeps it level. Needs Bopl Cosmetics 1.2.2 or newer; older versions keep it level. |
| `runSink` | How much lower the hat sits while the slime runs, as a share of its height (the Christmas Hat uses 0.2). Used by Bopl Cosmetics 1.2.3; from 1.2.4 a leaning hat rests on the head by itself in every running frame, and `runSink` is only a fallback. Set it to a small number besides `runTilt` to switch the running pose on without a lean. |
| `owners` | Who can wear it: Steam IDs, or `"*"` for everyone. |

## Adding glasses

Glasses need Bopl Cosmetics 1.6.0 or newer; older versions skip them.

1. Put the picture in `glasses/`, for example `glasses/round.png`: a PNG with a see-through
   background, drawn on the slime standing and facing right (so the lens on the left is the near,
   bigger one), cut tightly around the glasses, at most 1024 pixels each way and 1 MB.
2. Find the two eye points: where the middle of the slime's back (left) eye and front (right) eye
   go in the picture, each as `[across, down]`, shares of the picture's width and height from its top
   left (0 to 1). The mod turns, sizes and moves the picture so these land on the eyes in every frame.
3. Add an item to `items` in `cosmetics.json`:

```json
{
    "id": "round",
    "type": "glasses",
    "name": "Round Glasses",
    "picture": "glasses/round.png",
    "backEye": [0.4096, 0.567],
    "frontEye": [0.8391, 0.3692],
    "owners": ["*"]
}
```

They're picked in the lobby's hat grid, after the hats, and worn besides a hat.

## Adding a colour (a flag, say)

Colours need Bopl Cosmetics 1.4.0 or newer; older versions skip them, and friends on those see the
player in their normal colour.

1. Put the picture in `colors/`, for example `colors/sweden.png`. It's stretched over the slime's
   body in every frame (left edge of the picture on the left of the body, top on top), so draw it
   the shape of a flag, for example 220 x 160 pixels. At most 1024 pixels each way and 1 MB.
   See-through parts show as white.
2. Add an item to `items` in `cosmetics.json`:

```json
{
    "id": "sweden",
    "type": "color",
    "name": "Sweden",
    "picture": "colors/sweden.png",
    "owners": ["*"]
}
```

| Field | What it does |
| --- | --- |
| `id` | A short name: small letters, digits and dashes, never changed once people wear it. Not `normal` or `rainbow` (built in), and `norway` only for Norway's owners item below. |
| `type` | `color`. |
| `name` | What the mod's log calls it. |
| `picture` | The picture's path in this repository. |
| `owners` | Who can wear it: Steam IDs, `"*"` for everyone, or `[]` for nobody. |
| `arrow` | Optional: the colour of the arrows shot from the bow, written `"#rrggbb"`, for example `"#0039a6"` (blue) or `"#ffffff"` (white). Without it they're the flag's main colour: the colour covering most of the picture, white left out. The bow itself always shows the whole flag. Needs Bopl Cosmetics 1.6.5 or newer; older versions ignore it. |

In the lobby, a colour is one more stop on the colour arrows after Rainbow (and Norway), for the
players who own it.

### Norway

Norway is drawn by the mod itself (from Bopl Cosmetics 1.5.0 it's personal too), so its item has no
picture, only its owners:

```json
{
    "id": "norway",
    "type": "color",
    "name": "Norway",
    "owners": ["76561199805191658"]
}
```

It can have an `arrow` colour too (without one, Norway's arrows are red). Without this item nobody has Norway. (Versions 1.3.0 to 1.4.1 give Norway to everyone and note in
their log that they don't understand this item; that's harmless.) The slime's outline, eyes and mouth stay as they are, and when it faces left
the picture is mirrored with it.

## Notes

- Only the owners can pick a hat or colour, and everyone else's game only shows it on its owners,
  so nobody can show off someone else's by editing their settings.
- Anyone can read this repository, including the owners' Steam IDs.
- GitHub can take a few minutes to serve a changed file, so a change may need a second game start.
- If the list has a mistake, the mod leaves out the broken item and says why in its log
  (`BepInEx\LogOutput.log`, lines starting with "Online cosmetics list").

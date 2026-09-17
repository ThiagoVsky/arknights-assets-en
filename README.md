# Arknights game assets, EN server

Game assets from Arknights, extracted from the **EN** game server. This repository is
generated and refreshed by machine; do not edit its contents by hand.

## What is here

Source: `every bundle on the EN game server that is not audio and not already text`.

Mirrors the game's own `dyn/` tree, so paths match the container names inside the bundles:

- `arts/`: operator art, avatars, map art and character portraits.
- `avg/`: story backgrounds, key visuals and animated key art.
- `chararts/` and `skinpack/`: operator and skin texture sets.
- `spritepack/` and `ui/`: interface sprites and panels.
- `charpack/`, `battle/`, `building/`, `cutin/`, `prefabs/`, `retro/`, `activity/`: mode specific art and prefabs.
- `raw/`: video files, kept as the original `.usm` because they are not Unity bundles.

Bundles whose only content is meshes, prefabs, shaders or materials are kept as the raw `.ab` file, so those paths contain `.ab` rather than `.png`.

## Format

PNG for textures and sprites, raw `.ab` for bundles with nothing extractable

Text and JSON are excluded on purpose: the gamedata, story and Lua dumps already live in ArknightsGameDataEN, so this repository holds only what that repository does not.

## Updating

`.github/workflows/update.yml` runs once a day. Incremental state lives in
`.state/en.json`, so only bundles that are new or whose hash changed are downloaded
and extracted again; a rerun with nothing new is a no-op.

Run it locally:

```bash
python -m pip install "arkprts[all]" lameenc
python tools/assets_sync.py --out . --state .state
python tools/assets_sync.py --verify --out .
```

`tools/assets_sync.py` in this repository is a self-contained copy whose default group is
`en`. The canonical copy lives in [ArknightsGameDataEN](https://github.com/ThiagoVsky/ArknightsGameDataEN) under
`tools/assets_sync.py`; the download uses
[arkprts](https://github.com/thesadru/arkprts) and the extraction uses
[UnityPy](https://github.com/K0lb3/UnityPy) with the LZ4AK decompressor that arkprts
registers in place of the LZHAM that UnityPy does not implement.


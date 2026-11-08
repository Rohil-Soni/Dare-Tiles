# Dare Tiles

A Halloween-themed AR party game for Android, built with Unity 6 and Vuforia Engine. Point your phone at one of the 18 Dare Tile posters and a random dare appears on it in AR. There are 5 levels with 20 dares each, getting harder as you go, and every dare has its own countdown timer.

## Requirements

- Unity **6000.3.23f1** with Android Build Support
- Vuforia Engine **11.4.4** (not in this repo, see below)
- An Android phone running Android 13 or newer

## Setup

1. Clone the repo and open it in Unity Hub.
2. **Add Vuforia.** The Vuforia package is 132 MB, over GitHub's file limit, so it isn't in the repo.
   Download `add-vuforia-package-11-4-4.unitypackage` from <https://developer.vuforia.com/downloads/sdk>,
   then in Unity go to **Assets → Import Package → Custom Package** and import it. Click **Update** if asked.
3. **Add your Vuforia license key.** Get a free Basic key from the Vuforia License Manager.
   Select **ARCamera** in any LEVEL scene → **Open Vuforia Engine configuration** → paste the key.
4. Switch to Android: **File → Build Profiles → Android → Switch Platform**.

## Build

- **DareTiles → 2. Build Android APK** writes `Builds/DareTiles.apk`.
- **DareTiles → 1. Build Scenes + Settings** regenerates every scene and the player settings. This overwrites manual scene edits.
- **DareTiles → Add Dare Cards To Image Targets** puts a dare image card on each poster target.
- **DareTiles → 3. Export iOS Xcode Project** exports for iPhone. This needs iOS Build Support, then a Mac with Xcode.

Vuforia does not run in the Linux editor's Play mode, so test on a phone.

## How it works

| Path | What it is |
|---|---|
| `Assets/StreamingAssets/Vuforia/Dare_Tiles.*` | Vuforia device database with the 18 poster targets |
| `Assets/Editor/Vuforia/ImageTargetTextures/Dare_Tiles/` | The poster images, for printing |
| `Assets/Resources/DARES/LEVEL 1-5/` | 20 dare images per level (`001`-`100`) |
| `Assets/Scenes/LEVEL 1-5` | AR scenes: ARCamera plus `Tile_1`…`Tile_20` Image Targets, each with a Dare card |
| `Assets/Scripts/DareTileSpawner.cs` | Shuffles the level's dares onto the posters and shows them while a poster is tracked |
| `Assets/Scripts/LevelHUD.cs` | Dare panel and countdown timer |
| `Assets/Scripts/DareData.cs` | Level info and the text of all 100 dares |
| `Assets/Editor/` | The builder, the dare-card tool and the import settings |

On the **DareTiles** object in each level, **Card Mode** switches between showing the dare as an image, as text, or both. **Show Status** turns the AR diagnostics line on or off.

Scene flow: START → INST → LEVELS → LEVEL 1-5 → END.

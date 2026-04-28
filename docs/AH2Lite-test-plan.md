# AH2 Lite integration and test plan

This branch currently contains the following Lite artifacts:

- `1080i/Home_Lite.xml`
- `1080i/Includes_Lite_Home.xml`
- `1080i/Includes_Lite_Widgets.xml`
- `docs/AH2Lite-runtime-refactor-notes.md`

## Goal

Run a Lite version of the skin without TMDbHelper and use Kodi-native library widget paths.

## Recommended integration path

### Option 1: Quick local swap for testing

1. Back up the current files.
2. Rename `1080i/Home.xml` to `1080i/Home_OLD.xml`.
3. Rename `1080i/Home_Lite.xml` to `1080i/Home.xml`.
4. In `1080i/Includes.xml`, add:

```xml
<include file="Includes_Lite_Home.xml" />
<include file="Includes_Lite_Widgets.xml" />
```

5. Reload the skin in Kodi.

### Option 2: Keep parallel Lite files during development

1. Keep the original files untouched.
2. Copy the Lite file contents into local experimental files.
3. Adjust include references locally until the Lite path is stable.
4. Once stable, replace the original files in a follow-up commit outside this constrained environment.

## Widget test cases

Test these native Kodi library widget paths:

- `videodb://recentlyaddedmovies/`
- `videodb://recentlyaddedepisodes/`
- `videodb://movies/titles/`
- `videodb://tvshows/titles/`

## Expected results

### Home
- Skin loads without TMDbHelper installed.
- Home menu appears.
- No call is made to `plugin.video.themoviedb.helper`.

### Widgets
- Poster widgets populate from local Kodi library content.
- Empty libraries should fail gracefully by showing no items.
- Navigation into widget rows should not require TMDbHelper properties.

### Visuals
- Backgrounds still render.
- Header furniture still renders.
- Fullscreen widget container uses `AH2Lite.WidgetContainer`.

## Known gaps

The original files still contain TMDbHelper runtime references. The Lite files are meant to be used as the new controller and include layer. Additional migration work is still needed if you want the original file names updated in-repo.

## Follow-up tasks

- Replace original `Home.xml` with Lite version
- Fold Lite include files into main include chain
- Rework skinshortcuts templates to prefer Lite widget content
- Add Kodi-native clearlogo, fanart, and rating fallbacks
- Remove remaining TMDbHelper references from legacy includes

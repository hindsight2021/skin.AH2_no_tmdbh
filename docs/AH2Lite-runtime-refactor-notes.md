# AH2 Lite runtime refactor notes

This repository branch removes the hard install dependency on `plugin.video.themoviedb.helper` from `addon.xml`.

The remaining work is a runtime refactor of the XML controller layer.

## Confirmed runtime references still requiring replacement

### `1080i/Home.xml`
Replace all of the following:

- `TMDbHelper.DisableRatings` -> `AH2Lite.DisableRatings`
- `TMDbHelper.EnableCrop` -> `AH2Lite.EnableCrop`
- `TMDbHelper.EnableBlur` -> `AH2Lite.EnableBlur`
- `TMDbHelper.DisableArtwork` -> `AH2Lite.DisableArtwork`
- `TMDbHelper.MonitorContainer` -> `AH2Lite.MonitorContainer`
- `TMDbHelper.HideView` -> `AH2Lite.HideView`
- `TMDbHelper.WidgetContainer` -> `AH2Lite.WidgetContainer`
- `TMDBHelper.WidgetContainer` -> `AH2Lite.WidgetContainer`

Remove these lines entirely:

- `RunScript(plugin.video.themoviedb.helper,kodi_setting=myvideos.selectaction,property=KodiSetting.DefaultSelectAction)`
- `<include>Defs_TMDbHelper_Loader</include>`

### `1080i/Includes_Home.xml`
Replace:

- `TMDbHelper.WidgetContainer` -> `AH2Lite.WidgetContainer`
- `TMDBHelper.WidgetContainer` -> `AH2Lite.WidgetContainer`

### `1080i/Includes_Widgets.xml`
Replace:

- `TMDbHelper.WidgetContainer` -> `AH2Lite.WidgetContainer`
- `TMDBHelper.WidgetContainer` -> `AH2Lite.WidgetContainer`

## Native Kodi widget direction

The Lite skin should prefer native Kodi paths such as:

```xml
<content target="videos">videodb://movies/titles/</content>
<content target="videos">videodb://tvshows/titles/</content>
<content target="videos">videodb://recentlyaddedmovies/</content>
<content target="videos">videodb://recentlyaddedepisodes/</content>
```

Avoid TMDbHelper plugin paths for widget population.

## Known limitation during this refactor

Direct updates to the larger existing XML files were blocked by the GitHub write layer in this environment. This note documents the exact required runtime changes so they remain committed to the branch alongside the dependency removal work.

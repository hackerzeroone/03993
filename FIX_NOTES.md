# Fix Notes

## Repository URL

Aniyomi's add-repo screen accepts a URL that matches:

```text
https://.../index.min.json
```

Do not use the GitHub web/tree URL. Use the raw file URL:

```text
https://raw.githubusercontent.com/hackerzeroone/aniyomi-extensions/main/index.min.json
```

## `begin -1, end 0, length 6818`

That error is not caused by the repo JSON. It comes from the PornHub extension source code. The original extractor does this:

```kotlin
scriptPart.subSequence(
    scriptPart.indexOf("var ra"),
    scriptPart.indexOf(";flashvars.mediaDefinitions.hls") + 1,
)
```

When PornHub's embed page no longer contains those old markers, both `indexOf` calls return `-1`, which becomes `begin -1, end 0`.

The PornHub APK in this prepared repo was rebuilt with a safer extractor that searches for `mediaDefinitions`, validates missing markers, and returns a clear error instead of slicing with `-1`.

## PornHub video 404

PornHub now blocks stream data from some `/embed/{viewkey}` pages. The `13.8` PornHub APK loads stream data from the normal `/view_video.php?viewkey=...` page, sends age/platform cookies, returns playback URLs with PornHub referer headers, and uses fallbacks similar to yt-dlp: `flashvars_*`, JS quality variables, `/video/get_media`, and direct download links.

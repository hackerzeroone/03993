# Fix Notes

## Repository URL

Aniyomi's add-repo screen accepts a URL that matches:

```text
https://.../index.min.json
```

Do not use the GitHub web/tree URL. Use the raw file URL:

```text
https://raw.githubusercontent.com/hackerzeroone/aniyomi-adult-extensions/main/index.min.json
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

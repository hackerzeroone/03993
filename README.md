# Aniyomi Adult Extensions

Use this URL in Aniyomi:

```text
https://raw.githubusercontent.com/hackerzeroone/aniyomi-extensions/main/index.min.json
```

This repository layout is the app-facing extension feed:

- `index.min.json` is the URL Aniyomi asks for when adding the repo.
- `repo.json` is the metadata Aniyomi reads while registering the repo.
- `apk/` contains the extension APKs.
- `icon/` contains the extension icons.

The bundled APKs are based on `Livid96/Aniyomi-Adult-Extensions`. The PornHub APK was rebuilt with a safer extractor and all APKs were re-signed with this repo key so Aniyomi can trust them from the same repository fingerprint.

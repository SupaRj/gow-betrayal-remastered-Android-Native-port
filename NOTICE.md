# Notices and attribution

This project is a from-scratch, behavioural re-implementation of
*God of War: Betrayal* (the 2007 J2ME/mobile Java game by Glu Mobile,
built by Metaflow), written by reading the original game's own decompiled
bytecode (see `betrayal/docs/`). It is not affiliated with, endorsed by, or
supported by Sony Interactive Entertainment, Santa Monica Studio, Glu
Mobile, Metaflow, or the game's original developers and publishers.

## Game assets and distribution

While the original PC project by samioan does not distribute the `.jar`, the Android version bundles the required assets directly within the APK for convenience. *God of War: Betrayal* (2007) is obsolete abandonware that is no longer commercially available or purchasable through any legal channel, and Sony has far bigger fish to fry than a retro J2ME phone game from nearly two decades ago. This project exists purely for video game preservation and mobile accessibility.

## Artwork and third-party code

The launcher's background and icon are the game's promo art, supplied by the
project owner (`betrayal/port/src/launcher/assets/banner_source.png`; the
`banner.png` and `gow.ico` files are generated from it by
`tools/make_banner.py` / `tools/make_icon.py`). `.github/social-preview.jpg`
is made from the same image. The "God of War" wordmark and Kratos in it
belong to their owners.

| Component | Licence | Where |
|---|---|---|
| `stb_image` | public domain / MIT | `betrayal/port/third_party/stb/` |
| `puff` (zlib's reference inflate) | zlib | `betrayal/port/third_party/puff/` |
| `javalang` (dev tool only, not shipped) | MIT | used by `tools/java2cpp.py` |
| Vineflower (dev tool only, not shipped) | Apache-2.0 | `tools/vineflower.jar` |

The launcher's file picker uses `IFileOpenDialog` (COM) and its update check
uses WinHTTP, both Windows system components. Release builds link the CRT
statically, so no Visual C++ redistributable is needed.

## Trademarks

"God of War" and "God of War: Betrayal" are trademarks of Sony Interactive
Entertainment LLC. All names are used here for identification and
documentation of the decompilation process only.

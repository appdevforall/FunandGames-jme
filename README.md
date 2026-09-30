# FunandGames (jME)

Three small Android game templates for [Code On The Go](https://github.com/appdevforall/CodeOnTheGo),
built with [jMonkeyEngine](https://jmonkeyengine.org/). Each one creates a complete, playable game
project that builds and runs on the device.

| Template | Language | Engine | Game |
|---|---|---|---|
| **Demo (jME)** | Java | jME 3.6.1 | 3D Earth you drag to spin, an orbiting rocket with an exhaust trail and bloom glow, a starfield, tap for points |
| **Tetris (jME)** | Kotlin | jME 3.9.0 | Falling-block puzzle: drag to move, drag down to drop faster, tap to rotate, long-press to hard-drop |
| **Bubble Wand (jME)** | Kotlin | jME 3.9.0 | First-person shooter: catch floating balloon animals in bubbles using an on-screen D-pad and FIRE button |

A libGDX version of the same three games lives in
[FunandGames-libGDX](https://github.com/appdevforall/FunandGames-libGDX).

## Install in Code On The Go

1. Download [`FunandGames-jme.cgt`](FunandGames-jme.cgt) to the device's /sdcard/Download folder.
2. Use the Add-ons Manager in Preferences to install it.
3. **Create a new project** → pick **Demo (jME)**, **Tetris (jME)** or **Bubble Wand (jME)** → name it → **Create**.
4. Wait for "Project initialized", then tap **Run**.

The first build downloads jME from Maven Central, so it needs an internet connection; later builds use Gradle's cache.

## Controls

| Game | Controls |
|---|---|
| Demo | Drag to rotate the Earth · flick to spin with inertia · tap for +10 points |
| Tetris | Drag left/right to move · drag down to soft-drop · tap to rotate · long-press to hard-drop |
| Bubble Wand | Left half: drag to walk · right half: drag to look, tap to shoot · or use the D-pad and **FIRE** · **HIDE UI** toggles the buttons |

A hardware keyboard also works (arrow keys, space, WASD).

## Repository layout

```
demo/  tetris/  bubblewand/     one Code On The Go template each
  template/template.json        name, description and parameters shown in the IDE
  app/src/main/java/PACKAGE_NAME/*.peb   game source
  gradle/libs.versions.toml.peb          dependency versions
cgt/                            the three templates plus templates.json, as packaged
FunandGames-jme.cgt             zip of cgt/ — the file you install
```

Files ending in `.peb` are [Pebble](https://pebbletemplates.io/) templates. Code On The Go fills in
`${{PACKAGE_NAME}}`, `${{APP_NAME}}`, `${{AGP_VERSION}}`, `${{KOTLIN_VERSION}}`, `${{COMPILE_SDK}}` and the
other tokens listed in each `template.json` when it creates a project.

## Notes for template authors

- **AGP and Kotlin versions come from the IDE** (`${{AGP_VERSION}}`, `${{KOTLIN_VERSION}}`), so the
  templates follow whatever toolchain the installed Code On The Go ships. Tested with AGP 9.3.1,
  Kotlin 2.3.21 and Gradle 9.6.1.
- **AGP 9 built-in Kotlin:** the Kotlin templates don't apply `org.jetbrains.kotlin.android` in the app
  module (AGP 9 rejects it); `jvmTarget` is set through `kotlin { compilerOptions { } }`.
- **Pebble drops the newline right after `}}`.** A token at the end of a line needs a trailing space
  (`compileSdk = ${{COMPILE_SDK}} `), or the next line gets joined onto it.
- **ABIs:** builds include `armeabi-v7a` and `arm64-v8a` only. That's every phone and tablet that runs Code
  On The Go, but not x86 emulators.

## Rebuilding the package

After changing a template, copy it into `cgt/` and re-zip:

```bash
(cd cgt && zip -qr -X ../FunandGames-jme.cgt .)
```

`cgt/templates.json` lists the template folders the package contains.

## Tested

All three templates were downloaded from this repo, installed, built, installed as apps and played on a
Samsung tablet (SM-X238U, Android 16) with Code On The Go 26.40.

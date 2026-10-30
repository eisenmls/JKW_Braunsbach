# Kulturweg Braunsbach

Android app for the Jüdischer Kulturweg Braunsbach. The app is a plain website in `www/`, wrapped with [Capacitor](https://capacitorjs.com).

## Folders

| Path | What it is |
|---|---|
| `www/index.html` | The whole website: text, styling and script |
| `www/images/`, `www/audio/` | Media used by the website |
| `www/fonts/` | Fonts, stored here so the app works offline |
| `android/` | Android project, normally no need to touch it |
| `capacitor.config.json` | App name, app ID and website folder |

## Editing the website

Double-click `www/index.html` to open it in a browser. Edit the file and press F5 to see the change.

New media files go in `www/images/` or `www/audio/`:

- Use lowercase names without spaces or umlauts, for example `station-07-08-mikwe.jpg`.
- Keep photos to about 1600 px on the long side.

Keep original full-size files outside this repo.

## One-time setup per computer

Needed only to build the app. Editing the website needs none of this.

1. Install [Node.js](https://nodejs.org) (version 22 or newer) and [Git](https://git-scm.com).
2. Install [Android Studio](https://developer.android.com/studio) with the default options. Open it once and let it finish downloading the SDK. It includes Java 25, so you don't need to install Java separately.

Then run these two commands in PowerShell:

```powershell
setx JAVA_HOME "C:\Program Files\Android\Android Studio\jbr"
setx ANDROID_HOME "$env:LOCALAPPDATA\Android\Sdk"
```

Finally, close VS Code and any terminals completely, then reopen them so they pick up the new settings.

## Building the app

Run this in the project folder:

```powershell
npm.cmd run apk
```

The first run takes a few minutes. The APK ends up at:

```
android\app\build\outputs\apk\debug\app-debug.apk
```

This is a debug build for testing. It can't be uploaded to Google Play.

Use `npm.cmd`, not `npm`, because PowerShell may block plain `npm`. In Command Prompt either one works.

## Testing on a phone

Turn on USB debugging on the phone and connect it by USB, then run:

```powershell
npm.cmd run phone
```

To debug the running app, open `chrome://inspect` in Chrome on the PC. This works on debug builds.

Always check new media in the real app too. Android treats upper and lower case in file names as different, and Windows doesn't.

## Versions

| Tool | Version |
|---|---|
| Java | 25 |
| Gradle | 9.8.2 |
| Android Gradle Plugin | 9.5.0 |
| Capacitor | 8.6.0 |
| Target Android | Android 17 (API 37) |
| Minimum Android | Android 7.0 (API 24) |

Capacitor 8 ships with Android Gradle Plugin 8.13. This project uses 9.5.0 instead, which Java 25 and API 37 need. `android/build.gradle` sets the version for the whole build, even though Capacitor's own files still list 8.13.

Java 25 is only used to run the build. The app's code still compiles at Java 21 level, because Capacitor sets that.

When Capacitor 9 is stable, upgrade with `npx cap migrate`.

## Signing keys

Never commit a signing key. `.gitignore` blocks `*.jks`, `*.keystore` and `key.properties`.

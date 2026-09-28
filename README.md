# Garcia Patcher

Patches the ALLfiring (v1.1.22) Android game package so it redirects network traffic to a local or custom Garcia server. It restores the game's startup class and aligns and cryptographically signs every APK inside the .xapk archive.

## 1. Prerequisites

[Download the latest APK](https://apkpure.com/allfiring/com.genmugame.prometheus/download)

Download the latest [Android CMD-Line Tools](https://developer.android.com/studio?utm_source=gemini#command-tools)
> [!CAUTION]
> If the link above doesn't work, visit the [official website](https://developer.android.com/studio?utm_source=gemini#command-tools) and scroll down to the **Command Line Tools** section.

## Build

```powershell
cargo build --release
```

The patcher reads XAPK/APK archives directly, so 7-Zip is
not required. By default it uses `keytool` from `PATH` and the newest Android
Build Tools under `%LOCALAPPDATA%\Android\Sdk\build-tools`.

## Configure

Edit `config.toml` before patching.

```toml
[endpoints]
host = "10.0.0.186"
game_port = 8888
sdk_port = 18889
hotpatch_port = 18888

[tools]
# zipalign = "C:/Android/Sdk/build-tools/35.0.0/zipalign.exe"
# apksigner = "C:/Android/Sdk/build-tools/35.0.0/apksigner.bat"
# keytool = "C:/Program Files/Java/jdk-23/bin/keytool.exe"
# keystore = "garcia-local.p12"
```

Uncomment tool paths only when the defaults do not work. Relative paths are
resolved from the directory containing the selected configuration file.

## Patch

```powershell
.\target\release\garcia-patcher.exe `
  "C:\path\ALLfiring_1.1.22_APKPure.xapk"
```

Use another configuration file or output path through the CLI:

```powershell
.\target\release\garcia-patcher.exe `
  "C:\path\ALLfiring_1.1.22_APKPure.xapk" `
  --config "C:\path\garcia.toml" `
  --output "C:\path\ALLfiring-garcia.xapk"
```

The output is written next to the input as
`ALLfiring_1.1.22_APKPure-garcia-10.0.0.186.xapk`. The reusable signing key is
stored under the platform data directory (`%LOCALAPPDATA%\GarciaPatcher` on
Windows). Set `tools.keystore` to choose another location.

The patched settings are:

```text
cdn=http://HOST:HOTPATCH_PORT/prod/en/Android
ipaddress=HOST:GAME_PORT
url=http://HOST:SDK_PORT
noticeURL=http://HOST:SDK_PORT
```

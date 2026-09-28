# Garcia Patcher

Patches the ALLfiring (v1.1.22) Android game package so it redirects network traffic to a local or custom Garcia server. It restores the game's startup class and aligns and cryptographically signs every APK inside the .xapk archive.

## 1. Prerequisites.

- Download the [Allfiring | Version 1.1.22 APK](https://apkpure.com/allfiring/com.genmugame.prometheus/download).
- Download the latest [Android CMD-Line Tools](https://developer.android.com/studio?utm_source=gemini#command-tools).
> [!CAUTION]
> If the link above doesn't work, visit the [official website](https://developer.android.com/studio?utm_source=gemini#command-tools) and scroll down to the **Command Line Tools** section.

- Download and Install [Adoptium Temurin 17](https://adoptium.net).
- Download the [Android Platform-Tools](https://developer.android.com/tools/releases/platform-tools).
- Download and Install [MuMu Player 12](https://www.mumuplayer.com). It's optional but I highly recommended for this guide.

## 2. Step by Step.

### 3. Patch the Game.

Before we start, we should patch the game first to make sure that it should work later.

- Download the [Allfiring | Version 1.1.22 APK](https://apkpure.com/allfiring/com.genmugame.prometheus/download).
- Download the Zip file by pressing the green color `<> code` and select "Download Zip". Once it's finished, put the files to the `C:\Users\[Username]\Documents\` or anywhere, make a new folder and rename it to whatever you want and extract all the files there.
- Now, download and install [MuMu Player 12](https://www.mumuplayer.com), we need this to use the USB DEBUGGING via Developer Mode from the emulator.

Now build the [Garcia-Patcher], we need it to patch the apk.
> [!WARNING]
> You need to download [RUST](https://rust-lang.org/tools/install/) Programming Language in order to use this command.

```text
cargo build --release
```

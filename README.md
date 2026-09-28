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

Now that we have already build the cargo, there should be a new folder called `\target\release\` and inside that there should be a `garcia-patcher.exe`.

After that wee need to modify `config.toml`, you can edit the config by right-click > Edit with Notepad or Notepad++. Inside, there should be a line of texts, for example:
```
[endpoints]
  host = "10.0.0.186"
  game_port = 8888
  sdk_port = 18889
  hotpatch_port = 18888
  
[tools]
  zipalign = "C:/Android/Sdk/build-tools/35.0.0/zipalign.exe"
  apksigner = "C:/Android/Sdk/build-tools/35.0.0/apksigner.bat"
  keytool = "C:/Program Files/Java/jdk-23/bin/keytool.exe"
  keystore = "garcia-local.p12"
```

Before we edit this, you need to use your Local LAN Address for the `host` for the emulator and the server to recognize the game's connection.
- Once you finished downloading MuMu Emulator 12, go to the Settings > About Phone > Build Number, and tap it 7 times until it prompts you that you have unlocked DEVELOPER MODE.
- Go to System > Developer Option and enable **USD DEBUGGING**
- Once that's done, close the emulator, we won't need it for now.

Lastly, we need that LAN Address, open your **Command Prompt** and type `ipconfig` and look at your `IPv4 Address` and copy the address. Head back to the `config.toml` and replace the `"10.0.0.186"` with your LAN Address.
> [!CAUTION]
> Do not remove the `" "` as they are needed.

Now, patch the game via this command.
```
.\target\release\garcia-patcher.exe "C:\Users\[username]\Downloads\ALLfiring_1.1.22_APKPure.xapk"
```

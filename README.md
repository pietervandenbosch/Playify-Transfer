# Playify Transfer
Transfers Spotify playlists to Google Play Music. It is an addition to Playify.

## Setup
### Before you start...
You need to allow "less secure apps" to access your account. You can enable this in your [account settings](https://myaccount.google.com/lesssecureapps).

If you have two-factor authentication enabled (which you should!), you need to create a password for "less secure apps". Go to the [App Passwords](https://myaccount.google.com/apppasswords) on your account settings. Click on "Select apps", choose "Other" and name it something you like - Playify would sound nice. It will output a new password you will need to use with Playify (your email stays the same).

### Windows (pre-built)
Download the [latest release (standalone version)](https://github.com/krmax44/playify-transfer/releases/latest) and unzip it. Firstly, open `password.exe` and set a password. **Without setting a password, the Transfer app will not start.** You will need the password later. Then open `playify-transfer.exe`.

Now open a playlist link. You can take [this one](https://open.spotify.com/user/spotifycharts/playlist/37i9dQZEVXbMDoHDwVN2tF) for testing. Click on the red transfer icon in the bottom right corner to begin the transfer progress.

Transfer needs to run everytime you need to transfer a playlist. If you wish it runs always by default, right-click `playify-transfer-invisible.exe` and select "Create shortcut". Press <kbd>Win + R</kbd>, type in `shell:startup` and press enter. A explorer window will open. Now copy the created shortcut into this folder, double click it and it will always be running.

### Linux, Mac OS and Windows
Windows users should prefer the pre-built way of installing. You can use this if you already have Python installed.

[Download Python 3](https://www.python.org/downloads/). Once downloaded and installed, download the [latest release (source code)](https://github.com/krmax44/playify-transfer/releases/latest) and unzip it. Open a terminal in the folder where the files are located and enter:
```
$ pip install gmusicapi
$ pip install websocket_server
$ python password.py
```

Now set a password.

```
$ python playify-transfer.py
```

Transfer should now be running and you can start moving playlists in Playify.

**This setup needs only to be done once.** When using Transfer again, just type `python playify-transfer.py`. 

## API documentation

All commands are sent in JSON format via WebSocket to `ws://localhost:5673`.

### listing playlists
```
{
  "q": "get_playlists",
  "auth": "your transfer password",
  "email": "your gmail address",
  "password": "your google password"
}
```
will return an array of objects with playlist names and ids.

### transfering playlists
```
{
  "q": "transfer_playlist",
  "auth": "your transfer password",
  "email": "your gmail address",
  "password": "your google password",
  "tracks": ["Sample Song - Sample Artist", "Sample Song - Sample Artist"],
  "new_playlist": true,
  "playlist": "new playlist name"
}
```
`new_playlist` can be true or false; if false, `playlist` must contain a playlist id.

### Donate

<a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VRGZY3DW4UALC"><img src="https://www.paypal.com/en_US/i/btn/btn_donateCC_LG.gif" align="right"></a>
If you're feeling generous, I would really appreciate a small donation to keep the extension in development! Thank you! <a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VRGZY3DW4UALC">Donate with PayPal</a>

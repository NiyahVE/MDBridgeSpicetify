# Spicetify Bridge

`Spicetify Bridge` is a Macro Deck 2 plugin that controls Spotify through Spicetify's `Spicetify.Player` API.

This project was also made heavily with the help of AI.

Pull requests are welcome.

The connection is now fixed and does not require any plugin-side configuration:

- WebSocket URL: `ws://127.0.0.1:8974/ws/`
- No token

## How it works

1. The Macro Deck plugin starts a local WebSocket server on `127.0.0.1:8974`.
2. The Spicetify extension in `spicetify-extension/macrodeck-bridge.js` connects to that server.
3. Macro Deck actions send commands to the extension.
4. The extension calls `Spicetify.Player.*` and sends player state updates back to Macro Deck.

## Requirements

- Macro Deck 2
- Spotify desktop app
- Spicetify installed and working

## Install the Macro Deck plugin

1. Build the plugin.
2. Copy the built plugin DLL and `ExtensionManifest.json` into your Macro Deck plugins folder.
3. Start or restart Macro Deck.
4. Enable the `Spicetify Bridge` plugin inside Macro Deck.

## Enable the Spicetify extension

Follow these steps exactly.

### 1. Locate your Spicetify extensions folder

Open a terminal and run:

```powershell
spicetify -c
```

This shows your Spicetify configuration path. From there, locate the `Extensions` folder used by Spicetify.

### 2. Copy the extension file

Copy this file from the repository:

- `spicetify-extension/macrodeck-bridge.js`

into your Spicetify `Extensions` folder.

The filename should stay:

- `macrodeck-bridge.js`

### 3. Register the extension with Spicetify

Run:

```powershell
spicetify config extensions macrodeck-bridge.js
```

If you already use other extensions, make sure this command does not unintentionally remove them from your existing Spicetify config. Add `macrodeck-bridge.js` alongside your other extension entries as needed.

### 4. Apply the Spicetify changes

Run:

```powershell
spicetify apply
```

### 5. Restart Spotify

Close Spotify completely, then open it again.

### 6. Verify the extension connects

Once Spotify and Macro Deck are both running and the plugin is enabled, `spicetify-extension/macrodeck-bridge.js` should connect automatically to:

- `ws://127.0.0.1:8974/ws/`

No token or port setup is required.

## Usage

After installation:

1. Add the plugin actions in Macro Deck.
2. Press a button such as play, pause, next, previous, mute, volume up/down, or play URI.
3. Macro Deck variables should update from Spotify state changes.

## Notes for development

- `Main.cs` hard-codes the WebSocket port to `8974`.
- `Bridge/SpiceWebSocketServer.cs` accepts local WebSocket connections without token authentication.
- `spicetify-extension/macrodeck-bridge.js` connects to the fixed local WebSocket URL.
- If your local Macro Deck SDK path differs, update `Directory.Build.props`.

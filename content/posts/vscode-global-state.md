---
title: "Exploring VS Code's Global State"
date: 2021-08-15T00:55:00-07:00
tags: ['vscode', 'mythic', 'malware']
categories: ['Red Teaming']
featuredImage: images/posts/vscode-global-state.png
draft: false
---

While working on the [Venus payload for Mythic C2](https://github.com/MythicAgents/venus), which is a cross-platform implant that installs as a [Visual Studio Code extension](https://code.visualstudio.com/api), I needed a way to record that the malware checked in with the C2 server. I wanted the payload to behave like a normal VS Code extension as much as possible, so I decided to use the built-in `globalState` key/value store.

The `globalState` or [Memento](https://code.visualstudio.com/api/references/vscode-api#Memento) API is very straightforward to use and consists mostly of `update()` calls to store and `get()` calls to retrieve data. But once I needed to inspect, update and clear out this state outside of the context of a running extension (or Venus payload), that's when I started to dig into how it's implemented. Here's what I learned.

## Global state database

VS Code stores the contents of `globalState` in a SQLite3 db under `~/Library/Application\ Support/Code/User/globalStorage/state.vscdb` and `state.vscdb.backup` on macOS.

Some extensions store files--even executables--under the `globalStorage` directory by accessing that location for writes/reads via `globalStorageUri`. Non-global or workspace-specific state and storage live under `~/Library/Application\ Support/Code/User/workspaceStorage` instead.

The global state database has a single table, `ItemTable`, which has a key/value schema:

```
sqlite> .schema ItemTable
CREATE TABLE ItemTable (key TEXT UNIQUE ON CONFLICT REPLACE, value BLOB);
```

## Resetting Venus payload state 

When an extension uses `globalState` like Venus does, it's all stored together as a JSON blob under a key like `<PUBLISHER>.<NAME>`, where `PUBLISHER` corresponds to the value under that key in `package.json` (the extension's publisher), and `NAME` is the extension's identifier.

For example, once Venus has checked in with Mythic C2 and saved its callback UUID, it's stored as the boring-sounding "productID" like this:

```
sqlite> SELECT * FROM ItemTable WHERE key = 'corp.venus';
corp.venus|{"productID":"c5b3ee3a-0ddb-4406-9a7e-f450d0e4563d"}
```

Once this is stored in VS Code's global state, Venus extension won't try to check in again. You can clear out this value and force the payload to check in by deleting the `corp.venus` record. The exact key will vary based on your extension's publisher and name/identifier that you chose when building the payload in Mythic.

```
sqlite> DELETE FROM ItemTable WHERE key = 'corp.venus';
```

This will force your Venus payload to check in again the next time it starts, which can be handy for development/testing.

## References

https://code.visualstudio.com/api/references/vscode-api#ExtensionContext.globalState  
https://code.visualstudio.com/api/references/vscode-api#Memento  
https://code.visualstudio.com/api/references/vscode-api#ExtensionContext.globalStorageUri  
https://code.visualstudio.com/api/references/vscode-api#FileSystem  

# EMGauntlet — Online multiplayer with Netcode for GameObjects

> Assignment for the *Multiplayer Environments* course · Game Design & Development, URJC · 2025/26

![Unity](https://img.shields.io/badge/Unity-6-black?logo=unity) ![Netcode](https://img.shields.io/badge/Netcode_for_GameObjects-blue) ![C#](https://img.shields.io/badge/C%23-purple?logo=csharp)

<!-- TODO Iván: add a GIF with two game windows (host + client) moving at the same time -->

## About

**EMGauntlet** is a top-down dungeon crawler inspired by *Gauntlet* (Atari, 1985), provided by the course as a **single-player base project**. The assignment was to turn it into an **online multiplayer** game using Unity's **Netcode for GameObjects**.

> The base game (procedural map, enemies, drops, UI) is the course's starting project. **The networking work is mine**, done on the `ivan` branch and merged in [PR #1](../../pull/1).

## My work — networking

- Added **Netcode for GameObjects** and set up the `NetworkManager`
- **Host / client connection** flow from the main menu, plus a small testing UI (`TestingNetcodeUI`)
- **Client-authoritative movement** with a custom `ClientNetworkTransform`
- **Synced character selection**: the server stores each client's chosen character, and its colour is replicated to everyone
- **Same procedural map for everyone**: the server picks a random seed and shares it through a `NetworkVariable`, so every client generates the identical castle
- **Server-side player spawning**: one networked player per connected client, with safe spawn offsets
- **Clean disconnects**: the server removes the player's data, and a client that loses the connection shuts down Netcode and returns to the main menu (`GameManager` as a `NetworkBehaviour`)

Files I changed most: `PlayerController.cs`, `GameManager.cs`, `LevelGenerator.cs`, `CharSelectionMenuButtonsHandler.cs`, `UniqueEntity.cs`.

## Running it

1. Open `EMGuantlet-main` with **Unity 6000.2.x**.
2. Build the game, run two copies (or use *Multiplayer Play Mode*), start one as **Host** and join with the other as **Client**.

---

The original README of the base project (in Spanish) is kept in [`EMGuantlet-main/README.md`](EMGuantlet-main/README.md).

# Minecraft Unity

A fully functional Minecraft clone built from scratch in **Unity 2022.1.12f1** using **C#**. Features procedural world generation, a block-based survival system, and real-time multiplayer via Steam lobbies.

---

## Preview

![Home](home.png)
![World](world.png)
![Crafting](crafting.png)
![Building](building.png)


---

## Features

- 🌍 **Procedural world generation** — terrain, biomes, caves, and trees generated using layered Perlin noise
- 🧱 **Block system** — fully modular block database with custom block types and textures
- 🧍 **Player controller** — movement, jumping, gravity, block placement and breaking
- 🎒 **Inventory & hotbar** — item management with a heads-up display
- 💾 **Auto-save** — player position and inventory saved automatically
- 🌐 **Multiplayer** — real-time co-op using Mirror networking and Steam lobbies
- 🔧 **Crafting system** *(in progress)* — Minecraft-style 3×3 crafting grid with recipe matching

---

## Built With

| Tool | Purpose |
|------|---------|
| Unity 2022.1.12f1 | Game engine |
| C# | Scripting language |
| Mirror | Multiplayer networking |
| Steamworks.NET | Steam integration (lobbies, identity) |
| KcpTransport | Low-latency networking transport |
| ProBuilder | In-editor level prototyping |
| TextMeshPro | UI text rendering |

---

## Requirements

- Unity **2022.1.12f1** (exact version recommended)
- Visual Studio 2019 or **2022** (with "Game development with Unity" workload)
- **Steam** installed and running (required for multiplayer and identity)
- Windows / Mac / Linux

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/AbdulVaasay/Minecraft-Unity.git
```

### 2. Open in Unity Hub

- Open **Unity Hub**
- Click **Open → Add project from disk**
- Select the cloned folder (the one containing `Assets/` and `ProjectSettings/`)

### 3. Let Unity import

On first open, Unity will reimport all assets. This may take 3–5 minutes — let it finish completely.

### 4. Open the main scene

In the **Project panel**, navigate to `Assets/Scenes/` and double-click `World.unity`.

### 5. Run the game

Make sure **Steam is open and you are logged in**, then press the ▶ **Play** button.

---

## How to Play

1. Press **▶ Play** in Unity
2. In the game window, click **Host (LAN)** to start a world as the server
3. Another player can join by clicking **Client** and entering the host's IP
4. Use **WASD** to move, **Space** to jump, **Left Click** to break blocks, **Right Click** to place blocks

---

## Project Structure

```
Assets/
├── _Scripts/
│   ├── Block/              # Block types, block data manager, helpers
│   ├── Entity's/           # Player controller, camera, HUD
│   ├── Menus/              # Main menu, lobby creation, world creation
│   ├── Networking/         # MinecraftNetworkManager, WorldServer, LobbyManager
│   ├── World/              # World.cs, Chunk, ChunkData, WorldRenderer
│   ├── WorldGeneration/    # TerrainGenerator, BiomeGenerator, DomainWarping, TreeGenerator
│   └── Crafting/           # CraftingRecipe, CraftingManager, CraftingUI (in progress)
├── Mirror/                 # Mirror networking library
├── Models/                 # 3D models
├── Plugins/                # Steamworks.NET
├── Prefabs/                # Chunk, player, UI prefabs
├── Resources/              # Block Data scriptable object
├── Scenes/                 # World scene
├── Shaders/                # Custom block rendering shaders
├── Sounds/                 # Sound effects
└── Textures/               # Block textures and atlases
```

---

## Architecture Overview

The project is divided into four main systems that work together:

```
Steam + Mirror
      ↓
MinecraftNetworkManager
      ↓
    GameManager
   ↙     ↓     ↘
World   Block   Player
Gen     System  System
   ↘     ↓     ↙
      World.cs
         ↓
     WorldServer
         ↓
   Playable Game
```

**World Generation** — `TerrainGenerator` uses layered Perlin noise and `BiomeGenerator` to procedurally create the terrain. `DomainWarping` adds natural randomness and `TreeGenerator` places trees.

**Block System** — `BlockDataManager` holds the database of all block types. `ChunkData` stores raw block positions, `Chunk` manages 16×16 world sections, and `WorldRenderer` converts block data into visible 3D meshes.

**Player System** — `Player.cs` handles movement and physics. `PlayerCanvas` manages the hotbar and HUD. `AutoSave` persists the player's state between sessions.

**Networking** — `MinecraftNetworkManager` coordinates connections using Mirror. `LobbyManager` interfaces with Steam for lobby creation and joining. `WorldServer` syncs the world state across all connected players.

---

## Known Issues & Fixes

### Steam not initialized error
Steam must be **open and logged in** before pressing Play. If you see a `NullReferenceException` related to `SteamClient`, make sure Steam is running.

### Burst compiler error on first open
Delete the `Library/` folder in the project root and reopen the project. Unity will rebuild it fresh.

### Package resolution error
Go to **Window → Package Manager**, switch to **Unity Registry**, search for **Burst**, and update it to the latest version.

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "Add my feature"`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## License

This project is open source and available under the [MIT License](LICENSE).

---

## Acknowledgements

- [Mirror Networking](https://mirror-networking.com/) — open source multiplayer framework
- [Steamworks.NET](https://steamworks.github.io/) — C# wrapper for the Steamworks API
- Minecraft by Mojang — original game concept and inspiration

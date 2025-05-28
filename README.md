# MyProject2 - Thief Simulator

This project has been transformed from a basic FPS template into a **Thief Simulator** game with stealth mechanics, inventory management, and AI guards.

## Features

### 🥷 Stealth System
- **Dynamic Stealth Levels**: Your visibility changes based on movement
  - **Crouching**: Most stealthy (0.1 stealth level)
  - **Walking**: Moderate stealth (0.3 stealth level)  
  - **Running**: Highly visible (0.8 stealth level)
  - **Standing Still**: Slightly more stealthy than walking

- **Noise System**: Movement generates noise that can alert guards
  - **Crouching**: Very quiet (0.1 noise level)
  - **Walking**: Low noise (0.2 noise level)
  - **Running**: High noise (0.7 noise level)

- **Detection Feedback**: Visual and audio cues when detected by guards

### 🎒 Inventory System
- **Weight-Based Carrying Capacity**: Maximum 50kg carrying capacity
- **Item Values**: Each stolen item has a monetary value
- **Real-time Inventory Tracking**: See item count, total value, and weight
- **Inventory Full Protection**: Cannot pick up items if over weight limit

### 💎 Stealable Items
- **Interactive Objects**: Approach items to see steal prompts
- **Timed Stealing**: Hold E to steal items (2-second default)
- **Progress Tracking**: Visual progress bar during stealing
- **Item Variety**: Different items with varying weights and values

### 🛡️ Guard AI System
- **Four AI States**:
  - **Patrolling**: Guards follow preset patrol routes
  - **Investigating**: Moving to investigate suspicious sounds
  - **Chasing**: Actively pursuing detected player
  - **Searching**: Looking for player after losing sight

- **Detection Mechanics**:
  - **Field of View**: 90-degree vision cone
  - **Detection Range**: 800 units
  - **Line of Sight**: Guards can't see through walls
  - **Stealth-Based Detection**: Lower stealth = higher detection chance

- **Patrol System**: Set custom patrol points for each guard

### 🎮 Controls
- **WASD**: Movement
- **Mouse**: Look around
- **Ctrl**: Crouch (increases stealth, reduces noise)
- **Shift**: Run (decreases stealth, increases noise)
- **E**: Steal nearby items (hold to complete)
- **Space**: Jump

### 📊 HUD Elements
- **Stealth Meter**: Shows current stealth effectiveness (top-left)
- **Detection Status**: Red "DETECTED!" warning when spotted
- **Inventory Info**: Item count, total value, weight capacity (top-right)
- **Control Hints**: Basic controls displayed at bottom

## Getting Started

### Setting Up the Game

1. **Compile the Project**: Build the C++ code in Visual Studio or using Unreal Build Tool
2. **Open in Unreal Editor**: Launch the project in Unreal Engine 5.4+
3. **Create a Level**: Set up a basic level with floors, walls, and hiding spots

### Adding Stealable Items

1. **Place Stealable Items**: 
   - Add `AMyProject2StealableItem` actors to your level
   - Set the `ItemData` properties (name, value, weight, description)
   - Adjust `StealTime` for different difficulty levels
   - Assign a static mesh for visual representation

2. **Configure Item Properties**:
   ```cpp
   ItemData.ItemName = "Golden Watch";
   ItemData.Value = 500;
   ItemData.Weight = 0.5f;
   ItemData.Description = "An expensive timepiece";
   StealTime = 3.0f; // 3 seconds to steal
   ```

### Setting Up Guards

1. **Place Guard Actors**:
   - Add `AMyProject2Guard` actors to your level
   - Set patrol points in the `PatrolPoints` array
   - Adjust detection parameters (`DetectionRange`, `FOVAngle`)
   - Configure movement speeds (`PatrolSpeed`, `ChaseSpeed`)

2. **Configure Guard Behavior**:
   ```cpp
   DetectionRange = 800.0f;    // How far guards can see
   FOVAngle = 90.0f;          // Field of view in degrees
   SearchDuration = 10.0f;     // How long to search after losing player
   PatrolSpeed = 150.0f;       // Walking speed
   ChaseSpeed = 400.0f;        // Running speed when chasing
   ```

### Customizing the Player

The player character (`AMyProject2Character`) includes:
- **Stealth Component**: Manages visibility and noise
- **Inventory Component**: Handles stolen items and weight
- **Movement Modifiers**: Crouching and running affect stealth

## Code Architecture

### Core Components

1. **UMyProject2StealthComponent**: Handles stealth mechanics and detection
2. **UMyProject2InventoryComponent**: Manages stolen items and carrying capacity
3. **AMyProject2StealableItem**: Interactive objects that can be stolen
4. **AMyProject2Guard**: AI guards with patrol and detection behavior
5. **AMyProject2ThiefHUD**: UI display for stealth and inventory information

### Key Systems

- **Event-Driven Design**: Components communicate through delegates
- **Modular Architecture**: Each system is self-contained and reusable
- **Blueprint Integration**: All components expose Blueprint-callable functions
- **Debug Visualization**: Guards show detection ranges and FOV in-game

## Tips for Level Design

1. **Create Hiding Spots**: Use walls, furniture, and shadows for cover
2. **Plan Patrol Routes**: Set logical patrol points that create gameplay opportunities
3. **Balance Item Placement**: Put valuable items in risky locations
4. **Lighting Considerations**: Darker areas should provide better stealth opportunities
5. **Multiple Paths**: Give players different routes to objectives

## Future Enhancements

Potential additions to expand the thief simulator:
- **Light/Shadow System**: Dynamic stealth based on lighting
- **Sound Propagation**: More realistic noise detection
- **Alarm Systems**: Triggered security responses
- **Multiple Floors**: Vertical level design with stairs/elevators
- **Lockpicking Mini-game**: Interactive stealing mechanics
- **Fence System**: Sell stolen goods for money
- **Mission Objectives**: Specific targets and goals

## Troubleshooting

### Common Issues

1. **Compilation Errors**: Ensure all header includes are correct
2. **Missing Components**: Check that components are properly created in constructors
3. **Input Not Working**: Verify Enhanced Input Actions are set up in Blueprint
4. **Guards Not Detecting**: Check patrol points and detection settings
5. **Items Not Stealable**: Ensure collision components are properly configured

### Debug Features

- **Guard Vision Cones**: Red circles and yellow lines show detection areas
- **On-Screen Messages**: Debug text shows stealth status and item interactions
- **Console Commands**: Use for testing and debugging

---

**Have fun being a master thief!** 🥷💰 

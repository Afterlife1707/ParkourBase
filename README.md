# ParkourBase

A modular parkour system for Unreal Engine 5, part of a vertical slices project. This open-source system provides smooth, responsive parkour mechanics through independent, reusable components. This system is part of a larger vertical slices project. Each slice focuses on a specific game mechanic, with the parkour system being the first implementation.

## Overview

ParkourBase implements a comprehensive parkour system by breaking down complex movement mechanics into modular components that can be easily mixed, matched, and extended. Each component handles a specific parkour action while maintaining independence from others, allowing for flexible gameplay design. The project contains a small parkour map ready for playtesting, using engine assets.

## Features

### Core Movement Components

<img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/5f1fe8c9-db5c-4010-85fb-16146f5884ca" />
                                                 
- **Sprint Component** - Custom sprint functionalities with cooldown
- **Slide Component** - Ground sliding with momentum preservation based on timer and slope(used in accordance with the Slope Component to detect slopes)
- **Landing Component** - Fall detection and landing animations based on height
- **Vault/Mantle Component** - Obstacle traversal for low and high obstacles, can also climb ledges
- **Wall Run Component** - Vertical wall running with camera tilting and its own jump function
- **Grappling Hook Component** - Simple grappling gun with a cable component

<img width="720" height="500" alt="image" src="https://github.com/user-attachments/assets/c881f2bd-790b-4f40-a218-92b2f819aef6" />

(LedgeSwingComponent is incomplete as of this commit)

### Enhanced Jump System
- **Coyote Time** - Grace period for jumping after leaving platforms
- **Sprint Boost** - Forward momentum boost when jumping while sprinting
- **Context-Aware Jumping** - Different jump behaviours based on current state

## Architecture

### Component-Based Design
All parkour mechanics inherit from `UParkourComponentBase`. This base class provides standardized access to the character and movement component. There is no dependency of the components on each other, as each of them are called through the character and they do not need to know about each other. There is also a custom log class.

### Input Flow
**Controller Input → Character Class → Individual Components → Movement Execution**

### Installation
1. Clone this repository into your UE5 project's Source folder
2. Regenerate project files
3. Compile the project
4. AVSlicesCharacter is the character class being used, which is the base type of the "OwnerCharacter" variable used in the components
5. AVSlicesController is the controller class handling the enhanced action inputs

## Usage

### Basic Movement
The system provides intuitive functions for each parkour action:
- **Sprint**: Start and stop enhanced running speed
- **Slide**: Initiate ground sliding with momentum preservation
- **Grappling**: Fire grappling hook for traversal
- **Jumping**: Context-aware jumping that handles wall-runs, and vault/mantle attempts

### Component States
Each component provides getter functions to check current states:
- Check if character is currently sprinting
- Determine if sliding is active
- Get current slope information for movement restrictions
- Access wall-running status and camera tilt data
- Each component exposes blueprint-configurable parameters

### Animations and Audio Setup 
- All the animations are from Mixamo. Some of them are reused and combined using animation composite.
- In some animations, there is a custom notifier, which takes control of the camera pawn rotation, so the camera moves with the animation(like landing)
- There is audio on the animations available, which are reused quite a lot, so they may not sound great. They're all implemented using notifiers.
- The animation blueprint for the character is ABP_Character, which is the default ABP_Manny extended with custom logic

<img width="720" height="500" alt="image" src="https://github.com/user-attachments/assets/3c2898db-db25-4282-a90e-80c25196117e" />

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/647c9fd4-2b3b-495b-8cd6-b7cf9002d487" />


## Acknowledgments

- Mixamo for character animations
- Pixabay and Youtube for Royalty free sound effects
- https://www.youtube.com/watch?v=z4LdRAMaifY&ab_channel=UnrealAxis
- https://www.youtube.com/watch?v=zF7z-xrFABY&t=1126s&ab_channel=LocoDev
- https://www.youtube.com/watch?v=z4LdRAMaifY&t=516s&ab_channel=UnrealAxis
- Cartoon Grappling Hook" (https://skfb.ly/6UNYo) by Matt LeMoine is licensed under Creative Commons Attribution (http://creativecommons.org/licenses/by/4.0/)

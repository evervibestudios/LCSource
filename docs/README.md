# Last Chaos Source Code

## Project Overview

Last Chaos is a massively multiplayer online role-playing game (MMORPG) that was originally developed by T&E Soft. This repository contains the complete source code for both the client and server components of the game, making it a comprehensive game development resource for the Last Chaos community.

## Purpose

This source code was made available to help preserve and continue the development of Last Chaos, allowing the community to:
- Maintain and operate private servers
- Fix bugs and improve game stability
- Add new features and content
- Learn from a complete MMORPG implementation
- Contribute to the ongoing development of the game

## Origin and History

Last Chaos was originally a commercial MMORPG that featured:
- Fantasy-themed gameplay with multiple character classes
- Guild systems and player-versus-player combat
- Crafting and trading systems
- Dungeon and raid content
- Pet and mount systems

The source code represents a mature game engine with years of development and optimization for handling thousands of concurrent players.

## Technologies Used

### Core Languages
- **C/C++**: Primary development language for both client and server (5,400+ source files)
- **Lua**: Scripting support for game logic and configuration
- **SQL**: Database queries and schema definitions

### Key Technologies
- **MySQL**: Primary database system for character, game, and account data
- **Custom Networking**: Proprietary network protocol implementation
- **Visual Studio**: Primary development environment for Windows builds
- **zlib**: Compression library for data handling
- **DirectX/OpenGL**: Graphics rendering (client-side)

### Build Systems
- Visual Studio Solutions (.sln, .vcproj, .vcxproj)
- GNU Makefiles for Linux server builds
- Platform-specific build configurations

## Current State

### Maintenance Status
- **Community Maintained**: This is now a community-driven project
- **Legacy Codebase**: Contains mature but older C++ patterns and practices
- **Active Development**: Ongoing improvements and bug fixes by community contributors
- **Cross-Platform**: Server components support both Windows and Linux

### Known Characteristics
- Production-ready server architecture that handled commercial traffic
- Comprehensive game systems implementation
- Well-structured separation between client and server components
- Extensive configuration and customization options
- Multiple language and region support

## Repository Structure

- **`Client Source/`**: Complete game client implementation
- **`Server Source/`**: All server-side components and services
- **`docs/`**: Project documentation (this folder)

## Getting Started

For detailed information about the project architecture, building, and contributing, please refer to:

- [Architecture Overview](ARCHITECTURE.md)
- [Security Considerations](SECURITY.md)
- [Contributing Guidelines](CONTRIBUTING.md)

## Community

This source code is maintained by the Last Chaos community. Contributions are welcome to help improve the game, fix issues, and add new features while preserving the original game experience.

## License

This source code is provided for educational and community development purposes. Please respect any applicable licensing terms and the intellectual property rights of the original developers.
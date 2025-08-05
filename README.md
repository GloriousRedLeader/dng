# Ultima Online Development Environment

This repository contains a complete Ultima Online development setup with both client and server components.

## Structure

- `ClassicUO/` - Open source UO client (submodule)
- `ServUO/` - Open source UO server emulator (submodule)  
- `uo-data/` - Shared game data files

## Getting Started

### Prerequisites
- **.NET SDK 9.0 or later** (required for ClassicUO client)
- **.NET SDK 7.0 or later** (minimum for ServUO server)
- **Mono** (for running ServUO on macOS/Linux)
- **Visual Studio Code** (recommended) or Visual Studio
- **make** (for using ServUO build scripts)

### macOS Setup
1. Install Homebrew (if not already installed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Install required dependencies:
   ```bash
   brew install dotnet mono make
   ```

3. Clone this repository with submodules:
   ```bash
   git clone --recursive <your-repo-url>
   ```

4. Initialize submodules (if not cloned recursively):
   ```bash
   git submodule update --init --recursive
   ```

### Setup

### Building

#### ClassicUO (Client)

**Prerequisites:**
- .NET SDK 9.0 or later (ClassicUO requires .NET 9.0)
- Git submodules must be initialized

**Install .NET SDK 9.0:**
```bash
# macOS (using Homebrew)
brew install --cask dotnet-sdk

# Verify installation
dotnet --version  # Should show 9.0.x or later
```

**Initialize Submodules:**
ClassicUO requires external dependencies (FNA framework, etc.) that are included as git submodules:

```bash
cd ClassicUO
git submodule update --init --recursive
```

**Build the Client:**
```bash
cd ClassicUO/scripts
bash build-naot.sh
```

The build process will:
1. Build the Bootstrap project
2. Build the main Client project with Native AOT compilation
3. Copy platform-specific dependencies (macOS libraries for Metal/OpenGL)
4. Generate optimized native binaries

**Output:** Built client files will be in `ClassicUO/bin/dist/`

**Build Time:** Expect 30-60 seconds for a full build (Native AOT compilation takes time)

#### ServUO (Server)
**Windows:**
```bash
cd ServUO
_winrelease.bat
```

**macOS/Linux:**
```bash
cd ServUO
make -f _makedebug build    # For development/debug build
# OR
make -f _makerelease build  # For production/release build
```

## Running the Server

### macOS Instructions

1. **Build the server** (development mode):
   ```bash
   cd ServUO
   make -f _makedebug build
   ```

2. **Configure the data path** (already configured to use `uo-data/`):
   The server is pre-configured to look for UO game data files in the `uo-data/` directory.

3. **Run the server**:
   ```bash
   mono ServUO.exe -debug
   ```

4. **Stop the server**:
   - Use `Ctrl+C` in the terminal
   - If that doesn't work, find the process and kill it:
     ```bash
     ps aux | grep mono
     kill <process-id>
     ```

### Visual Studio Code

You can also build and run from VS Code:

1. **Open the ServUO folder** in VS Code
2. **Build**: Use `Cmd+Shift+P` → "Tasks: Run Task" → "build debug"
3. **Run**: The launch configuration is set up to run with Mono

**Note**: ServUO targets .NET Framework 4.8, which requires Mono runtime on macOS/Linux.

## Running the Client

### macOS Instructions

1. **Build the client** (if not already done):
   ```bash
   cd ClassicUO/scripts
   bash build-naot.sh
   ```

2. **Run the client**:
   ```bash
   cd ClassicUO
   ./ClassicUO -UODataDir /Users/Arthur.Olliff/dng/uo-data/ -Server 127.0.0.1 -Port 2593
   ```

This will launch the client with your UO data directory and connect to the local server.

**Note**: ClassicUO is a native client that supports multiple graphics APIs on macOS (Metal, OpenGL, MoltenVK).

## Troubleshooting

### ClassicUO Build Issues

**"Microsoft.Xna" namespace errors:**
- Make sure git submodules are initialized: `git submodule update --init --recursive`
- The FNA framework (in `external/FNA`) provides the XNA compatibility layer

**".NET SDK version" errors:**
- ClassicUO requires .NET 9.0 or later
- Check version: `dotnet --version`
- Update if needed: `brew install --cask dotnet-sdk`

**Missing dependencies:**
- Ensure you're in the `ClassicUO/scripts` directory when building
- Try cleaning and rebuilding: `dotnet clean` then `bash build-naot.sh`

### ServUO Issues

**"ServUO.exe not found":**
- Make sure you built the server first: `make -f _makedebug build`
- Check that Mono is installed: `mono --version`

**Data path errors:**
- Verify `ServUO/Config/DataPath.cfg` points to the correct `uo-data/` directory
- Ensure UO data files exist in the `uo-data/` directory

## Configuration

1. Configure ServUO server settings in `ServUO/Config/Server.cfg`
2. Configure ClassicUO client settings as needed

## Development Workflow

This project uses **forked submodules** to allow custom modifications while staying current with official updates.

### Making Changes (Stored in YOUR repositories)

#### For ClassicUO modifications:
```bash
# Navigate to ClassicUO
cd ClassicUO

# Make your changes to files...
# Edit, add, or modify any files as needed

# Commit your changes
git add .
git commit -m "My custom ClassicUO feature"
git push origin main  # Pushes to YOUR fork (GloriousRedLeader/ClassicUO)

# Update parent repo to track your changes
cd ..
git add ClassicUO
git commit -m "Update ClassicUO with custom changes"
git push origin main
```

#### For ServUO modifications:
```bash
# Navigate to ServUO
cd ServUO

# Make your changes to files...
# Edit, add, or modify any files as needed

# Commit your changes
git add .
git commit -m "My custom ServUO feature"
git push origin master  # Pushes to YOUR fork (GloriousRedLeader/ServUO)

# Update parent repo to track your changes
cd ..
git add ServUO
git commit -m "Update ServUO with custom changes"
git push origin main
```

### Pulling Latest Updates from Official Repositories

#### Update ClassicUO from official repository:
```bash
cd ClassicUO
git fetch upstream                # Get latest from official ClassicUO
git merge upstream/main           # Merge official updates with your changes
git push origin main              # Push merged version to your fork
cd ..
git add ClassicUO
git commit -m "Update ClassicUO with latest official changes"
```

#### Update ServUO from official repository:
```bash
cd ServUO
git fetch upstream                # Get latest from official ServUO
git merge upstream/master         # Merge official updates (ServUO uses 'master')
git push origin master            # Push merged version to your fork
cd ..
git add ServUO
git commit -m "Update ServUO with latest official changes"
```

### Repository Structure

- **Your changes** are stored in your personal forks:
  - `GloriousRedLeader/ClassicUO` (your ClassicUO fork)
  - `GloriousRedLeader/ServUO` (your ServUO fork)
- **Official updates** come from upstream repositories:
  - `ClassicUO/ClassicUO` (official ClassicUO)
  - `ServUO/ServUO` (official ServUO)
- **This parent repository** tracks which versions of your forks to use

### Remotes Configuration

Each submodule has two remotes configured:
- `origin`: Your personal fork (where you push changes)
- `upstream`: Official repository (where you pull updates)

## Contributing

This is a personal development environment with forked submodules. 

**Official repositories:**
- ClassicUO: https://github.com/ClassicUO/ClassicUO
- ServUO: https://github.com/ServUO/ServUO

**Personal forks:**
- ClassicUO: https://github.com/GloriousRedLeader/ClassicUO
- ServUO: https://github.com/GloriousRedLeader/ServUO

## License

See individual component licenses in their respective directories.

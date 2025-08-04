# Ultima Online Development Environment

This repository contains a complete Ultima Online development setup with both client and server components.

## Structure

- `ClassicUO/` - Open source UO client (submodule)
- `ServUO/` - Open source UO server emulator (submodule)  
- `UO_7_0_102_3/` - Shared game data files

## Getting Started

### Prerequisites
- .NET SDK
- Visual Studio Code or Visual Studio

### Setup
1. Clone this repository with submodules:
   ```bash
   git clone --recursive <your-repo-url>
   ```

2. Initialize submodules (if not cloned recursively):
   ```bash
   git submodule update --init --recursive
   ```

### Building

#### ClassicUO (Client)
```bash
cd ClassicUO/scripts
bash build-naot.sh
```

#### ServUO (Server)
**Windows:**
```bash
cd ServUO
_winrelease.bat
```

**macOS/Linux:**
```bash
cd ServUO
./_makerelease
```

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

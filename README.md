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

## Contributing

This is a personal development environment. The official repositories are:
- ClassicUO: https://github.com/ClassicUO/ClassicUO
- ServUO: https://github.com/ServUO/ServUO

## License

See individual component licenses in their respective directories.

# i3_session

A simple Ruby script that saves and restores your window layout to the respective monitors when they are unplugged or plugged back in.

**Note:** The "watch" mode only works per session. If you log out or power off your machine, the script will not automatically restore the latest state when you log back in.

## Requirements

- Ruby
- i3 window manager
- xrandr (for monitor management)

## Installation

1. Make the script executable:
```bash
chmod +x i3_session
```

2. Optionally:
```bash
sudo cp i3_session ~/./local/bin/
```

## I3 Usage

Add to i3 config:
```
exec_always ~/.local/bin/i3_session -w &
```

### Modes

The script will try to active the mode `i3_session_multi_monitor`.

## Manual Usage

### Save Current Session
```bash
./i3_session --save
```
Saves your current window layout and monitor configuration.

### Restore Session
```bash
./i3_session --restore
```
Restores the previously saved session.

### Watch Mode (Auto-manage)
```bash
./i3_session --watch
```
Automatically saves and restores sessions when monitors are connected/disconnected.

### Help
```bash
./i3_session --help
```

## Development

```bash
DEBUG=1 ./i3_session -w
```

## How It Works

The script saves:
- Window positions and workspaces
- Monitor configurations and layouts
- Session data to `~/.config/i3/i3_session.json`

Perfect for laptop users who frequently connect/disconnect external monitors!

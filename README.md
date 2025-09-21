# i3_rewind

A simple Ruby script that restores windows and workspaces to their respective monitors when they are disconnected and reconnected.

**Note:** The "watch" mode only works per session. If you log out or power off your machine, the script will not automatically restore the latest state when you log back in.

## Requirements

- Ruby
- i3 window manager
- xrandr (for monitor management)

## Installation

1. Make the script executable:
```bash
chmod +x i3_rewind
```

2. Optionally:
```bash
sudo cp i3_rewind ~/./local/bin/
```

## I3 Usage

Add to i3 config:

```bash
exec_always ~/.local/bin/i3_rewind -w &
```

## My way of use

Create file at ~/.config/i3/i3_rewind_script.sh

```bash
#!/bin/bash

case "$I3_REWIND_TRANSITION" in
    to_multi_monitor)
        i3-msg mode "i3_rewind_multi_monitor"
        ;;
    to_primary_monitor)
        i3-msg mode "default"
        ;;
esac
```

Add to i3 config:

```bash
exec_always ~/.local/bin/i3_rewind -w -t ~/.config/i3/i3_rewind_script.sh &
```

## Modes

The script will try to active the mode `i3_rewind_multi_monitor`.

### Watch Mode (Auto-manage)
```bash
./i3_rewind --watch
```
Automatically saves and restores sessions when monitors are connected/disconnected.

### Manual Usage

#### Save Current Session
```bash
./i3_rewind --save
```
Saves your current window layout and monitor configuration.

#### Restore Session
```bash
./i3_rewind --restore
```
Restores the previously saved session.


### Help
```bash
./i3_rewind --help
```

## Development

```bash
DEBUG=1 ./i3_rewind -w
```

## How It Works

The script saves:
- Window positions and workspaces
- Monitor configurations and layouts
- Session data to `~/.config/i3/i3_rewind.json`

Perfect for laptop users who frequently connect/disconnect external monitors!

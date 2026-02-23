# omarchy-caps-lock-fix
A fix for omarchy caps lock delay.

## Step 1
Type in your terminal: sudo nvim /usr/share/X11/xkb/symbols/capslock

## Step 2
Search for ctrl_modifier and erase it. Add this instead:
hidden partial modifier_keys
xkb_symbols "ctrl_modifier" {
    key <CAPS> {
        type="ALPHABETIC",
        repeat=No,
        symbols[Group1] = [ Caps_Lock, Caps_Lock ],
        actions[Group1] = [ LockMods(modifiers=Lock), LockMods(modifiers=Shift+Lock,affect=unlock) ]
    };
};

## Step 3
Type in your terminal: sudo rm -rf /var/lib/xkb/*

## Step 4
Go to hyprland.conf and add this: kb_options = caps:ctrl_modifier

## Step 5
Restart Omarchy.

## Bonus: Some Configs for Omarchy
### KeyBindings
```
bindd = SUPER SHIFT, S, Screenshot de Região, exec, ~/.local/share/omarchy/bin/omarchy-cmd-screenshot smart clipboard
```
### Monitors
App: nwg-displays
### Hyprland.conf
```
misc {
	vfr = false
}
cursor {
    no_hardware_cursors = true
}
```
### Input.conf
```
# Control your input devices
# See https://wiki.hypr.land/Configuring/Variables/#input
input {
  # Use multiple keyboard layouts and switch between them with Left Alt + Right Alt
  # kb_layout = us,dk,eu
  kb_layout = us
  kb_variant = intl
  kb_options = caps:ctrl_modifier# ,grp:alts_toggle

  # Change speed of keyboard repeat
  repeat_rate = 40
  repeat_delay = 600

  accel_profile = flat
  force_no_accel = true
  # Start with numlock on by default
  numlock_by_default = true

  # Increase sensitivity for mouse/trackpad (default: 0)
  # sensitivity = 0.35

  touchpad {
    # Use natural (inverse) scrolling
    natural_scroll = true

    # Use two-finger clicks for right-click instead of lower-right corner
    # clickfinger_behavior = true

    # Control the speed of your scrolling
    scroll_factor = 0.4

    # Enable the touchpad while typing
    # disable_while_typing = false

    # Left-click-and-drag with three fingers
    # drag_3fg = 1
  }
}

# Scroll nicely in the terminal
windowrule = match:class (Alacritty|kitty), scroll_touchpad 1.5
windowrule = match:class com.mitchellh.ghostty, scroll_touchpad 0.2

# Enable touchpad gestures for changing workspaces
# See https://wiki.hyprland.org/Configuring/Gestures/
# gesture = 3, horizontal, workspace`
```



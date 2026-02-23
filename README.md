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


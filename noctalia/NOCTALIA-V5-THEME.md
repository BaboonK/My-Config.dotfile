# Noctalia v5 Theme Notes

## Files

- Active theme selector: `~/.config/noctalia/theme.toml`
- Custom palettes: `~/.config/noctalia/palettes/*.json`

Current palette:

- `~/.config/noctalia/palettes/Lain-Pink.json`

## How v5 loads the theme

Noctalia v5 reads `*.toml` files in `~/.config/noctalia/`.

The current selector is:

```toml
[theme]
mode = "dark"
source = "custom"
custom_palette = "Lain-Pink"
```

This means:

- use dark mode
- use a custom palette
- load `~/.config/noctalia/palettes/Lain-Pink.json`

## Palette format

A custom palette is a JSON file with `dark` and optionally `light` sections.

Example:

```json
{
  "dark": {
    "mPrimary": "#FF8888",
    "mOnPrimary": "#121215",
    "mSecondary": "#FF79C6",
    "mOnSecondary": "#121215",
    "mTertiary": "#8BE9FD",
    "mOnTertiary": "#121215",
    "mError": "#FF5555",
    "mOnError": "#121215",
    "mSurface": "#121215",
    "mOnSurface": "#E0E0D8",
    "mSurfaceVariant": "#1A1A1D",
    "mOnSurfaceVariant": "#9A9AAD",
    "mOutline": "#4D4F60",
    "mShadow": "#121215",
    "mHover": "#4D4F60",
    "mOnHover": "#E0E0D8"
  }
}
```

`terminal` colors can also be included in the same JSON file.

## How to import a new custom palette

1. Put the palette JSON into `~/.config/noctalia/palettes/`
2. Name it like `MyTheme.json`
3. Edit `~/.config/noctalia/theme.toml`
4. Set:

```toml
[theme]
mode = "dark"
source = "custom"
custom_palette = "MyTheme"
```

Important:

- `custom_palette` uses the file name without `.json`
- the file should be directly under `palettes/`
- do not use the old nested path style like `palettes/MyTheme/MyTheme.json`

## If the theme does not apply

Check whether GUI-managed overrides are taking precedence:

- `~/.local/state/noctalia/settings.toml`

v5 loads config in this rough order:

1. built-in defaults
2. `~/.config/noctalia/*.toml`
3. `~/.local/state/noctalia/settings.toml`

So `settings.toml` may override `theme.toml`.

## Useful commands

Verify what v5 is actually using:

```bash
noctalia config export full
```

Expected theme section:

```toml
[theme]
mode = "dark"
source = "custom"
custom_palette = "Lain-Pink"
```

## Autostart

Hyprland Lua:

```lua
hl.on("hyprland.start", function()
    hl.exec_cmd("noctalia")
end)
```

Niri:

```kdl
spawn-at-startup "noctalia"
```

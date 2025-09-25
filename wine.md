# Wine
Usually, Wine Just Works.

```sh
wine ./path/to/exe
```

## Observations
Wine creates a dummy Windows filesystem at a location called the "Wine Prefix".
This is controllable by the `WINEPREFIX` environment variable.
This defaults to `~/.wine`.

The `WINEDLLOVERRIDES` environment variable selects specific DLLs to be substituted.
I still don't know how this works, and in practice applications that need these DLLs seem to just fail
to load necessary DLLs if they're in this list.

## 32-bit wine


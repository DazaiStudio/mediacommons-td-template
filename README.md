# NYU Media Commons DMX Lighting Control

TouchDesigner-based DMX lighting control system for the NYU 370 Jay Street Media Commons facility, outputting via sACN (streaming ACN / E1.31).

https://github.com/DazaiStudio/mediacommons-td-template/releases/download/v0.1.0/mc-td-demo.mp4

## Rooms & Fixtures

The system controls 4 rooms at the NYU Media Commons on **sACN Universe 1**:

| Room | Fixtures |
|------|----------|
| 221 – Ballroom | Sixpar 300IP, ETC D22 LustrPlus, ETC Source 4WRD Color, Elation Unibar |
| 222 – Ballroom | (shared fixture pool) |
| 223 – Ballroom | (shared fixture pool) |
| 224 – Ballroom | (shared fixture pool) |

### Fixture Summary

| Fixture | Mode | Count | Channels |
|---------|------|-------|----------|
| Sixpar 300IP | 8-Ch | 16 (SP101–SP116) | R, G, B, W, A, UV, Dim, Strobe |
| ETC D22 LustrPlus | 9-Ch (Direct, Str Enabled) | 16 (D22_201–D22_216) | R, W, A, G, C, B, I, Int, Strobe |
| ETC Source 4WRD Color | 6-Ch | 12 (S4_301–S4_312) | Int, R, G, B, A, Strobe |
| Elation Unibar | 1-Ch (Dimmer) | 6 (UB501–UB506) | Int |

## Project Structure

```
mediacommons/
├── mediacommons.toe          # Main project file
├── DMX_Ballrooms.tox         # Ballroom fixtures & DMX buffer
├── DMX_AudioLab.tox          # Audio Lab fixtures
├── DMX_Blackbox.tox          # Blackbox fixtures
└── Backup/                   # Local backups (git-ignored)
```

## sACN Output

- Uses TouchDesigner's native `dmxoutCHOP` at project level
- sACN gateway IP: `192.168.0.101`
- Local NIC address must be set to `192.168.0.234`

## Requirements

- [TouchDesigner](https://derivative.ca/) (tested on 2024.x)
- Network access to sACN gateway on `192.168.0.0/24`

## Usage

1. Open `mediacommons/mediacommons.toe` in TouchDesigner
2. Verify the `dmxoutCHOP` local address matches your network interface
3. Control fixtures via the room panels

## Notes

- **Sixpar 300IP**: Strobe channel (ch8) must be set to `255` for light output — default `0` means no light
- The `dmxoutCHOP` must remain at project level (not inside nested baseCOMPs) to cook properly

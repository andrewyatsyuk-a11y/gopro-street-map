# GoPro Street Map

**See exactly where your GoPro videos were filmed — street by street.**

GoPro Street Map is a desktop app for Windows and macOS. Drop in your GoPro videos and it reads the GPS data recorded inside them, draws each route on a map, finds every street you drove or walked on, and lets you search across all your footage by street name. Play a video and a marker follows along on the map in real time.

## Features

- **Live map sync**: as the video plays, a marker moves along the route and the part already travelled is highlighted. Click anywhere on a route to jump to that moment in the video.
- **Many videos at once**: add single files, whole folders, or the `DCIM` folder of your SD card. Every route is shown on one map in its own colour.
- **Automatic street detection**: each video gets a timeline of the streets it passes, e.g. `0:00–1:42  McIvor Avenue  River East, Winnipeg`. Click a street to jump there.
- **Street search**: type part of a street, neighbourhood or city name to see which videos were recorded there and at what time. Matching sections light up on the map.
- **Captioned screenshots**: press **S** or click **Screenshot** to save the current frame in full resolution (up to 4K), captioned with the street, the date and the local time:
  > **McIvor Avenue, River East, Winnipeg**
  > Thursday, November 5, 2026 · 11:06:02 AM (UTC−06:00)
  > 49.95072, -97.06833 · 4 km/h · GX010018.MP4 @ 2:37
- **Correct local time**: the time zone comes from where the video was filmed, so the time stays right even if the camera clock or time-zone setting was wrong.
- **Live stats**: shows the current street, speed, altitude, distance travelled and local time.
- **Map layers**: OpenStreetMap, Esri streets and satellite imagery.
- **Remembers everything**: your video list and the streets it found are kept between sessions, so streets are looked up only once.

## Download

Get the latest version from the **[Releases](../../releases/latest)** page:

| Your computer | File |
|---|---|
| Windows 10 / 11 (64-bit) | `GoPro-Street-Map-Windows.zip` |
| Mac with Apple chip (M1, M2, M3, M4…) | `GoPro-Street-Map-macOS-AppleSilicon.zip` |
| Mac with Intel processor | `GoPro-Street-Map-macOS-Intel.zip` |

Not sure which Mac you have? Open  menu → **About This Mac**. If it lists **Chip: Apple M…**, use Apple Silicon. If it lists **Processor: Intel…**, use Intel.

### Install on Windows

1. Unzip the archive anywhere, for example into *Documents*. Don't run the app from inside the zip.
2. Double-click **GoPro Street Map.exe**.
3. If Windows SmartScreen appears, click **More info → Run anyway**. The app is not code-signed.

### Install on macOS

1. Unzip the archive and drag **GoPro Street Map.app** into *Applications*.
2. The app is not signed by Apple, so you need to unblock it once. Open **Terminal** and run:
   ```bash
   xattr -cr "/Applications/GoPro Street Map.app"
   ```
   ```bash
   codesign --force --deep --sign - "/Applications/GoPro Street Map.app"
   ```
3. Open the app normally. From then on it opens like any other app.

## How to use

1. Click **+ Add videos** or **Add folder**, or drag videos onto the window.
2. Wait a few seconds while the GPS is read and the streets are found. Progress is shown in the video list.
3. Pick a video and press play. The map follows along.
4. Search for a street in the search box, or browse the **Streets** tab.
5. Press **S** to save a captioned screenshot. Screenshots go to `Pictures/GoPro Street Map`.

**Keyboard shortcuts:** `S` screenshot · `Space` play/pause · `←` / `→` skip 5 s · `/` search

## Supported cameras

The app works with GoPro cameras that record GPS into the video's GPMF telemetry track. That covers HERO5 Black and newer, including HERO13 Black and MAX. GPS must be turned on in the camera settings. Videos recorded without a GPS lock are listed but have no route.

HEVC (H.265) and H.264 videos play on any reasonably recent Windows or Mac.

## Privacy

- Your videos never leave your computer. They are read and played locally.
- To find street names, the app sends GPS coordinates (not video) to [OpenStreetMap Nominatim](https://nominatim.org/), at most one request per second, following their usage policy. Results are cached locally.
- Map tiles are loaded from OpenStreetMap or Esri.

Street lookup and maps need an internet connection. Playback and the GPS track work offline.

## Build from source

You need [Node.js](https://nodejs.org/) and Python 3.

```bash
npm install
```

Download the official Electron release zips (`electron-vX-win32-x64.zip`, `electron-vX-darwin-arm64.zip`, `electron-vX-darwin-x64.zip`) from the [Electron releases](https://github.com/electron/electron/releases) page into one folder, then run:

```bash
python build.py path/to/electron-zips
```

The packages are written to `dist/`. Tested with Electron 44.

### Project structure

| File | What it does |
|---|---|
| `gpmf.js` | Reads GoPro GPMF telemetry (GPS5 / GPS9) from MP4 files without loading the whole video |
| `streets.js` | Converts a GPS track into street segments via Nominatim, with rate limiting and caching |
| `main.js` | Electron main process: video library, local video streaming server, screenshots |
| `renderer/` | User interface: Leaflet map, player, search, captioned screenshots |
| `build.py` | Packages the app for Windows and macOS |

## Credits

- Map data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors
- Map rendering by [Leaflet](https://leafletjs.com/)
- Satellite imagery © Esri
- Time-zone lookup by [@photostructure/tz-lookup](https://github.com/photostructure/tz-lookup)
- Built with [Electron](https://www.electronjs.org/)

GoPro and HERO are trademarks of GoPro, Inc. This project is not affiliated with or endorsed by GoPro.

## License

MIT

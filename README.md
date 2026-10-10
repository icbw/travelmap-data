# travelmap-data

Reference data releases for the TravelMap Android app: country packs (cities and
admin-1 regions), railway lines, railway stations and, since `data-2`, road
networks for routing journeys added by hand offline, downloaded by the app only
after the user confirms. Each release is pinned by the app version that uses it; the app checks
every file against SHA-256 values it ships with.

TravelMap 的参考数据：国家包（城市、一级行政区）、铁路线、车站，以及（`data-2` 起）
离线算路用的路网。App 只在用户确认后下载，
每个文件都按 App 内置的 SHA-256 校验。

## Files in a release

| File | Content |
| --- | --- |
| `geo-<id>.db.gz` | A country pack: admin-1 regions and cities of one country, or of the small countries of one region (gzipped SQLite) |
| `rail-blocks.pmtiles` | Railway, tram and metro lines at 0.2 m, one block per z8 web-mercator tile (PMTiles container; tile content is TravelMap's own deflated encoding, not MVT). The app reads single blocks with HTTP range requests |
| `rail-blocks.idx` | Block index: byte offset, length and a 128-bit SHA-256 prefix of every block |
| `core_ref.db` | The core bundled with the app: time zones, countries and disputed areas at 1 km, airports, and the manifest of this release |
| `stations.db.gz` | Railway stations and halts of the world (names in the local language, Chinese, English, Japanese), for adding journeys by hand; downloaded on first use (gzipped SQLite) |
| `packs.json` | The country packs' manifest entries (id, version, countries, size, SHA-256) |
| `road-main-blocks.pmtiles` | Main roads (motorway to tertiary and their links) of the countries cut so far, one block per z8 web-mercator tile, for offline car and bus routing; read in single blocks with HTTP range requests (since `data-2`) |
| `road-street-blocks.pmtiles` | Streets (unclassified, residential, living street) of the same countries, one block per z10 tile (since `data-2`) |
| `road-main-blocks.idx`, `road-street-blocks.idx` | Block indexes of the two road archives: byte offset, length and a 128-bit SHA-256 prefix of every block |
| `road-countries.json` | The countries the road archives cover (`data-2`: Switzerland, Italy) and the OpenStreetMap extract date |

The files are built from the sources below by the `georef` tool of the TravelMap
project (`georef core`, `georef packs`, `georef rail`, `georef rail-archive`,
`georef stations`, `georef airports`, `georef roads`, `georef manifest`).

## Releases

| Tag | Date | What changed |
| --- | --- | --- |
| `data-2` | 2026-10-10 | Road networks of Switzerland and Italy (OSM 2026-10-08) for offline routing; the core's manifest lists them. The other files as in `data-1` and its later station list |
| `data-1` | 2026-10-05 | 47 country packs, railway lines in 4,793 z8 blocks, block index, the core |

## Sources and licences

See [LICENSE](LICENSE).

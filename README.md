# travelmap-data

Reference data releases for the TravelMap Android app: country packs (cities and
admin-1 regions) and railway lines, downloaded by the app only after the user
confirms. Each release is pinned by the app version that uses it; the app checks
every file against SHA-256 values it ships with.

TravelMap 的参考数据：国家包（城市、一级行政区）和铁路线。App 只在用户确认后下载，
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

The files are built from the sources below by the `georef` tool of the TravelMap
project (`georef core`, `georef packs`, `georef rail`, `georef rail-archive`,
`georef stations`, `georef airports`, `georef manifest`).

## Sources and licences

See [LICENSE](LICENSE).

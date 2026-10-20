# Sunlight meetings data

Aggregated AA meeting data for the [Sunlight](https://github.com/oliverhatch) iPhone
app's meeting finder: **~115,000 weekly meetings across the US and
Canada**, in [Meeting Guide API](https://github.com/code4recovery/spec)
format. Listings that several feeds publish (an area feed republishing
its intergroups) are merged into one; address-only listings are
geocoded with the US Census geocoder.

## `v2/` — the current format (schema 2)

- `v2/index.json` — one entry per 0.5° map tile that has meetings:
  `[id, hash, sun, mon, tue, wed, thu, fri, sat, lat, lng, place, region…]`
  (tile id = row × 720 + col, row = ⌊(lat + 90) / 0.5⌋, col =
  ⌊(lng + 180) / 0.5⌋; the hash is the first 16 hex digits of the file's
  SHA-256; the weekday columns count the tile's meetings; lat/lng is their
  centroid). Plus `regions` (`[key, hash, count]`), `feeds` (attribution),
  and `offices` (`[lat, lng, name, url]`, local AA offices with a verified
  website).
- `v2/tiles/{id}.json` — the tile's in-person and hybrid meetings.
- `v2/regions/{country}-{state}.json` — the state's meetings with no map
  location: online-only meetings, and the rare address that couldn't be
  geocoded.

Meeting objects carry `feed` (source id), `timezone` (IANA), and, when
other feeds list the same meeting, `also` (their `feed/slug` ids).

## Schema 1 (legacy)

`manifest.json` + `shards/{country}-{state}.json`: the same meetings
sharded by state, for app builds that predate `v2/`. It will be removed.

## Provenance

Meetings are aggregated from the public Meeting Guide–format JSON
feeds that AA intergroups and central offices publish on their own
websites (mostly via the open-source
[12 Step Meeting List](https://wordpress.org/plugins/12-step-meeting-list/)
WordPress plugin), plus a small number of politely-crawled public
meeting directories. Each meeting's `feed` field identifies its source.
Data is refreshed weekly; `generated` in the index is the build
timestamp.

The meeting information itself belongs to the local AA service
entities that publish it. If you run one of the source websites and
want your feed excluded or see an error, open an issue or email
oliverjhatch@gmail.com and it will be handled promptly.

## Not affiliated

This project is not affiliated with, approved by, or endorsed by
Alcoholics Anonymous World Services, the Meeting Guide app, or any AA
service entity. "AA" and "Alcoholics Anonymous" are registered
trademarks of AAWS, used only to describe the meetings listed.
Meeting details change; always confirm with the local intergroup.

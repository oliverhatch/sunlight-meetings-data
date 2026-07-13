# Sunlight meetings data

Aggregated AA meeting data for the [Sunlight](https://github.com/oliverhatch) iPhone
app's meeting finder: **~78,000 weekly meetings across the US and
Canada**, in [Meeting Guide API](https://github.com/code4recovery/spec)
format, sharded by state.

- `manifest.json` — shard index: per-state file, meeting count, bytes,
  sha256, bounding box, and source feeds (`schema_version: 1`)
- `shards/{country}-{state}.json` — minified arrays of spec-format
  meeting objects, extended with `feed` (source id) and `timezone`
  (IANA), sorted by day/time

## Provenance

Meetings are aggregated from the public Meeting Guide–format JSON
feeds that AA intergroups and central offices publish on their own
websites (mostly via the open-source
[12 Step Meeting List](https://wordpress.org/plugins/12-step-meeting-list/)
WordPress plugin), plus a small number of politely-crawled public
meeting directories. Each meeting's `feed` field and the manifest's
`feeds` lists identify its source. Data is refreshed roughly monthly;
`generated` in the manifest is the build timestamp.

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

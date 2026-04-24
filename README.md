# vreca.github.io

Data source site of [vreca.org](https://event.vreca.org). This repo serves as data mirror for use by the VRChat gimmick,
in conformation to the "Trusted URLs" policy imposed by VRChat. https://creators.vrchat.com/worlds/udon/string-loading#trusted-urls

> Register your own event now at VRECA: https://event.vreca.org

## URL layout

| Path | What |
|------|------|
| `/` | `index.html` (landing) |
| `/v1/events.json` | Public events index (see below) |
| `/v1/img/{eventId}/poster.jpg` | Cached poster image for that event ID |


## Data: `/v1/events.json`

Top-level object:

| Field | Type | Meaning |
|-------|------|---------|
| `data` | `APIEvent[]` | List of events |
| `updated_at` | string (ISO 8601) | When the file was last generated / exported |

Each item in `data` is an event object, including at least: `id`, `title`, `description`, `time_start`, `time_end`, `instance_type`, optional `group_id`, `group_name`, `cal_id`, `tags`, and **`poster`**.

### `poster` field

- In JSON, `poster` is a partial path, always prepend it with base URL `https://vreca.github.io/v1` to get the full URL.

Example result should look like `https://vreca.github.io/v1/img/019da5e6-8529-7b95-95f5-30a4555094ea/poster.jpg`

**Resolve on the same host:** if the site is served with this layout, a client can treat poster URLs as relative to the `v1` “folder”, e.g. `new URL(event.poster, location.origin + "/v1/")`, or `"/v1" + event.poster` when `event.poster` is `/img/...`.

## Local folder map

```text
vreca.github.io/
├── index.html  
└── v1/
    ├── events.json    # { data, updated_at }
    └── img/
        └── {eventId}/
            └── poster.jpg
```

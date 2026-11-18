# protecting_camp

A small Express storefront API for camping gear, packaged as a Docker web-security exercise.

## What it does

The app serves a static camping shop page and a JSON API for listing and adding items. It also exposes connection-check and flag endpoints; the flag is read from `flag.txt` at runtime and is only served when the request URL, parsed with `parse-url`, points at loopback.

Endpoints documented by `GET /api`:

| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/api/items` | List the items |
| `POST` | `/api/items` | Add an item (`{"name": "...", "price": 0}`) |
| `POST` | `/api/check_connection` | Fetch an outward URL and return a short preview |
| `GET` | `/api/flag_status` | Report that the flag exists |
| `GET` | `/api/flag` | Return the flag (private) |

## Stack

- Node.js 18, Express 4
- `parse-url` and `request`
- Docker image running as an unprivileged `challenge` user

## Running

```bash
npm install
npm run run        # node ./index.js, port 3000
# or: npm run dev  # nodemon
```

Docker:

```bash
docker build -t protecting_camp .
docker run --rm -p 3000:3000 protecting_camp
```

The Dockerfile copies `flag.txt` into the image and makes it read-only for the app user. That file is not in the repository, so a local build needs it beside the Dockerfile.

## Notes

- No database: items start from a hard-coded list and live in memory.
- The app is an exercise, not a production service.

# TikTok Profile Search API

Search TikTok users by username. No API key needed.

Live: https://tiktok-profile-api.faizankhichi.me/?u=prince_faizee

Demo: https://tiktok-profile-api.faizankhichi.me/demo

## Usage

```
GET /?u=<username>
GET /?u=https://www.tiktok.com/@prince_faizee
```

## Response

```json
{
  "success": true,
  "query": "prince_faizee",
  "user": {
    "username": "prince_faizee",
    "nickname": "Faizan Ahmad Khichi | FAK LABS",
    "secUid": "MS4wLjABAAAAd2G0i7JWf5llkIzL_iYfaXEGVDfHDjNt9oo-r-8bHhp5N9Xe2S2f4b0ARh0ju9ph",
    "userId": "7379105450284319750",
    "verified": false,
    "avatar": "https://p16-common-sign.tiktokcdn-us.com/...",
    "followerCount": 819
  },
  "total": 10,
  "users": [ "..." ]
}
```

`user` is the exact match (case-insensitive), or `null` if no exact match
exists. `users` is the full result list, `total` is the total match count.

## Errors

- Missing `?u=` → 400
- Non-GET → 405
- Upstream failure → 502 (with `upstreamStatus`)

## Notes

- CORS open (`*`), no API key.
- The demo page is built with the API itself. Its code is in this repo
  under `example-site/` — take it, build your own.

---

*This repo is documentation only.*

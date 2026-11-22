# TikTok Profile Search API

Search TikTok users by username — or list a profile's videos with
download links, in bulk. No API key needed.

Live: https://tiktok-profile-api.faizankhichi.me/?u=prince_faizee

Demo: https://tiktok-profile-api.faizankhichi.me/demo

## Usage

```
GET /?u=<username>                              search users
GET /?u=https://www.tiktok.com/@prince_faizee
GET /profile?u=<username>                       full profile
GET /videos?u=<username>                        profile videos + download links
GET /videos?u=<username>&limit=60&cursor=<cursor>
```

`limit` is 1–90 (default 30). One call returns up to 30 videos; use the
returned `cursor` with `hasMore` to page through the rest.

## Response — search

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

## Response — profile

```json
{
  "success": true,
  "query": "prince_faizee",
  "profileUrl": "https://www.tiktok.com/@prince_faizee",
  "user": {
    "username": "prince_faizee",
    "nickname": "Faizan Ahmad Khichi | FAK LABS",
    "userId": "7379105450284319750",
    "verified": false,
    "bio": "Founder @ FAK LABS | AI Engineer ...",
    "avatar": "https://p16-common-sign.tiktokcdn-us.com/...",
    "stats": { "followers": 819, "following": 0, "likes": 55, "videos": 8, "friends": 4 },
    "privateAccount": false
  }
}
```

## Response — videos (bulk download)

```json
{
  "success": true,
  "query": "prince_faizee",
  "user": { "...": "same profile object as /profile" },
  "videos": [
    {
      "id": "7708437799829114133",
      "url": "https://www.tiktok.com/@prince_faizee/video/7708437799829114133",
      "desc": "Free X API. ...",
      "cover": "https://p16-common-sign.tiktokcdn-eu.com/...",
      "duration": 6,
      "created": 1794760540,
      "stats": { "plays": 90, "likes": 2, "comments": 0, "shares": 0 },
      "downloadUrl": "https://v45.tiktokcdn-eu.com/...",
      "playUrl": "https://v45.tiktokcdn-eu.com/..."
    }
  ],
  "total": 7,
  "hasMore": false,
  "cursor": null,
  "note": "Download links are signed and expire — fetch a fresh link right before downloading."
}
```

## Errors

- Missing `?u=` → 400
- Unknown username → 404 (`/profile`, `/videos`)
- Non-GET → 405
- Upstream failure → 502 (with `upstreamStatus`)

## Notes

- CORS open (`*`), no API key.
- Download links are signed and expire. Fetch a fresh link from `/videos`
  right before downloading, and download from the same IP.
- A private account returns its profile with an empty `videos` list.
- The demo page is built with the API itself. Its code is in this repo
  under `example-site/` — take it, build your own.

---

*This repo is documentation only.*

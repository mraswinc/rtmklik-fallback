# RTMKlik Fallback — Static Live Streaming Page

A lightweight, zero-dependency static fallback page for RTMKlik live streaming.
Designed as DR target when the primary Amplify Next.js app has high error rates during FIFA World Cup 2026.

## Quick Start

```bash
npx serve public -l 3000
```

## Deploy to AWS Amplify

1. Push this repo to GitHub
2. AWS Amplify Console → New App → Host Web App → GitHub
3. Select this repository  
4. Amplify auto-detects `amplify.yml` and deploys `public/`

## Configuration

Edit `public/index.html` — update the `CHANNELS` object with HLS stream URLs from MediaPackage/IVS.

## Features

- Pure static HTML — no server-side dependencies
- HLS.js player with auto-quality and retry logic
- Channel switcher (Sukan+, Okey, FIFA WC 1-3)
- Auto-retry on stream errors (5s backoff)
- Dark theme matching RTMKlik production UI
- Responsive (mobile + desktop)

## WAR Room Failover

```bash
# Activate fallback
aws amplify update-app --app-id YOUR_APP_ID \
  --custom-rules '[{"source":"/<*>","target":"/fallback.html","status":"200"}]'

# Deactivate
aws amplify update-app --app-id YOUR_APP_ID --custom-rules '[]'
```

## License

Internal use — Radio Television Malaysia / AWS.

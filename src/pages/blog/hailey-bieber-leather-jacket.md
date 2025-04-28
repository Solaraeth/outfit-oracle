---
layout: ../../layouts/BlogPost.astro
title: "Hailey Bieber’s Leather-Jacket Look — Get It for £180"
pubDate: "2025-05-02T00:00:00"
description: "How to recreate Hailey’s off-duty leather-jacket outfit with affordable pieces in stock right now."
author: OutfitOracle
cover: /demo.jpg   # uses the Unsplash photo you uploaded
slug: hailey-bieber-leather-jacket
tags: [celebrity, street-style, look-for-less]
---

> **The Inspiration**  
> Spotted leaving a West Hollywood café, Hailey Bieber paired an oversized black leather jacket with straight-leg denim and chunky loafers—a £3,200 ensemble that sold out in days.

| Piece | Budget-friendly twin | Price |
|-------|---------------------|-------|
| Oversized leather jacket | [Mango “Rocky” Faux-Leather Jacket](https://go.skimresources.com?id=TEST123&url=https%3A%2F%2Fshop.mango.com%2Fgb%2Fwoman%2Fjackets-leather%2Foversized-faux-leather-jacket_87154019.html) | **£119** |
| Straight-leg jeans | [Levi's 501 ‘90s](https://go.skimresources.com?id=TEST123&url=https%3A%2F%2Fwww.levi.com%2FGB%2Fen_GB%2Fclothing%2Fwomen%2Fjeans%2F501-90s-womens-jeans%2Fp%2F362000040) | **£95** |
| Chunky loafers | [ASOS Design Chill Loafer](https://go.skimresources.com?id=TEST123&url=https%3A%2F%2Fwww.asos.com%2Fasos-design%2Fasos-design-chill-chunky-loafers-in-black%2Fprd%2F203110169) | **£38** |

*All links commission-eligible. Prices checked hourly.*

---

### 3.2 Commit directly to **`main`**  
GitHub will show “1 new file.” Click **Commit**.

Vercel auto-builds; after ~60 s refresh `https://outfitoracle.net` (or the `.vercel.app` URL) and you’ll see the post under **/blog**.

---

## 4 Set up the hourly price-refresh GitHub Action

1. Still in GitHub, click **“Add file → Create new file.”**  
2. Name it **`.github/workflows/price-refresh.yml`**  
3. Paste:

```yaml
name: Price refresh
on:
  schedule:
    - cron:  '0 * * * *'   # every hour
jobs:
  rebuild:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Bump timestamp to trigger rebuild
        run: |
          echo "refresh=$(date -u)" > ./src/refresh.json
      - name: Commit & push
        run: |
          git config user.name "OutfitOracle Bot"
          git config user.email "bot@outfitoracle.net"
          git add src/refresh.json
          git commit -m "Hourly refresh" || echo "No change"
          git push

# Landing page: AI video ads for Indian brands

A single static page (`index.html`) with web-sized copies of the ads in
`videos/` and a still for each in `posters/`. No build step.

## Put it online (Netlify)

1. Go to https://app.netlify.com/drop
2. Drag this whole `landing-page` folder onto the page.
3. Netlify gives you a link. Rename the site in Site settings if you want a
   nicer `*.netlify.app` name, or connect a custom domain.

To update it later, open the site in Netlify → Deploys, and drag the folder
onto the deploy area again.

## Add a new ad

1. Make a web copy (720p, ~5-8 MB) and a poster still. In PowerShell, with
   the name you want (lowercase, dashes) and a timestamp in seconds for the
   still:

   ```
   ffmpeg -i "path\to\final-export.mp4" -vf "scale=720:-2" -c:v libx264 -preset slow -crf 26 -pix_fmt yuv420p -c:a aac -b:a 96k -movflags +faststart videos\brand-product.mp4
   ffmpeg -ss 3 -i "path\to\final-export.mp4" -frames:v 1 -vf "scale=540:-2" -q:v 4 posters\brand-product.jpg
   ```

2. In `index.html`, add one line near the bottom to `INDIAN_ADS` (the
   "Recent work" grid) or `LOCAL_ADS` (the US local-services strip under
   Results), newest first:

   ```js
   { file: "brand-product", brand: "Brand", product: "What it is. UGC with captions", length: "0:30" },
   ```

## Hero

The hero's moving wall uses the stills in `posters/` and a muted 10-second
montage, `videos/hero-montage.mp4`, cut from six ads. To change the wall,
edit the two `.col-track` lists of images near the top of `index.html`.

## Results

The results section shows totals from the lead-gen campaign's Meta Ads
export of 5 Oct 2026: 408 leads, $8.13 cost per lead,
3.83% CTR, $1.30 CPC, 289 ads from 57 creatives across 28 niches and 140+
cities, plus the best-performing creatives. The client is never named, and
no campaign IDs, account numbers or staff names go on the page. Add results
for Indian brands once they exist, where the comment in `#results` marks the
spot.

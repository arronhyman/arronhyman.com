# arronhyman.com

Personal site for **Arron Hyman**, Founder & CEO of Lesuto Technologies.

- Motto: *Let's Succeed Together*
- Stack: static HTML/CSS + nginx on **Cloud Run** (`min-instances=0`, free when idle)
- Domain: `arronhyman.com` (GoDaddy registrar, Route53 DNS; Google Workspace MX unchanged)

## Local preview

```bash
python3 -m http.server 4173
# open http://localhost:4173
```

```bash
docker build -t arron-hyman .
docker run --rm -p 8080:8080 arron-hyman
# open http://localhost:8080
```

## Live

- Cloud Run (direct, no load balancer): https://arron-hyman-xbscrs6jja-uw.a.run.app
- Custom domain via Cloud Run domain mapping: https://arronhyman.com / https://www.arronhyman.com
- Free when idle (`min-instances=0`). No global LB.
- Google Workspace MX and `et.arronhyman.com` left unchanged

## Next: Connect + SDK on this site

Once Arron's Lesuto Connect meeting type exists on the Lesuto Technologies channel:

1. Create a public meeting type in Lesuto Connect (Seller or admin).
2. Replace `https://meet.lesuto.com/` links on this site with the personal URL (`https://meet.lesuto.com/{slug}`).
3. Optional: embed the Connect booking module via Chameleon SDK with the merchant site key.
4. Livestream / go-live: embed `livestream-player` (or Hub live) with the store's channel token / site key after the Arron Hyman merchant store is published.

Contact forms can POST through the gateway once a small serverless endpoint or SDK form module is wired to that merchant store. Until then, mailto + Connect booking is the path.

## Deploy

1. Add GitHub secrets on this repo:
   - `GCP_PROJECT_ID`
   - `GCP_SA_KEY` (service account JSON with Cloud Run + Artifact Registry push)
2. Tag and push:

```bash
git tag "v$(date +%Y%m%d-%H%M%S)"
git push origin main --tags
```

Or run **Deploy arronhyman.com** via Actions → workflow_dispatch.

## DNS cutover (after first Cloud Run deploy)

Leave **MX** and **`et.arronhyman.com`** alone.

1. Map custom domains in Cloud Run (or load balancer) for `arronhyman.com` and `www.arronhyman.com`.
2. In Route53 hosted zone `ZFRIRXJSGPVBZ`, replace the apex `A` alias that points at S3 website hosting with the records Google provides.
3. Add `www` as instructed by domain mapping.
4. After HTTPS works, disable the S3 bucket website redirect on `arronhyman.com` (it currently 301s to LinkedIn).

## Contact

- Email: arron@lesuto.com
- LinkedIn: https://www.linkedin.com/in/arronhyman/
- Instagram: https://www.instagram.com/lesutoandtravel
- Lesuto: https://www.lesuto.com/

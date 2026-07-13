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

- Cloud Run: https://arron-hyman-xbscrs6jja-uw.a.run.app
- Custom domain (GCP global LB `136.68.12.116`): https://arronhyman.com / https://www.arronhyman.com
- Managed SSL cert provisions after DNS propagates (can take up to ~60 minutes)
- Google Workspace MX and `et.arronhyman.com` left unchanged

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

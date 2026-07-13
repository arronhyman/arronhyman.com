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

## Connect + SDK

- Site key: embedded in `index.html` (`data-site-key`)
- Contact: SDK `support-form` in the Connect section
- Booking: iframe to `https://meet.arronhyman.com/` (create a public meeting type in Connect so slots appear)
- Domains verified for injection: `arronhyman.com`, `www.arronhyman.com`; booking: `meet.arronhyman.com`

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

## Contact

- Email: arron@lesuto.com
- Booking: https://meet.arronhyman.com/
- LinkedIn: https://www.linkedin.com/in/arronhyman/
- Instagram: https://www.instagram.com/lesutoandtravel
- Lesuto: https://www.lesuto.com/

# V5 Medical Business Communication Portal

Source for [12888.de](https://12888.de), the dedicated outbound business
communication portal used by the V5 Medical international business team.

The primary company website, product catalog, quality resources and inquiry
workflow remain on [v5med.net](https://v5med.net).

## Local preview

```bash
python3 -m http.server 8088
```

Then open `http://127.0.0.1:8088`.

## Deployment notes

- Static files only; no build step or third-party runtime dependencies.
- `_headers` is applied by Cloudflare Pages.
- Keep sender verification addresses and the primary-domain confirmation route
  aligned with the live mail configuration.
- Review `DOMAIN_TRUST_CHECKLIST.md` before treating the sender domain as fully
  hardened; the website is only one layer of email trust.

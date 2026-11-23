# 12888.de domain trust checklist

Checked on 2026-11-23. This document contains no credentials or private keys.

## Website

- [x] Replace the unrelated Vvohoo landing page with a V5 Medical business
  communication portal.
- [x] Identify `rex@12888.de` and `leo@12888.de` as designated business
  mailboxes.
- [x] Provide an independent confirmation route through `sales@v5med.net`.
- [x] Link products, company verification, privacy and formal inquiries to the
  primary domain, `v5med.net`.
- [x] Add metadata, structured data, sitemap, robots policy and Cloudflare
  Pages security headers.
- [ ] Deploy the reviewed branch and verify the response headers on the live
  domain.

## DNS and transport findings

| Control | Observed | Recommended next action |
|---|---|---|
| Apex website | `https://12888.de` returns HTTP 200 | Re-test after deployment. |
| `www` website | `https://www.12888.de` returns Cloudflare 530 and has no public A/CNAME answer | Add the intended `www` DNS record/custom domain, then retain the 301 redirect to the apex. |
| MX | Zoho MX records present | No change unless the mail provider changes. |
| SPF | Zoho include with `~all` | Confirm every legitimate sender, then consider changing to `-all`. |
| DKIM | Zoho selector published | Verify actual messages from Rex and Leo show `dkim=pass` and aligned `header.d=12888.de`. |
| DMARC | `p=none` with aggregate reporting | Review reports, move gradually to `p=quarantine`, then `p=reject` after legitimate traffic is proven aligned. |
| MTA-STS | Not published | Add policy hosting and `_mta-sts` TXT if supported by the operating mail setup. |
| TLS reporting | Not published | Add `_smtp._tls` reporting after choosing a monitored report mailbox. |
| BIMI | Not published | Optional after DMARC enforcement; do not prioritize before SPF/DKIM/DMARC alignment. |

## Safe DMARC rollout

Do not jump directly from monitoring to reject without reading aggregate
reports. A conservative sequence is:

1. Confirm that mail from both designated accounts passes SPF or DKIM with
   DMARC alignment.
2. Inventory any CRM, cold-email platform or transactional sender that uses
   `12888.de` in the visible From address.
3. Move to quarantine with a limited percentage and monitor failures.
4. Raise the percentage after all legitimate sources are aligned.
5. Move to reject only after the monitoring window shows no unexplained
   legitimate failures.

## Post-deployment acceptance

- [ ] `https://12888.de` shows the V5 Medical portal and returns HTTP 200.
- [ ] `https://www.12888.de` resolves and redirects once to the apex.
- [ ] The page has no browser console errors or missing local assets.
- [ ] All `v5med.net` links return HTTP 200.
- [ ] Mobile navigation works at 390 px width.
- [ ] A test message from Rex and Leo independently shows SPF, DKIM and DMARC
  pass in the receiving mailbox's original-message view.
- [ ] Reply-To and From identities match the intended sales workflow.
- [ ] No email template asks a recipient to trust changed bank details solely
  from email.

# Quick Reference

This page is part of the Personal Website Setup Guide. If you are joining mid-series, start at the [Home page](index.md).

---

All configuration values, DNS records, and settings from this guide in one place.

---

## DNS records: GitHub Pages

Add these in Cloudflare DNS. Every record must be set to **DNS only** (grey cloud).

> **Note:** In DNS records, `@` represents your root domain (for example, `yourname.com`). Do not type your actual domain name in the Name field. Type `@` exactly as shown.
>
> Replace `yourusername.github.io` in the CNAME Content field with your actual GitHub Pages URL before saving.

| Type | Name | Content | Proxy status |
|------|------|---------|-------------|
| A | @ | 185.199.108.153 | DNS only |
| A | @ | 185.199.109.153 | DNS only |
| A | @ | 185.199.110.153 | DNS only |
| A | @ | 185.199.111.153 | DNS only |
| CNAME | www | yourusername.github.io | DNS only |

---

## DNS records: Email Routing

Cloudflare adds these automatically when you enable Email Routing. You do not need to add them manually.

| Type | Purpose |
|------|---------|
| MX | Routes incoming email to Cloudflare Email Routing |
| TXT | SPF record: verifies that Cloudflare is authorised to send email for your domain and helps prevent emails from being marked as spam |

---

## Gmail SMTP settings

Use these when adding your custom address in Gmail under Accounts and Import.

| Setting | Value |
|---------|-------|
| SMTP Server | smtp.gmail.com |
| Port | 587 (preferred) |
| Username | Your full Gmail address |
| Password | 16-character App Password |
| Connection | TLS |

> **Note:** If port 587 with TLS fails due to network restrictions, use port 465 with SSL as an alternative.

---

## System summary

| What | How |
|------|-----|
| Website hosting | GitHub Pages, free, no server required |
| Domain registration | Cloudflare Registrar, at-cost pricing |
| DNS management | Cloudflare DNS, DNS only for all GitHub records |
| HTTPS | Issued automatically by GitHub via Let's Encrypt |
| Email receiving | Cloudflare Email Routing forwarding to Gmail |
| Email sending | Gmail SMTP with App Password |

---

## Key URLs

| Resource | URL |
|----------|-----|
| GitHub | [github.com](https://github.com) |
| Cloudflare dashboard | [dash.cloudflare.com](https://dash.cloudflare.com) |
| Google Account Security | [myaccount.google.com/security](https://myaccount.google.com/security) |
| App Passwords | [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords) (only accessible if 2-Step Verification is enabled) |
| GitHub Pages IP verification | [docs.github.com/pages](https://docs.github.com/pages) |
| DNS propagation checker | [dnschecker.org](https://dnschecker.org) |

---

If something is not working, see the [Troubleshooting](troubleshooting.md) page.

---

*Written by Douglas Ebhoman, a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.*
*[douglasebhoman.com](https://douglasebhoman.com) · [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)*
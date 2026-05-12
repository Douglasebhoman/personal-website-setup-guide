# Personal Website Setup Guide

This guide walks you through building a complete personal website with a custom domain, HTTPS, and a professional email address, using free tools and one paid component.

By the end you will have:

- A live website hosted for free on GitHub Pages
- A custom domain pointing to that site (for example, yourname.com)
- HTTPS enabled automatically
- A professional email address (you@yourname.com) that sends and receives through Gmail

The entire system is free except for the domain name itself, which costs approximately $10 to $12 per year for a .com domain.

---

## What you will need

Before starting, make sure you have the following:

- A GitHub account, free at [github.com](https://github.com)
- A Cloudflare account, free at [cloudflare.com](https://cloudflare.com)
- A Gmail account
- A domain name purchased through Cloudflare Registrar (covered in the Domain Registration section)
- A basic HTML file for your website, or willingness to create one

No prior experience with GitHub, DNS, or email configuration is assumed. Every step is explained from scratch.

---

## How this guide is structured

| Page | What it covers |
|------|---------------|
| [GitHub Pages](part-1-github-pages.md) | Create a repository, add your HTML file, and enable GitHub Pages |
| [Domain Registration](part-2-domain-registration.md) | Purchase a custom domain through Cloudflare Registrar |
| [DNS Configuration](part-3-dns-configuration.md) | Connect your domain to GitHub Pages and enable HTTPS |
| [Professional Email](part-4-professional-email.md) | Set up a custom email address that sends and receives through Gmail |
| [Quick Reference](part-5-quick-reference.md) | All DNS records and configuration values in one place |
| [Troubleshooting](troubleshooting.md) | Solutions to the most common problems at each stage |

---

## How the system works

The components of this guide work together as a connected system:

```
GitHub Pages          → hosts your website files
Cloudflare Registrar  → owns your domain name
Cloudflare DNS        → routes your domain to GitHub Pages
Cloudflare Email      → receives email at your custom domain
Gmail SMTP            → sends email from your custom domain
```

Each part is independent, you can complete them in any order, but the order in this guide is the most logical sequence for a first-time setup.

---

Start with [GitHub Pages](part-1-github-pages.md).
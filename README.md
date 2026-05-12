# Personal Website Setup Guide

Most personal website guides stop at hosting. This one covers the complete setup: a live website, a custom domain, HTTPS, and a professional email address using your own domain, at no additional cost beyond the domain registration itself.

Built with GitHub Pages, Cloudflare, and Gmail. No paid hosting. No email subscription required.

**Live documentation site:** [douglasebhoman.com/personal-website-setup-guide](https://douglasebhoman.com/personal-website-setup-guide/)

No prior experience with GitHub, DNS, or email configuration is required. Every step is explained from scratch.

---

## What this guide covers

| Page | What it covers |
|------|---------------|
| [GitHub Pages](docs/part-1-github-pages.md) | Create a repository, add your HTML file, and deploy a live website for free |
| [Domain Registration](docs/part-2-domain-registration.md) | Purchase a custom domain through Cloudflare Registrar |
| [DNS Configuration](docs/part-3-dns-configuration.md) | Link your domain to GitHub Pages using DNS records and enable HTTPS |
| [Professional Email](docs/part-4-professional-email.md) | Set up a custom domain email address that sends and receives through Gmail |
| [Quick Reference](docs/part-5-quick-reference.md) | All DNS records and configuration values in one place |
| [Troubleshooting](docs/troubleshooting.md) | Solutions to the most common problems at each stage |

The entire system is free except for the domain name itself, which costs approximately $10 to $12 USD per year.

---

## Repository structure

```
personal-website-setup-guide/
├── mkdocs.yml
├── README.md
└── docs/
    ├── index.md
    ├── part-1-github-pages.md
    ├── part-2-domain-registration.md
    ├── part-3-dns-configuration.md
    ├── part-4-professional-email.md
    ├── part-5-quick-reference.md
    ├── troubleshooting.md
    └── stylesheets/
        └── brand.css
```

---

## Tools used

| Tool | Purpose | Cost |
|------|---------|------|
| GitHub Pages | Website hosting | Free |
| Cloudflare Registrar | Domain registration | Approximately $10 to $12 USD per year |
| Cloudflare DNS | DNS management | Free |
| Cloudflare Email Routing | Email receiving | Free |
| Gmail SMTP | Email sending | Free |

---

## Publishing workflow

This guide is version-controlled and deployed via GitHub Actions, the same workflow described in the guide itself.

---

## About the author

**Douglas Ebhoman** is a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.

- [douglasebhoman.com/cv](https://douglasebhoman.com/cv)
- [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)
- [douglasebhoman.com](https://douglasebhoman.com)

---

> Documentation is infrastructure. I treat it that way.
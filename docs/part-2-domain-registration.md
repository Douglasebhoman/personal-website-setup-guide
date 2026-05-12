# Part 2: Domain Registration

This page is part of the Personal Website Setup Guide. If you are joining mid-series, start at the [Home page](index.md).

---

A custom domain replaces the default `yourusername.github.io` URL with a professional address like `yourname.com`. This part covers purchasing a domain through Cloudflare Registrar.

---

## Why Cloudflare Registrar

Cloudflare sells domains at cost with no markup. There are no renewal price increases after the first year and no upsells during checkout.

Since your DNS will also be managed through Cloudflare in Part 3, purchasing the domain here keeps everything in one place. There is no need to transfer DNS to a separate provider.

---

## What is a DNS zone

A DNS zone is the control panel for your domain's DNS records. Every time someone types your domain into a browser, DNS records tell the internet where to send them.

When you purchase a domain through Cloudflare, a DNS zone is created automatically. Part 3 of this guide uses that zone to connect your domain to GitHub Pages.

---

## Step 1: Register a domain

1. Log into your Cloudflare account at [dash.cloudflare.com](https://dash.cloudflare.com)
2. In the left sidebar, click **Domain Registration** then **Register Domains**
3. Search for the domain name you want, for example, `yourname.com`. If your preferred name is unavailable, consider alternatives such as `.me`, `.dev`, or adding a middle initial.
4. Select your preferred domain and click **Purchase**
5. Complete payment. `.com` domains typically cost around $10 to $12 USD per year. Pricing varies by region and currency.

After completing payment, Cloudflare will send a confirmation email to your registered address. The domain will appear in your dashboard within a few minutes.

---

## What you should see

After completing the purchase:

- Your domain appears in the Cloudflare dashboard under **Domain Registration**
- A DNS zone is created automatically under **DNS** in the left sidebar
- You receive a confirmation email from Cloudflare

You do not need to do anything additional at this stage. The DNS zone will not have any custom records until you add them in Part 3.

> **Important:** ICANN, the governing body for domain registration, requires you to verify your email address within 15 days of registering a new domain. Cloudflare will send a verification email immediately after purchase. Click the verification link as soon as it arrives. If you miss the 15-day window, your domain will be suspended until you complete verification.

If your domain does not appear within a few minutes, refresh the dashboard. Domain registration confirmation is sometimes delayed by a few minutes.

---

Move to [DNS Configuration](part-3-dns-configuration.md) to continue.

---

*Written by Douglas Ebhoman, a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.*
*[douglasebhoman.com](https://douglasebhoman.com) · [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)*
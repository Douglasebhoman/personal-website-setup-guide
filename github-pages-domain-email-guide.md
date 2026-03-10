# How to Build a Personal Website with a Custom Domain and Professional Email

A practical guide to GitHub Pages, Cloudflare, and Gmail — including every problem you are likely to run into.

---

## What This Guide Covers

By the end of this guide you will have:

- A live website hosted for free on GitHub Pages
- A custom domain (for example, `yourname.com`) pointing to that site
- HTTPS enabled automatically
- A professional email address (`you@yourname.com`) that sends and receives through Gmail

This guide assumes no prior experience with GitHub, DNS, or email configuration. Every step is explained from scratch.

---

## What You Will Need

- A GitHub account — free at [github.com](https://github.com)
- A Cloudflare account — free at [cloudflare.com](https://cloudflare.com)
- A Gmail account
- A domain name purchased through Cloudflare Registrar (covered in Part 2)
- A basic HTML file for your website, or willingness to create one

---

## Part 1 — Create a GitHub Pages Site

### Step 1 — Create a new repository

1. Log into GitHub and click the **+** icon in the top-right corner
2. Select **New repository**
3. Name the repository exactly: `yourusername.github.io` — replacing `yourusername` with your actual GitHub username. This naming convention is required for GitHub Pages to work
4. Set visibility to **Public**
5. Click **Create repository**

> **Why the name matters:** GitHub treats a repository named `yourusername.github.io` as a special Pages repository. Any other name will not activate the root Pages URL automatically.

---

### Step 2 — Add your HTML file

1. Inside your new repository, click **Add file → Create new file**
2. Name the file `index.html`
3. Add your HTML content — even a minimal file works to start:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Your Name</title>
</head>
<body>
  <h1>Hello, I'm Your Name</h1>
</body>
</html>
```

4. Scroll down and click **Commit changes**

> **Why `index.html` specifically:** When a browser visits a URL without specifying a file, the server looks for `index.html` by default. If your file is named anything else — `home.html`, `main.html` — GitHub Pages will not know what to serve and the site will return a 404 error.

---

### Step 3 — Enable GitHub Pages

1. Go to your repository's **Settings** tab
2. In the left sidebar, click **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Under **Branch**, select `main` and leave the folder set to `/ (root)`
5. Click **Save**

GitHub will display a message: *"Your site is live at `https://yourusername.github.io`"*

---

### Troubleshooting — GitHub Pages setup

**Problem: Site not showing after enabling Pages**

This is almost always a timing issue. GitHub Pages does not go live instantly — it can take between 2 and 10 minutes after you enable it. Wait a few minutes, then hard-refresh your browser (`Ctrl + Shift + R` on Windows, `Cmd + Shift + R` on Mac).

If it still does not appear after 10 minutes:
- Confirm the branch is set to `main` (not `master` or any other branch)
- Confirm your file is named exactly `index.html` — not `Index.html` or `index.HTML`
- Go to the **Actions** tab in your repository and check whether the Pages deployment workflow completed successfully. A red ✗ means something failed — click it to read the error.

**Problem: 404 error on the live URL**

A 404 after the site has been enabled almost always means one of two things:

1. **The file is in the wrong location.** Your `index.html` must be in the root of the repository, not inside a subfolder. If it is inside a folder called `src/` or `public/`, GitHub Pages will not find it unless you configure the source folder accordingly in Settings → Pages.

2. **The wrong branch is selected.** Double-check Settings → Pages and confirm the branch shown is the one your `index.html` is committed to. If you committed to `main` but Pages is set to deploy from `master`, it will serve nothing.

---

## Part 2 — Purchase a Domain on Cloudflare

### Step 1 — Register a domain

1. Log into your Cloudflare account at [dash.cloudflare.com](https://dash.cloudflare.com)
2. In the left sidebar, click **Domain Registration → Register Domains**
3. Search for the domain name you want (for example, `yourname.com`)
4. Select your preferred domain and click **Purchase**
5. Complete payment — `.com` domains typically cost around $10–12 per year

> **Why Cloudflare Registrar:** Cloudflare sells domains at cost with no markup, and since your DNS will also be managed through Cloudflare, the setup is simpler. There is no need to transfer DNS to a separate provider.

Once the purchase is complete, Cloudflare automatically creates a DNS zone for your domain. You will manage all DNS records from here.

---

## Part 3 — Link Your Domain to GitHub Pages

This is the section most people find confusing. It requires changes in two places — Cloudflare and GitHub — and they must be done in the right order.

### Step 1 — Add DNS records in Cloudflare

1. In the Cloudflare dashboard, click on your domain
2. Click **DNS → Records**
3. Add the following records one by one:

**Four A records** (these point your root domain to GitHub's servers):

| Type | Name | Content | Proxy status |
|------|------|---------|--------------|
| A | `@` | `185.199.108.153` | DNS only |
| A | `@` | `185.199.109.153` | DNS only |
| A | `@` | `185.199.110.153` | DNS only |
| A | `@` | `185.199.111.153` | DNS only |

**One CNAME record** (this handles the `www` version of your domain):

| Type | Name | Content | Proxy status |
|------|------|---------|--------------|
| CNAME | `www` | `yourusername.github.io` | DNS only |

> **Critical: every record must be set to DNS only (grey cloud).** If any record shows the orange Cloudflare proxy cloud, your HTTPS certificate will not issue correctly. See the troubleshooting section below for why this happens.

---

### Step 2 — Add your custom domain in GitHub

1. Go to your repository on GitHub
2. Click **Settings → Pages**
3. Under **Custom domain**, type your domain name: `yourname.com`
4. Click **Save**

GitHub will run a DNS check. If the records are correct, it will accept the domain. If it shows an error, wait 5 minutes and try again — DNS changes are not always instant.

---

### Step 3 — Enable HTTPS

1. Still in Settings → Pages, wait for the **HTTPS certificate** section to appear
2. Once it shows the certificate as issued, tick **Enforce HTTPS**

> **HTTPS may take up to 24 hours to issue.** This is normal. GitHub uses Let's Encrypt to generate the certificate automatically — it just needs time to verify your DNS records are correctly pointing to GitHub's servers. Do not keep clicking Save or changing settings while waiting — leave it and check back later.

---

### Troubleshooting — Domain and DNS

**Problem: Figuring out which DNS records to add**

GitHub Pages requires four A records pointing to their servers, plus one CNAME for the `www` subdomain. The four IP addresses are:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

These are GitHub's official IP addresses and are unlikely to change, but you can always verify them at [docs.github.com/pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

**Problem: Cloudflare proxy (orange cloud) breaking the connection**

This is one of the most common issues when using Cloudflare with GitHub Pages.

When a DNS record has the orange cloud enabled, Cloudflare proxies all traffic through its own servers. This is useful for performance and security in many situations — but it interferes with the HTTPS certificate that GitHub Pages tries to issue automatically.

The result is usually one of these errors:
- The site loads over HTTP but not HTTPS
- The HTTPS certificate never issues
- The browser shows a security warning

**The fix is simple:** For every DNS record that points to GitHub Pages, click the orange cloud icon and switch it to grey (DNS only). This tells Cloudflare to pass traffic directly to GitHub without proxying it.

After making this change, wait 10–15 minutes and check whether the certificate begins issuing in GitHub Settings → Pages.

**Problem: HTTPS certificate not issuing**

If you have waited more than 24 hours and the certificate still has not issued, work through this checklist in order:

1. **Check the proxy status** — confirm all four A records and the CNAME are set to DNS only (grey cloud) in Cloudflare. This is the cause in the majority of cases.

2. **Check the custom domain field** — in GitHub Settings → Pages, confirm the custom domain is saved and matches your domain exactly (`yourname.com`, not `www.yourname.com`).

3. **Run a DNS check** — go to [dnschecker.org](https://dnschecker.org) and search for your domain. Confirm the A records are resolving to GitHub's four IP addresses from multiple locations. If they are not, your DNS records may not have propagated yet — wait a few more hours.

4. **Remove and re-add the custom domain** — in GitHub Settings → Pages, clear the custom domain field, save, then re-enter it and save again. This forces GitHub to re-run its DNS verification and can restart the certificate issuance process.

---

## Part 4 — Set Up a Professional Email Address

This section covers how to create a professional email address using your custom domain (`you@yourname.com`) without paying for Google Workspace or any other email hosting service. The setup uses Cloudflare Email Routing to receive emails and Gmail SMTP to send them.

---

### How it works

```
Someone sends email to you@yourname.com
        ↓
Cloudflare Email Routing receives it
        ↓
Forwards it to your Gmail inbox
        ↓
You reply from Gmail, but it appears to come from you@yourname.com
```

---

### Step 1 — Enable Cloudflare Email Routing

1. In the Cloudflare dashboard, click on your domain
2. In the left sidebar, click **Email → Email Routing**
3. Click **Get started**
4. Under **Destination addresses**, add your Gmail address and click **Send verification email**
5. Check your Gmail inbox and click the verification link Cloudflare sends
6. Back in Email Routing, under **Routing rules**, click **Create address**
7. In the **Custom address** field, type the prefix you want — for example, `hello` to create `hello@yourname.com`
8. Set the action to **Send to** and select your verified Gmail address
9. Click **Save**

Cloudflare will automatically add the required MX and TXT records to your DNS. You do not need to add these manually.

**Test it:** Send an email to your new address from any account. It should arrive in your Gmail inbox within a few minutes.

---

### Step 2 — Configure Gmail to send from your custom address

Receiving email is now working. This step allows you to send email from Gmail so it appears to come from your custom domain address.

#### 2a — Generate a Gmail App Password

Gmail requires an App Password (not your regular Gmail password) for this configuration. App Passwords are only available if you have two-factor authentication enabled on your Google account.

1. Go to [myaccount.google.com](https://myaccount.google.com)
2. Click **Security** in the left sidebar
3. Under **How you sign in to Google**, click **2-Step Verification** — enable it if it is not already on
4. Once 2-Step Verification is enabled, go back to the Security page
5. In the search bar at the top of the page, type **App passwords** and click the result

> **Troubleshooting — cannot find App Passwords:** This is the most common issue in this section. The App Passwords option is hidden unless 2-Step Verification is fully enabled. If you recently enabled 2-Step Verification, try signing out of Google and signing back in — this refreshes your account session and makes the option visible. If you still cannot find it, go directly to: [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)

6. In the **App name** field, type something recognisable — for example, `Gmail SMTP yourname.com`
7. Click **Create**
8. Google will display a 16-character password. **Copy this immediately** — it will not be shown again. Save it somewhere temporarily.

---

#### 2b — Add your custom address to Gmail

1. In Gmail, click the **Settings gear** → **See all settings**
2. Click the **Accounts and Import** tab
3. Under **Send mail as**, click **Add another email address**
4. A window will open. Fill in:
   - **Name:** Your name as you want it to appear
   - **Email address:** `you@yourname.com`
   - Leave **Treat as an alias** unticked
5. Click **Next Step**
6. Fill in the SMTP settings:
   - **SMTP Server:** `smtp.gmail.com`
   - **Port:** `587`
   - **Username:** Your full Gmail address (not your custom domain address)
   - **Password:** The 16-character App Password you just generated
   - Select **Secured connection using TLS**
7. Click **Add Account**

---

#### 2c — Configure reply behaviour

Once the address is added, there is one more setting to configure to ensure replies always go out from the correct address.

1. Still on the **Accounts and Import** tab, find the **When replying to a message** section
2. Select **Reply from the same address the message was sent to**
3. Next to `you@yourname.com`, click **make default**

> **Why this matters:** If you leave the default set to your Gmail address, any reply you send will appear to come from your personal Gmail rather than your professional address — even if the original email was sent to your custom domain. Changing these two settings ensures your professional address is used consistently.

---

#### 2d — Verify the address

Gmail will send a confirmation email to your custom domain address. Because Cloudflare Email Routing is already set up, this email will arrive in your Gmail inbox.

1. Find the email from Gmail with the subject **Gmail Confirmation**
2. Click the confirmation link inside it

Your custom domain address is now verified. You can now compose emails in Gmail and select `you@yourname.com` from the **From** dropdown before sending.

---

## Quick Reference — DNS Records

For easy reference, here are all the DNS records this guide requires.

**GitHub Pages (add in Cloudflare DNS):**

| Type | Name | Content | Proxy |
|------|------|---------|-------|
| A | `@` | `185.199.108.153` | DNS only |
| A | `@` | `185.199.109.153` | DNS only |
| A | `@` | `185.199.110.153` | DNS only |
| A | `@` | `185.199.111.153` | DNS only |
| CNAME | `www` | `yourusername.github.io` | DNS only |

**Email Routing (added automatically by Cloudflare):**

Cloudflare adds the MX and TXT records for Email Routing automatically when you enable it. You do not need to add these manually.

---

## Summary

| What | How |
|------|-----|
| Website hosting | GitHub Pages — free, no server required |
| Domain registration | Cloudflare Registrar — at-cost pricing |
| DNS management | Cloudflare DNS — grey cloud (DNS only) for all GitHub records |
| HTTPS | Issued automatically by GitHub via Let's Encrypt |
| Email receiving | Cloudflare Email Routing → forwards to Gmail |
| Email sending | Gmail SMTP with App Password |

The entire system is free except for the domain registration itself, which costs approximately $10–12 per year for a `.com` domain.

---

*Written by Douglas Ebhoman — Technical Writer & Documentation Specialist*
*[douglasebhoman.com](https://douglasebhoman.com)*

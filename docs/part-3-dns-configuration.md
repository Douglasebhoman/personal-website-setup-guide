# Part 3: DNS Configuration

This page is part of the Personal Website Setup Guide. If you are joining mid-series, start at the [Home page](index.md).

---

DNS configuration connects your custom domain to GitHub Pages. This requires changes in Cloudflare and in GitHub, in that order.

---

## Step 1: Add DNS records in Cloudflare

1. In the Cloudflare dashboard, click on your domain
2. Click **DNS** then **Records**
3. Add the following records one by one:

**Four A records. These point your root domain to GitHub's servers:**

> **Note:** In DNS records, `@` represents your root domain (for example, `yourname.com`). Do not type your actual domain name in the Name field. Type `@` exactly as shown.

| Type | Name | Content | Proxy status |
|------|------|---------|-------------|
| A | @ | 185.199.108.153 | DNS only |
| A | @ | 185.199.109.153 | DNS only |
| A | @ | 185.199.110.153 | DNS only |
| A | @ | 185.199.111.153 | DNS only |

**One CNAME record. This handles the www version of your domain:**

> **Note:** Replace `yourusername.github.io` in the Content field with your actual GitHub Pages URL before saving.

| Type | Name | Content | Proxy status |
|------|------|---------|-------------|
| CNAME | www | yourusername.github.io | DNS only |

> **Critical:** Every record must be set to **DNS only** (grey cloud). If any record shows the orange Cloudflare proxy cloud, your HTTPS certificate will not issue correctly. See the [Troubleshooting](troubleshooting.md) page for why this happens and how to fix it.

---

## Step 2: Add your custom domain in GitHub

1. Go to your repository on GitHub
2. Click **Settings** then **Pages**
3. Under **Custom domain**, type your domain name: `yourname.com`
4. Click **Save**

GitHub will run a DNS check. DNS changes typically propagate within a few minutes but can take up to 48 hours in some regions. If the check fails immediately, wait 5 minutes and try again.

If the records are correct, GitHub will display a confirmation message and your custom domain will appear saved below the input field.

> **Pro-tip:** While waiting for DNS to propagate, visit [dnschecker.org](https://dnschecker.org) and search for your domain. You will see checkmarks turning green across different global locations as your records propagate. It gives you something active to monitor rather than refreshing the GitHub settings page.

> **Note:** GitHub handles the redirect between `www.yourname.com` and `yourname.com` automatically. If you enter the root domain in GitHub and have the CNAME set up in Cloudflare, both versions of your domain will work without any additional configuration.

---

## Step 3: Enable HTTPS

1. Still in **Settings** then **Pages**, wait for the HTTPS certificate section to appear
2. Once it shows the certificate as issued, tick **Enforce HTTPS**

The certificate section will show a green checkmark and the text "Certificate is active" once it has issued successfully.

> **Note:** HTTPS may take up to 24 hours to issue. This is normal. GitHub uses Let's Encrypt to generate the certificate automatically. It needs time to verify your DNS records are correctly pointing to GitHub's servers. Do not keep clicking Save or changing settings while waiting. Leave it and check back later.

---

## What you should see

After completing all three steps and waiting for HTTPS to issue, visiting `https://yourname.com` should display your website with a padlock icon in the browser address bar confirming the connection is secure.

If the certificate is not issuing or the domain is not connecting correctly, see the [Troubleshooting](troubleshooting.md) page.

---

Move to [Professional Email](part-4-professional-email.md) to continue.

---

*Written by Douglas Ebhoman, a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.*
*[douglasebhoman.com](https://douglasebhoman.com) · [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)*
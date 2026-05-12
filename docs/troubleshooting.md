# Troubleshooting

This page is part of the Personal Website Setup Guide. If you are joining mid-series, start at the [Home page](index.md).

---

This page consolidates solutions to the most common problems at each stage of the setup. Find the section that matches where you are in the guide.

---

## Domain Registration

### Domain suspended after registration

If your domain stops working shortly after registration, the most likely cause is an unverified ICANN email.

ICANN requires you to verify your email address within 15 days of registering a new domain. Cloudflare sends a verification email immediately after purchase. If you did not click the verification link in time, your domain will be suspended.

**The fix:**

1. Log into your Cloudflare dashboard at [dash.cloudflare.com](https://dash.cloudflare.com)
2. Click on your domain
3. Look for a banner or notification about email verification
4. Cloudflare will allow you to resend the verification email from the dashboard
5. Click the verification link in the new email

Your domain should be restored within a few minutes of verification.

---

## GitHub Pages

### Site not showing after enabling Pages

This is almost always a timing issue. GitHub Pages does not go live instantly. It can take between 2 and 10 minutes after you enable it. Wait a few minutes, then hard-refresh your browser (`Ctrl + Shift + R` on Windows, `Cmd + Shift + R` on Mac).

If it still does not appear after 10 minutes, check the following:

- Confirm the branch is set to `main` (not `master` or any other branch)
- Confirm your file is named exactly `index.html`. File names are case-sensitive on GitHub's servers. `Index.html` and `index.HTML` will not work.
- Go to the **Actions** tab in your repository and check whether the Pages deployment workflow completed successfully. A red X means something failed. Click it to read the error.

---

### 404 error on the live URL

A 404 after the site has been enabled means one of the following:

**The file is in the wrong location.** Your `index.html` must be in the root of the repository, not inside a subfolder. If it is inside a folder called `src/` or `public/`, GitHub Pages will not find it unless you configure the source folder in Settings, then Pages.

**The wrong branch is selected.** Double-check Settings, then Pages, and confirm the branch shown is the one your `index.html` is committed to. If you committed to `main` but Pages is set to deploy from `master`, it will serve nothing.

**The filename has incorrect capitalisation.** GitHub's servers are case-sensitive. A file named `Index.html` or `index.HTML` will not be served as the default page. Rename it to exactly `index.html`.

---

## DNS Configuration

### DNS records required for GitHub Pages

For the full list of required DNS records and their values, see the [Quick Reference](part-5-quick-reference.md) page.

---

### Cloudflare proxy breaking the connection

This is one of the most common issues when using Cloudflare with GitHub Pages.

When a DNS record has the orange cloud enabled, Cloudflare proxies all traffic through its own servers. This interferes with the HTTPS certificate that GitHub Pages tries to issue automatically.

The result is usually one of these errors:

- The site loads over HTTP but not HTTPS
- The HTTPS certificate never issues
- The browser shows a security warning

**The fix:** For every DNS record that points to GitHub Pages, click the orange cloud icon and switch it to grey (DNS only). This tells Cloudflare to pass traffic directly to GitHub without proxying it.

After making this change, wait 10 to 15 minutes and check whether the certificate begins issuing in GitHub Settings, then Pages.

---

### HTTPS certificate not issuing

If you have waited more than 24 hours and the certificate still has not issued, work through this checklist in order:

1. **Check the proxy status.** Confirm all four A records and the CNAME are set to DNS only (grey cloud) in Cloudflare. This is the cause in the majority of cases.

2. **Check the custom domain field.** In GitHub Settings, then Pages, confirm the custom domain is saved and matches your domain exactly (`yourname.com`, not `www.yourname.com`).

3. **Run a DNS check.** Go to [dnschecker.org](https://dnschecker.org) and search for your domain. Confirm the A records are resolving to GitHub's four IP addresses from multiple locations. If they are not, your DNS records may not have propagated yet. DNS changes work like a broadcast: Cloudflare updates its records immediately, but every server around the world needs time to receive that update. This is normal and not a sign that something is wrong. Wait a few more hours.

4. **Remove and re-add the custom domain.** In GitHub Settings, then Pages, clear the custom domain field and save. Then re-enter it and save again. This forces GitHub to re-run its DNS verification and can restart the certificate issuance process.

---

## Professional Email

### Cannot find App Passwords in Google Account

The App Passwords option is hidden unless 2-Step Verification is fully enabled on your Google account.

If you recently enabled 2-Step Verification, try signing out of Google and signing back in. This refreshes your account session and makes the option visible.

If you still cannot find it, go directly to: [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)

---

### Email not arriving at custom address

If emails sent to `you@yourname.com` are not arriving in your Gmail inbox, check the following:

- Check your Gmail spam folder. Forwarded emails occasionally trigger spam filters on first delivery.
- Confirm Email Routing is enabled in the Cloudflare dashboard under Email, then Email Routing.
- Confirm the routing rule is active and points to your verified Gmail address.
- Confirm the destination Gmail address is verified. Unverified addresses will not receive forwarded email.
- Check the Cloudflare Email Routing logs for any delivery errors.

---

### Gmail showing personal address instead of custom address when replying

This happens when the reply behaviour setting is not configured correctly.

In Gmail, go to Settings, then Accounts and Import. Under **When replying to a message**, select **Reply from the same address the message was sent to**. Also confirm that `you@yourname.com` is set as the default sending address in the same section.

---

### SMTP authentication failing when adding address to Gmail

The most common cause is using your regular Gmail password instead of an App Password.

Gmail requires an App Password specifically for this configuration. Your regular password will not work even if it is correct. Generate a new App Password at [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords) and use that instead.

If authentication still fails after using an App Password, your network may be blocking port 587. Try switching to port 465 with SSL instead.

---

If your problem is not listed here, raise an issue on the [GitHub repository](https://github.com/Douglasebhoman/personal-website-setup-guide) with a description of the problem, what you expected to happen, and what actually happened.

---

*Written by Douglas Ebhoman, a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.*
*[douglasebhoman.com](https://douglasebhoman.com) · [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)*
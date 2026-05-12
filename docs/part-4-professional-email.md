# Part 4: Professional Email

This page is part of the Personal Website Setup Guide. If you are joining mid-series, start at the [Home page](index.md).

---

This part covers setting up a professional email address using your custom domain (you@yourname.com) without paying for Google Workspace or any other email hosting service. This setup is completely free.

The setup uses Cloudflare Email Routing to receive emails and Gmail SMTP to send them.

---

## How it works

```
Someone sends email to you@yourname.com
        ↓
Cloudflare Email Routing receives it
        ↓
Forwards it to your Gmail inbox
        ↓
You reply from Gmail, appearing to send from you@yourname.com
```

---

## Step 1: Enable Cloudflare Email Routing

1. In the Cloudflare dashboard, click on your domain
2. In the left sidebar, click **Email** then **Email Routing**
3. Click **Get started**
4. Under **Destination addresses**, add your Gmail address and click **Send verification email**
5. Check your Gmail inbox and click the verification link Cloudflare sends
6. Back in Email Routing, under **Routing rules**, click **Create address**
7. In the **Custom address** field, type the part of the email address that comes before the @ symbol. For example, type `hello` to create `hello@yourname.com`.
8. Set the action to **Send to** and select your verified Gmail address
9. Click **Save**
10. Send an email to your new address from any account to confirm it arrives in your Gmail inbox within a few minutes.

Cloudflare will automatically add the required MX and TXT records to your DNS. You do not need to add these manually. The records Cloudflare adds include an SPF record, which helps prevent your professional emails from being marked as spam by recipients.

---

## Step 2: Configure Gmail to send from your custom address

Receiving email is now working. This step allows you to send email from Gmail so it appears to come from your custom domain address.

### 2a: Generate a Gmail App Password

Gmail requires an App Password for this configuration. App Passwords are only available if you have two-factor authentication enabled on your Google account.

1. Go to [myaccount.google.com](https://myaccount.google.com)
2. Click **Security** in the left sidebar
3. Under **How you sign in to Google**, click **2-Step Verification** and enable it if it is not already on
4. Once 2-Step Verification is enabled, go back to the Security page

> **Note:** The App Passwords option is hidden unless 2-Step Verification is fully enabled. If you recently enabled 2-Step Verification, try signing out of Google and signing back in. This refreshes your account session and makes the option visible. If you still cannot find it, go directly to: [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)

5. In the search bar at the top of the page, type **App passwords** and click the result
6. In the **App name** field, type something recognisable, for example, `Gmail SMTP yourname.com`
7. Click **Create**
8. Google will display a 16-character password. Copy this immediately. It will not be shown again.

> **Security note:** Store your App Password in a password manager. If you lose it, you cannot view it again. You will need to delete it and generate a new one at [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords).

---

### 2b: Add your custom address to Gmail

1. In Gmail, click the **Settings gear** then **See all settings**
2. Click the **Accounts and Import** tab
3. Under **Send mail as**, click **Add another email address**
4. A window will open. Fill in:
   - **Name:** Your name as you want it to appear
   - **Email address:** you@yourname.com
   - Leave **Treat as an alias** unticked. Leaving this unticked ensures Gmail sends from your custom address directly rather than treating it as a forwarding alias.
5. Click **Next Step**
6. Fill in the SMTP settings:
   - **SMTP Server:** smtp.gmail.com
   - **Port:** 587
   - **Username:** Your full Gmail address (not your custom domain address)
   - **Password:** The 16-character App Password you generated in Step 2a
   - Select **Secured connection using TLS**
7. Click **Add Account**

> **Note:** If port 587 with TLS fails due to network restrictions, use port 465 with SSL as an alternative.

---

### 2c: Configure reply behaviour

1. Still on the **Accounts and Import** tab, find the **When replying to a message** section
2. Select **Reply from the same address the message was sent to**
3. Next to `you@yourname.com`, click **make default**

> **Why this matters:** If you leave the default set to your Gmail address, any reply you send will appear to come from your personal Gmail rather than your professional address, even if the original email was sent to your custom domain. Changing these two settings ensures your professional address is used consistently.

---

### 2d: Verify the address

Gmail will send a confirmation email to your custom domain address. Because Cloudflare Email Routing is already set up, this email will arrive in your Gmail inbox.

1. Find the email from Gmail with the subject **Gmail Confirmation**
2. Click the confirmation link inside it

Verification is usually instant. If Gmail does not confirm immediately, wait a few minutes and check again.

Your custom domain address is now verified. You can compose emails in Gmail and select `you@yourname.com` from the From dropdown before sending.

---

## What you should see

After completing all steps in this part:

- Emails sent to `you@yourname.com` arrive in your Gmail inbox
- You can compose a new email in Gmail, select `you@yourname.com` from the From dropdown, and send it
- Recipients see your custom domain address, not your Gmail address

If email routing or SMTP is not working as expected, see the [Troubleshooting](troubleshooting.md) page.

---

Your setup is complete. See the [Quick Reference](part-5-quick-reference.md) page for all configuration values in one place.

---

*Written by Douglas Ebhoman, a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.*
*[douglasebhoman.com](https://douglasebhoman.com) · [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)*
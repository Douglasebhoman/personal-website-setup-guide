# Part 1: GitHub Pages

This page is part of the Personal Website Setup Guide. If you are joining mid-series, start at the [Home page](index.md).

---

GitHub Pages is a free hosting service built into GitHub. It serves your HTML files directly from a repository as a live website. No server configuration, no hosting fees, no build step required.

This part covers creating the repository, adding your HTML file, and enabling GitHub Pages.

---

## Step 1: Create a new repository

1. Log into GitHub and click the **+** icon in the top-right corner
2. Select **New repository**
3. Name the repository exactly: `yourusername.github.io`, replacing `yourusername` with your actual GitHub username. This naming convention is required for GitHub Pages to work.
4. Set visibility to **Public**
5. Click **Create repository**

> **Why the name matters:** GitHub treats a repository named `yourusername.github.io` as a special Pages repository. Any other name will not activate the root Pages URL automatically.

---

## Step 2: Add your HTML file

> **Note:** If you initialised the repository with a README file during setup, the file will already appear in the repository. Click **Add file** to add your `index.html` alongside it.

1. Inside your new repository, click **Add file** then **Create new file**
2. Name the file `index.html`
3. Add your HTML content. A minimal file works to start:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Your Name</title>
</head>
<body>
  <h1>Hello, I am Your Name</h1>
</body>
</html>
```

4. Scroll down and click **Commit changes**

> **Why index.html specifically:** When a browser visits a URL without specifying a file, the server looks for `index.html` by default. If your file is named anything other than `index.html`, GitHub Pages will not know what to serve and the site will return a 404 error.

---

## Step 3: Enable GitHub Pages

1. Go to your repository **Settings** tab
2. In the left sidebar, click **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Under **Branch**, select `main` and leave the folder set to `/ (root)`
5. Click **Save**

GitHub will display a message: "Your site is live at `https://yourusername.github.io`"

The message appears immediately, but the site itself may take a few minutes to become accessible. Wait a few minutes, then open your browser and visit `https://yourusername.github.io` to confirm the site is live.

If it is not appearing after 10 minutes, hard-refresh your browser (`Ctrl + Shift + R` on Windows, `Cmd + Shift + R` on Mac).

---

## What you should see

After enabling GitHub Pages and waiting a few minutes, visiting `https://yourusername.github.io` should display your HTML file rendered in the browser.

If the site is not appearing after 10 minutes, see the [Troubleshooting](troubleshooting.md) page.

---

Move to [Domain Registration](part-2-domain-registration.md) to continue.

---

*Written by Douglas Ebhoman, a technical writer based in Prague who builds documentation systems for DevTools and SaaS companies.*
*[douglasebhoman.com](https://douglasebhoman.com) · [LinkedIn](https://linkedin.com/in/douglas-ebhoman-757329289)*
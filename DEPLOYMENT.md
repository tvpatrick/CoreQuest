# Deploying CoreQuest to GitHub Pages
## A click-by-click walkthrough — no command line required

This takes the contents of this folder from your computer to a live website at www.corequest.net, hosted free on GitHub Pages. Total active time: about 20 minutes, plus DNS waiting time. Your current IONOS site stays live until Step 6, so there is no downtime.

**Before you start, check one thing at IONOS:** if you have any email addresses on the corequest.net domain, confirm with IONOS that the email service is separate from (or survives cancellation of) your MyWebsite NOW / hosting product. Do not cancel anything until Step 8.

---

## Step 1 — Create the repository

1. Log in at github.com (or create a free account).
2. Click the **+** in the top-right corner → **New repository**.
3. Repository name: `corequest`
4. Description: `A free workshop method for supercharging your Human/AI partnership.`
5. Visibility: **Public** (required for free GitHub Pages, and the point of a CC BY-SA project).
6. Do NOT check "Add a README" (you're uploading your own).
7. Click **Create repository**.

## Step 2 — Upload the files

1. On the new empty repository page, click the link that says **uploading an existing file**.
2. Open the unzipped CoreQuest folder on your computer. Select ALL of its contents — index.html, session.html, README.md, LICENSE.md, DEPLOYMENT.md, and the `downloads` and `images` folders — and drag them onto the GitHub upload area. (Drag the folders themselves; GitHub preserves the folder structure.)
3. In the "Commit changes" box at the bottom, type: `Initial upload of CoreQuest site and kit`
4. Click **Commit changes** and wait for the upload to finish.

Your repository front page should now show the README rendered as a formatted page. Every file is now versioned: any future change to any file is recorded permanently with a date and note.

## Step 3 — Turn on GitHub Pages

1. In the repository, click **Settings** (top menu) → **Pages** (left sidebar).
2. Under "Build and deployment," Source: **Deploy from a branch**.
3. Branch: **main**, folder: **/ (root)**. Click **Save**.
4. Wait a minute or two, then refresh the page. A banner appears: "Your site is live at `https://YOURUSERNAME.github.io/corequest/`".

## Step 4 — Test the temporary address

Visit that github.io address and click through everything: the hero image loads, the workshop accordions open, the Copy prompt button works, the download buttons deliver the Markdown files, and the Team Session link opens the Session tool. This is your dress rehearsal — the site at your real domain will behave identically.

## Step 5 — Tell GitHub about your domain

1. Back in **Settings → Pages**, find **Custom domain**.
2. Enter: `www.corequest.net` and click **Save**. (This creates a small CNAME file in your repository — that's expected.)
3. GitHub will show a DNS warning until Step 6 is done. That's normal.

## Step 6 — Point the domain at GitHub (at IONOS)

1. Log in to IONOS → **Domains & SSL** → corequest.net → **DNS**.
2. Add or edit these records (delete any existing A or CNAME records for `www` and the bare domain that point at IONOS hosting):

   **CNAME record**
   - Host/Name: `www`
   - Points to: `YOURUSERNAME.github.io` (your actual GitHub username, no /corequest)

   **Four A records** (these make the bare corequest.net work too)
   - Host/Name: `@`
   - Values (create one A record for each):
     - `185.199.108.153`
     - `185.199.109.153`
     - `185.199.110.153`
     - `185.199.111.153`

   *These IP addresses are GitHub's published Pages servers. If anything looks off, verify the current values at: docs.github.com → Pages → "Managing a custom domain".*

3. Leave any MX (email) records untouched.
4. Save. DNS changes usually take effect within an hour, occasionally up to 24.

## Step 7 — Turn on HTTPS

Once GitHub's DNS warning in Settings → Pages clears (give it an hour or so):

1. Check the **Enforce HTTPS** box in Settings → Pages.
2. Visit https://www.corequest.net — your site, secure, live, free.

## Step 8 — Clean up at IONOS

Only after the new site has been live and stable for a few days:

1. Cancel the MyWebsite NOW / website builder product.
2. KEEP the domain registration (corequest.net itself) — that stays at IONOS and just renews annually as before.
3. Keep any email product you use, per your Step-0 check.

## Ongoing: how to edit the site later

1. In the repository, click any file (e.g., index.html or a kit file in `downloads/`).
2. Click the **pencil icon** (top right of the file view).
3. Make your edit, scroll down, write a one-line note about what changed, click **Commit changes**.
4. The live site updates within a minute or two. The old version stays in the history forever.

## Ongoing: feedback and contributions

- **Issues** (repository top menu) is your public inbox — people ask questions and report problems there, others can answer, and nothing implies a reply deadline. You'll get email notifications you can triage whenever you're back from the trail.
- **Pull requests** are proposed changes from others. GitHub shows you exactly what would change; you click **Merge** to accept or close to decline. The contributor's name attaches to the change permanently — attribution by format, at platform scale.
- Optional: Settings → General → Features → check **Discussions** if you'd like a forum-style space separate from bug reports.

# Competitor Analysis: AI in Prenatal Ultrasound

An interactive, single-page report on the AI startups and OEM platforms building quality
assurance and risk prediction for prenatal ultrasound. Built to be shared with colleagues
as a website via GitHub Pages.

The whole report is one file: **`index.html`**. Demo videos are embedded from YouTube and
product screenshots load from each company's own website, so viewers need an internet
connection for the visuals to appear.

---

## Access (login)

The report is gated. To open it a viewer must enter an **authorized company email** and the
**access password**. These credentials are shared separately and are deliberately **not**
stored in this repository.

How it works and how secure it is:

- The report content is **AES-256 encrypted** inside `index.html`. Until the correct password
  is entered, the text is not present in the page source, only ciphertext is. The password is
  never stored in the file; it is used to derive the decryption key in the browser
  (PBKDF2-SHA-256, then AES-GCM via the Web Crypto API).
- This is meaningful protection against casual access and against someone reading the page
  source, which a plain JavaScript password check would not provide.
- **Honest limits:** it is a single shared password, so anyone given it can open the report,
  and the company-email requirement is a front-end gate only (it is not part of the encryption
  key). For per-person accounts, revocation, or an audit trail, host instead on a platform with
  real authentication (Cloudflare Access, Netlify Identity, or an internal server).
- To change the password or the allowed email domain later, the file must be regenerated (both
  are baked in), so ask for a fresh build rather than editing by hand.

---

## Option A: Publish with the GitHub website (no command line)

1. Go to https://github.com/new and create a new repository. Set it to **Public** (required for
   free GitHub Pages) and click **Create repository**.
2. On the new repo page, click **uploading an existing file**.
3. Drag in the contents of this folder: `index.html`, `README.md`, and `.nojekyll`
   (the `.nojekyll` file may be hidden in Finder; press `Cmd + Shift + .` to show hidden files).
   Click **Commit changes**.
4. Go to **Settings -> Pages**. Under **Build and deployment -> Source**, choose
   **Deploy from a branch**. Set branch to **main** and folder to **/ (root)**. Click **Save**.
5. Wait about one minute, then refresh. GitHub shows the live URL, which will look like:
   `https://YOUR-USERNAME.github.io/YOUR-REPO/`
6. Share that link plus the credentials with colleagues. To update the report later, edit or
   re-upload `index.html` and the site refreshes automatically.

---

## Option B: Publish with git (command line)

```bash
cd "competitor-analysis-site"
git init
git add .
git commit -m "Competitor analysis report"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO.git
git push -u origin main
```

Then in the repo: **Settings -> Pages -> Source -> Deploy from a branch -> main -> / (root) -> Save.**
The live URL appears within a minute.

---

## Notes

- **Only upload this folder.** Publish just the three files in `competitor-analysis-site/`
  (`index.html`, `README.md`, `.nojekyll`). An unprotected, plaintext master copy of the report
  sits one level up (`Competitor_Analysis_Prenatal_Ultrasound_MASTER.html`) for editing; do not
  put that file in the public repo, or the gate is moot.
- **Keep credentials out of the repo.** Share the email domain and password with colleagues
  directly (chat, password manager), not in any committed file.
- **`.nojekyll`** tells GitHub Pages to serve the files as-is (it skips Jekyll processing).
  Keep it in the repo.
- **Custom domain:** optional, in Settings -> Pages.
- **Private sharing:** a free GitHub Pages site is reachable by anyone with the link (the login
  still gates the content). For true access control, use Cloudflare Access, Netlify Identity, or
  an internal host.
- **If a video shows "unavailable":** that video has embedding disabled by its owner; a
  "Watch on YouTube" link sits directly beneath each video as a fallback.
- **If a screenshot does not load:** the vendor changed or blocked the image URL. Broken images
  are hidden automatically and the product link beside them still works.

Compiled June 2026.

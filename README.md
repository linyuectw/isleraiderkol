# Isle Raider KOL landing page — deploy guide

Contents
- `index.html` — the landing page (single file)
- `assets/` — images
- `apps-script/Code.gs` — receives applications, saves them to a Google Sheet and emails linyue.ctw@gmail.com
- `.nojekyll` — tells GitHub Pages to serve files as-is

## Step 1. Create the receiver (Google Apps Script) — about 5 minutes
1. In Google Drive create a new **Google Sheet** (name it e.g. "Isle Raider KOL applications").
2. In the sheet: **Extensions → Apps Script**.
3. Delete the sample code, paste in everything from `apps-script/Code.gs`, click **Save**.
4. Choose the function **testSetup** in the toolbar and click **Run**. Google asks for permission (Sheets + sending mail) — approve it. A test email should arrive at linyue.ctw@gmail.com.
5. Click **Deploy → New deployment → type: Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
6. Deploy, then copy the **Web app URL** (ends with `/exec`).

Applications are sent from the Google account that owns the script, and replies go to the applicant (Reply-To). Free Gmail accounts can send about 100 script emails/day; Google Workspace accounts about 1,500/day.

## Step 2. Connect the page
Open `index.html`, find this line and paste the URL between the quotes:

    var SUBMIT_URL = "";

## Step 3. Publish on GitHub Pages
1. Create a GitHub repository and upload **everything in this folder** (keep `index.html` at the top level).
2. Repo **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main` / `/ (root)` → Save.
3. After a minute the site is live at `https://<user>.github.io/<repo>/`. A custom domain can be added on the same screen.

## Step 4. Test
Submit a test application on the live page. You should get the email and see a new row in the sheet.

## Notes
- If you change `Code.gs` later, use **Deploy → Manage deployments → Edit → New version**; the URL stays the same.
- The Web app URL is visible in the page source (unavoidable for a static site). The script only accepts and stores form data; the honeypot field and length checks reduce spam. If spam becomes a problem, add Cloudflare Turnstile or reCAPTCHA.
- Applicant data lives in your Google Sheet; consider adding a short privacy notice to the page.

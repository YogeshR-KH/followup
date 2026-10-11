# Kamla — Dispatch & Credit Follow-up (app)

Mobile web app for staff to track the follow-up steps after every invoice:
Bill and Ledger shared (credit sales), LR Copy or Receiving shared (proof of dispatch),
and the dispatch call. Each step is recorded with the date and the logged-in staff
member, which feeds the KPI tab used for KRA reviews.

- **Data:** Google Sheet "Dispatch & Credit Follow-up" (Entries, KPI, Rules, TAT, Lists, Users)
- **Backend:** Apps Script web app bound to that sheet (`Code.gs`, kept outside this repo)
- **This repo:** the static page Vercel serves — no build step, no dependencies

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app (HTML + CSS + JS). `API_URL` at the top of the script points to the Apps Script web app. |
| `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png`, `favicon.png` | "Add to Home Screen" name and icons |
| `vercel.json` | Security headers, no-cache (staff always get the latest version), noindex |
| `robots.txt` | Keeps search engines out |

## Deploy (first time)

1. **GitHub:** create a new **private** repository, e.g. `kamla-followup`. Click
   *Add file → Upload files*, drag in every file from this folder, and *Commit changes*.
2. **Vercel:** *Add New → Project → Import* the `kamla-followup` repo.
   Framework preset: **Other**. Leave build and output settings empty. Click *Deploy*.
3. **Domain (optional):** in the Vercel project → *Settings → Domains*, add e.g.
   `f.kamlahoreca.com`. At your DNS provider add a **CNAME** record:
   `f` → `cname.vercel-dns.com`. Vercel issues the SSL certificate automatically.
4. Open the address on a phone, log in, then use *Add to Home Screen*.

## Updating

- **App change:** replace `index.html` in GitHub (*Upload files* again). Vercel redeploys in about a minute.
- **Backend change:** paste the new `Code.gs` in Apps Script, then *Deploy → Manage deployments →
  Edit (pencil) → Version: New version → Deploy*. This keeps the **same** `/exec` URL, so
  `index.html` does not need to change. (Creating a *New deployment* instead gives a new URL,
  which would then have to be pasted into `API_URL`.)

## Notes

- Logins are name + 4-digit PIN from the hidden **Users** tab (owner-only). A login lasts until midnight IST.
- If the backend URL changes, update `API_URL` near the top of the `<script>` in `index.html`.
- Version history and pending decisions: `PENDING-CHANGES.md` (kept with the Apps Script files).

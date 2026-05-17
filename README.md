# shotclock-legal

Static legal pages (privacy policy and imprint, in German) for the Android apps **ShotClock** and **ScoreBoard**, served via GitHub Pages under the custom domain `scoreboard.krabbenfudder.de`. The URL is referenced from the apps' Google Play Store listings.

## Contents

| File          | Purpose                                                |
| ------------- | ------------------------------------------------------ |
| `index.html`  | Landing page with short app descriptions and nav links |
| `privacy.html`| Privacy policy and imprint (combined, valid for both apps) |
| `CNAME`       | Custom domain declaration for GitHub Pages             |
| `README.md`   | This file                                              |

The site uses only system fonts and no external resources (no Google Fonts, no CDN scripts, no trackers). This keeps the privacy policy accurate: the page itself collects nothing beyond what GitHub Pages logs server-side.

## Final URL

- Landing page: `https://scoreboard.krabbenfudder.de/`
- Privacy policy (use this in the Play Console): `https://scoreboard.krabbenfudder.de/privacy.html`

## Deployment

### 1. Create the GitHub repository

1. Create a new public repository on GitHub named `shotclock-legal` under the account `hrkuenstler`.
2. Push the contents of this folder (including the `CNAME` file) to the `main` branch.

### 2. Configure DNS

At your DNS provider for `krabbenfudder.de`, add a CNAME record:

| Field | Value                       |
| ----- | --------------------------- |
| Type  | CNAME                       |
| Name  | scoreboard                  |
| Value | hrkuenstler.github.io.      |
| TTL   | 3600 (or provider default)  |

The trailing dot on `hrkuenstler.github.io.` makes it a fully qualified domain name. Some DNS UIs require it, some add it automatically — either way the record must resolve to the GitHub Pages host.

### 3. Enable GitHub Pages

1. In the repository: **Settings → Pages**.
2. Under **Source**, select **Deploy from a branch**.
3. Choose **Branch: `main`**, **Folder: `/ (root)`**, then **Save**.
4. Under **Custom domain**, GitHub should already show `scoreboard.krabbenfudder.de` (read from the `CNAME` file). If not, enter it manually and click **Save**.
5. Wait for the DNS check to pass (usually a few minutes after DNS propagation).
6. Wait for the Let's Encrypt certificate to be issued (usually under 30 minutes, can take up to 24h).
7. Tick **Enforce HTTPS**. This is required — Google Play rejects HTTP-only policy URLs.

### 4. Verify

Open `https://scoreboard.krabbenfudder.de/privacy.html` in an incognito window. It must load without warnings, without login, and over HTTPS.

## Before publishing

- Replace `[E-Mail-Adresse einfügen]` in `privacy.html` (appears twice: once in the privacy section under "Verantwortlicher", once in the imprint section under "Kontakt") with the contact email address.
- Verify the page renders correctly on mobile — Google Play reviewers check from mobile.
- Confirm the URL is reachable in incognito mode with no login required.

## Updating the policy

When the apps change (e.g. crash reporting is added later, or a default broker is shipped), update `privacy.html` and bump the date under the `<h1>`. Old versions can be kept in Git history; Google Play only requires the current URL to be accurate.

## Legal notes

- The imprint follows `§ 5 DDG` (Digitale-Dienste-Gesetz, the successor to TMG since May 2024) and `§ 18 Abs. 2 MStV`.
- The privacy policy is written for the GDPR (DSGVO) context and is appropriate for an app that does not collect personal data and does not run any backend operated by the developer.
- This is a template prepared for a specific use case. It is **not** legal advice. If the apps' behaviour changes — particularly if any analytics, crash reporting, push notifications, ads, or developer-operated server is added — the policy must be revised accordingly.

# The Coliving Operator Confidence Program

Free monthly workshop registration page. Static single-page site deployed on Netlify.

## Setup

### 1. Configure

Open `index.html` and edit the `CONFIG` object near the bottom of the file:

```js
const CONFIG = {
  REGISTRATION_URL: "https://lu.ma/aj3cajlz",
  WEEKDAY: 3,          // 0=Sun 1=Mon 2=Tue 3=Wed 4=Thu 5=Fri 6=Sat
  WEEK_OF_MONTH: 1,    // 1=first, 2=second, 3=third, 4=fourth
  HOUR: 19,            // 24-hour, in TIMEZONE below
  MINUTE: 0,
  TIMEZONE: "America/Denver",
  TIMEZONE_LABEL: "Mountain Time",
  DURATION_MINUTES: 60,
};
```

- **REGISTRATION_URL** — Your Lu.ma event page. All CTA buttons point here. Lu.ma handles signup, calendar invites, and reminders.
- **Schedule fields** — The page auto-calculates the next session date from these. It rolls forward each month and handles year boundaries. No manual date updates needed.

### 2. Deploy to Netlify

1. Push this repo to GitHub.
2. Go to [app.netlify.com](https://app.netlify.com) > **Add new site** > **Import an existing project**.
3. Connect your GitHub account and select this repository.
4. Leave build settings empty (Netlify uses `netlify.toml`).
5. Click **Deploy site**.

Every push to `main` triggers an automatic redeploy.

### 3. Custom Domain

1. In Netlify: **Site settings** > **Domain management** > **Add custom domain**.
2. Enter your domain (e.g. `workshop.yourdomain.com`).
3. At your DNS provider, add a CNAME record:
   - **Name:** `workshop` (or `@` for apex)
   - **Value:** `your-site-name.netlify.app`
4. Netlify provisions a free SSL certificate automatically.

For apex domains (`yourdomain.com` without a subdomain), use Netlify DNS or an `ALIAS`/`ANAME` record if your registrar supports it.

## Project Structure

```
index.html      Single-page site (HTML + CSS + JS, no dependencies)
netlify.toml    Netlify config: headers, caching, 404 fallback
.gitignore      Standard ignores
README.md       This file
```

## Adding Pages Later

The 404 redirect in `netlify.toml` won't shadow real files. To add a thank-you page or any other route, just create the HTML file (e.g. `thank-you.html`) and it will be served at `/thank-you` automatically.

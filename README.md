# NFC business card

Single-page contact site for an NFC tag. Someone taps the card, this page
opens, and they can save your contact, view your résumé, or reach you.

Everything is inline in one HTML file — no frameworks, no fonts, no CDN,
no build step, no JavaScript, no trackers. The whole page is under 15 KB.

## Files

| File          | Purpose                                                        |
|---------------|----------------------------------------------------------------|
| `index.html`  | The page. All CSS is inline; nothing loads from the network.   |
| `contact.vcf` | vCard 3.0 downloaded by **Save contact**.                      |
| `resume.pdf`  | Your résumé, opened by **View résumé**.                        |
| `.nojekyll`   | Empty file. Tells GitHub Pages to skip Jekyll for fast deploys.|

All links in `index.html` are relative (`contact.vcf`, `resume.pdf`, no
leading slash), so the site works whether it's served from a user site
(`you.github.io`) or a project site (`you.github.io/repo`).

## Deploy to GitHub Pages

1. Create a repo and push these files to the root of the default branch:

   ```bash
   git init
   git add .
   git commit -m "Add NFC contact card"
   git branch -M main
   git remote add origin https://github.com/1destroyer100yt/<repo>.git
   git push -u origin main
   ```

2. In the repo: **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*.
4. Choose branch **main** and folder **/ (root)**, then **Save**.
5. Wait ~1 minute. Your site is at:
   - `https://1destroyer100yt.github.io/` if the repo is named
     `1destroyer100yt.github.io`, or
   - `https://1destroyer100yt.github.io/<repo>/` for any other repo name.

Write that final URL onto the NFC tag with any tag-writer app (e.g.
NFC Tools). Test the tap on a phone before handing out the physical card.

## Update it later

- **Change a link, wording, or color:** edit `index.html` and push. The
  accent color lives in the `--accent` CSS variables near the top (there's
  a light value and a dark-mode value under `prefers-color-scheme: dark`).
- **New résumé:** replace `resume.pdf` (keep the name) and push. Nothing
  else needs to change.
- **Change contact details:** edit them in **both** `index.html` (the
  button links) **and** `contact.vcf` (the saved card), then push.

### Editing `contact.vcf`

It's vCard 3.0 on purpose — iOS parses 3.0 more reliably than 4.0. Keep
these intact:

- `VERSION:3.0`
- Both `N:` (structured: `Last;First;;;`) and `FN:` (display name)
- Phone in E.164 format: `+17343381208`
- Lines end in CRLF (`\r\n`). Most editors preserve this; if a parser
  starts choking, check the line endings first.

## Accessibility & rendering notes

- Dark mode follows the phone's system setting via
  `prefers-color-scheme`; colors are verified for AA contrast in both.
- Every tap target is at least 44 px tall with real spacing between.
- Semantic HTML with a labelled `nav`; works with VoiceOver.
- The page renders with no horizontal scroll at 375 px wide and does not
  break if `resume.pdf` is missing (the link just 404s until you add it).

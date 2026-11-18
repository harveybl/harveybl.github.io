# harveybl.github.io

User-pages site (GitHub Pages, branch `main`, folder `/`, `.nojekyll`). It serves files that shipped apps
and outside services depend on. **Treat every path below as permanent.**

## Do not

- **Never set a custom domain** on this repository (Settings › Pages › Custom domain, or a `CNAME` file).
  On a user site a custom domain redirects all of `harveybl.github.io`, including `/.well-known/`, to that
  domain, and Apple does not follow redirects for the association file. It also moves every **project** site
  served under this host (`/aitodo-legal/`, `/Lease-Exit-Calculator/` and the others).
- **Never make this repository private, archive it, delete it, rename it, or transfer it to another owner.** Each one takes the site
  down, and a freed `harveybl.github.io` name could be claimed by someone else, who would then control a
  page shown in the middle of a bank sign-in and an association file every shipped SAFE Budget build trusts.
- **Never change the Pages settings** (source branch or folder, or switch to a GitHub Actions build).
- **Never remove `.nojekyll`** or add Jekyll configuration. Jekyll skips dot-folders, so `/.well-known/`
  would stop being served.
- **Never add redirects** (meta refresh, JavaScript, or a `404.html` trick) in front of the paths below.
- Also keep the GitHub account `harveybl` itself: renaming or deleting the account has the same effect,
  and an account rename also moves every project site under this host.

## Permanent dependencies

| Path | Used by |
|---|---|
| `/.well-known/apple-app-site-association` | Every shipped SAFE Budget build (iOS and macOS, app ID `7GCG6NK3W3.com.safebudget.app`). Associates `/safebudget/plaid-oauth*` with the app. |
| `/safebudget/plaid-oauth/` (`safebudget/plaid-oauth/index.html`) | The Plaid OAuth redirect address `https://harveybl.github.io/safebudget/plaid-oauth`, compiled into every shipped SAFE Budget build and typed by each Bring-your-own-Plaid customer into their own Plaid Dashboard. Neither can be changed from here. |
| `/.well-known/appspecific/com.tesla.3p.public-key.pem` | Tesla Fleet API partner-account domain verification. The file is a public key and is meant to be public; Tesla requires it to be reachable over plain HTTPS. |
| `/aitodo-legal/*` (separate repo, `harveybl/aitodo-legal`) | Privacy, Terms and Support links compiled into SAFE Budget builds from before the Gallahadd cutover and their store metadata (and possibly AI ToDo Plus builds). Served under this host, so a custom domain or account rename here breaks them too. |

Later SAFE Budget releases add `https://safebudget.gallahadd.com/plaid-oauth`, but they keep this address as a
fallback for customers who registered it. It is never retired.

## What breaks, and how fast

Bank accounts that are already linked keep syncing in every case: the redirect address is used only when a
bank is linked or repaired.

| Change | Effect |
|---|---|
| Association file removed, redirected or served with an error | Apple's CDN copy (`https://app-site-association.cdn-apple.com/a/v1/harveybl.github.io`) refreshes within about a day. A new install picks up the failure at once; existing devices within about a week. From then on, banks that sign in on their own website cannot be linked or repaired in SAFE Budget for every customer using this address. |
| Return page removed | iPhone still returns to the app. Anyone whose browser handles the address sees a GitHub 404 in the middle of a bank sign-in. |
| Custom domain set, repo private/renamed/deleted | Both of the above at once, plus the Tesla verification file. |
| Name claimed by someone else | They control the page and the association file. Phishing and breakage. |

## Checks

```sh
curl -sSI https://harveybl.github.io/.well-known/apple-app-site-association   # expect HTTP/2 200, no Location
curl -sS  https://app-site-association.cdn-apple.com/a/v1/harveybl.github.io  # expect the same JSON
curl -sSIL https://harveybl.github.io/safebudget/plaid-oauth                  # expect 301 to .../plaid-oauth/ then 200
```

## Tesla

The Tesla public key lives at `/.well-known/appspecific/com.tesla.3p.public-key.pem` so Tesla can verify domain
control during partner-account registration. The file is intentionally public: it is a public key, and Tesla
requires it to be reachable over plain HTTPS. See https://developer.tesla.com/docs/fleet-api.

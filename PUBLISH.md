# Publish Rallr privacy

Prepared 4 November 2026. Files are ready locally; nothing has been committed or pushed.

## 1. Commit and push

Run these commands in Terminal:

```sh
cd /private/tmp/rallr-privacy
git switch -C main
git add index.html privacy/index.html privacy/styles.css .nojekyll PUBLISH.md
git diff --cached --check
git commit -m "Add Rallr privacy policy"
git push -u origin main
```

If GitHub asks you to sign in, use your own GitHub login flow; do not share passwords or tokens in chat. If the remote has changed since this empty repository was cloned, stop on a rejected push and reconcile it; do not force push. Git may require your existing author identity to be configured before the first commit. No identity settings have been changed by this work.

## 2. Enable Pages

Open https://github.com/IKiprotich/rallr-privacy/settings/pages

1. Under Build and deployment, set Source to Deploy from a branch.
2. Select main and /(root).
3. Click Save.
4. Open the repository's Actions tab and wait for the Pages deployment to succeed.
5. Return to Settings > Pages and open Visit site.

The empty .nojekyll file lets GitHub publish these static files without Jekyll processing. No package installation or local build is needed. Free GitHub Pages supports public repositories; private repositories require a qualifying plan.

## 3. Check the live link

Open https://ikiprotich.github.io/rallr-privacy/privacy/

Confirm the page shows Privacy policy, Last updated: 4 November 2026, all policy sections and the correct mailto contact. Follow the homepage privacy link too. Check on your phone with light and dark appearance. If it returns 404, confirm main/root, a successful Pages deployment and the exact repository path before retrying.

Optional Terminal check:

```sh
curl -IL https://ikiprotich.github.io/rallr-privacy/privacy/
```

Look for a final 200 response. A status code alone is not proof of the correct content; inspect the page as well.

Send this github.io link back once Pages is deployed so it can be checked publicly and used to update the app's privacy link. App code has not been changed.

## 4. Optional: rallr.app

Only do this if you own rallr.app and want it to serve this site. You do not need a custom domain to publish the policy.

1. In Settings > Pages > Custom domain, enter rallr.app and Save BEFORE changing DNS. GitHub creates a root CNAME file containing only rallr.app when deploying from a branch. Verify the file is present; no https:// or /privacy in it.
2. In your domain provider's DNS panel, set these A records for the apex host (@):

| Type | Host | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Replace conflicting apex website records deliberately. Leave email/MX records alone. Optionally add www as a CNAME to ikiprotich.github.io (no repository path). The repository CNAME file and a DNS CNAME record are different things; the apex setup above uses A records.

3. Wait for GitHub's DNS check and certificate provisioning, then enable Enforce HTTPS in Settings > Pages. DNS/certificate availability can take up to 24 hours.
4. Pull GitHub's generated CNAME commit locally:

```sh
git pull --ff-only origin main
```

5. Verify https://rallr.app/privacy redirects if needed and displays the policy at https://rallr.app/privacy/ over HTTPS. Check the final page, not just DNS.

If adding the CNAME file manually instead, put exactly rallr.app on one line at repository root, commit/push it, and confirm the matching Custom domain setting. Do not add the file before deciding to use your owned domain.

## 5. App Store Connect

Paste the final verified HTTPS policy URL into App Store Connect > your app > App Privacy > Privacy Policy URL, then save. Use the same URL in the app. Use the github.io address if you do not own or are not configuring rallr.app.

## References

- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

# Discord Subdomain Site

Publish this folder as a separate GitHub Pages repository for `discord.teamzenkai.com`.

## Files

- `index.html` serves the Open Graph metadata and redirects to the Discord invite.
- `CNAME` binds the site to `discord.teamzenkai.com`.

## Deploy

1. Create a new GitHub repository for the subdomain site.
2. Copy `index.html` and `CNAME` from this folder into the root of that repository.
3. In GitHub repository settings, enable GitHub Pages from the main branch root.
4. Confirm the custom domain is `discord.teamzenkai.com`.
5. Wait for the Pages certificate to issue before forcing HTTPS.

The Open Graph image URL points to `https://teamzenkai.com/opengraphEmbed.png`, so the root site must stay published.
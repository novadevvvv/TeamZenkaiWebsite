# Team Zenkai Deployment Setup

GitHub root repository:

- `https://github.com/novadevvvv/TeamZenkaiWebsite`

This workspace now contains:

- Root site for `teamzenkai.com`
- A deployable template for a separate GitHub Pages site at `discord.teamzenkai.com`


## Root Site

Files already in this repository root:

- `index.html` - maintenance page
- `opengraphEmbed.png` - shared image asset
- `CNAME` - binds GitHub Pages to `teamzenkai.com`


### GitHub Pages

1. Push this repository to `novadevvvv/TeamZenkaiWebsite`.
2. Open repository settings.
3. Go to Pages.
4. Set Source to deploy from the main branch root.
5. Confirm the custom domain is `teamzenkai.com`.
6. After DNS resolves, enable `Enforce HTTPS`.

## Discord Subdomain Site

Use the files in `discord-site-template/` as a second repository.

### GitHub Pages

1. Create a new GitHub repository for the Discord redirect site under the same account, for example `novadevvvv/TeamZenkaiDiscord`.
2. Copy the contents of `discord-site-template/` into the root of that repository.
3. Open repository settings.
4. Go to Pages.
5. Set Source to deploy from the main branch root.
6. Confirm the custom domain is `discord.teamzenkai.com`.
7. After DNS resolves, enable `Enforce HTTPS`.

## Cloudflare DNS

Set all GitHub Pages DNS records to `DNS only` while validating.

### Apex domain

Create these records for `teamzenkai.com`:

| Type | Name | Target |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

### Discord subdomain

Create this record for `discord.teamzenkai.com`:

| Type | Name | Target |
| --- | --- | --- |
| CNAME | discord | novadevvvv.github.io |

This should stay `DNS only` in Cloudflare while validating Pages.

### Optional `www` redirect

If you want `www.teamzenkai.com` to resolve too:

| Type | Name | Target |
| --- | --- | --- |
| CNAME | www | novadevvvv.github.io |

Or add a Cloudflare redirect rule from `www.teamzenkai.com/*` to `https://teamzenkai.com/$1`.

## Cloudflare SSL

1. Set SSL mode to `Full`.
2. Enable `Always Use HTTPS`.
3. Keep GitHub Pages records on `DNS only` unless you have a specific reason to proxy them.

## Current DNS Diagnosis

Current live lookup results from this machine:

- `teamzenkai.com` returns only the Cloudflare zone `SOA` record and no `A` or `AAAA` answers
- `discord.teamzenkai.com` resolves, but it is currently proxied through Cloudflare edge IPs

That means `teamzenkai.com` is failing at DNS before GitHub Pages can respond. The fix is in Cloudflare DNS, not in the HTML files.

## Verification

1. `https://teamzenkai.com` shows the maintenance page.
2. `https://teamzenkai.com/opengraphEmbed.png` loads.
3. `https://discord.teamzenkai.com` redirects to the Discord invite.
4. GitHub Pages shows valid HTTPS for both custom domains.
# Cloudflare DDNS updater with Bash and Crontab
## About
- Cloudflare DDNS updater with Bash.
- Detects host IP and updates cloudflare A record if it is different (supports Cloudflare Proxy).
- API Token is only supported for security reasons.

## Requirements
- curl
- jq
- A Cloudflare api-token with ZONE-DNS-EDIT Permissions
- A DNS Record must be pre created (api-token should only be set to edit dns records)

## How to create Cloudflare API Token?
- Open https://dash.cloudflare.com/profile/api-tokens
- Click **Cretea Token**
- Select **Use template** for **Edit zone DNS**
- Set permissions to **Zone - DNS - Edit**
- Set zone resource to **Include - Specific zone - domain.com**
- Click **Continue to summary** and **Create Token**
- Use the newly created token in this script

## Installation
```
url="https://raw.githubusercontent.com/leomoon-studios/cloudflare-ddns-with-bash/main/src/ddns"
sudo wget $url -O /usr/local/bin/ddns
sudo chmod +x ddns
```

## Examples
In these examples we're using `5SPAFH7MF6Xgqe2wDoFsjNB5ZngSvxbAZ25AHart` as API token.

Updating `domain.com` record (root) for `domain.com` zone in verbose mode.
```
ddns -z domain.com -a test.domain.com -t 5SPAFH7MF6Xgqe2wDoFsjNB5ZngSvxbAZ25AHart -v
```

Updating `test.domain.com` record for `domain.com` zone in verbose mode.
```
ddns -z domain.com -a test.domain.com -t 5SPAFH7MF6Xgqe2wDoFsjNB5ZngSvxbAZ25AHart -v
```

## Automating with Crontab
Run every 5 minutes
```
*/5 * * * * /usr/local/bin/ddns -z domain.com -a test.domain.com -t 5SPAFH7MF6Xgqe2wDoFsjNB5ZngSvxbAZ25AHart
```

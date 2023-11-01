# Heroku Buildpack for the Salesforce CLI

This is the official [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for installing the Salesforce CLI into your Heroku dyno. It will also install `jq`, a command-line tool that is like sed for JSON data, which makes it easy to interact with JSON output from the Salesforce CLI.

## Usage

This buildpack adds `sfdx` & `jq` the `$PATH` in the dyno, so that they are immediately usable.

In the following commands:  
✏️ *Replace `$ORG_USERNAME` with the target org's username or sfdx alias.*  
✏️ *Replace `$APP_NAME` with the target Heroku app's name.*

**To enable automated authentication with a Salesforce org** add its secret refresh token `sfdxAuthUrl` to the Heroku app:

```bash
heroku config:set --app $APP_NAME SFDX_AUTH_URL="$(sfdx force:org:display -u "$ORG_USERNAME" --verbose --json | jq -r .result.sfdxAuthUrl)"
```

Then, create a `.profile` file with the following contents, and commit/deploy it to the Heroku app. Everytime a dyno starts-up, this script will read that secret value to authenticate `sfdx` with the org:

```bash
#!/bin/bash

# Write config var to a file for sfdx
echo "$SFDX_AUTH_URL" > sfdx-auth-url.txt

# Authenticate sfdx with the org
sfdx force:auth:sfdxurl:store -f sfdx-auth-url.txt -s

# Delete the secret material
rm sfdx-auth-url.txt
```

Finally, verify that authentication is working using a one-off dyno:

```bash
heroku run bash --app $APP_NAME
~ $ sfdx force:org:list
=== Orgs
     USERNAME           ORG ID              CONNECTED STATUS
───  ─────────────────  ──────────────────  ────────────────
(U)  xxxxx@example.com  00D6g000000XXXXXXX  Connected

No active scratch orgs found. Specify --all to see all scratch orgs
```

🏁 Once finished, the Heroku app's `sfdx` CLI will maintain authentication with the Salesforce org


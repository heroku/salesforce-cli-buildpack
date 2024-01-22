# Heroku Buildpack for the Salesforce CLI

This is the official [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for installing the Salesforce CLI into your Heroku dyno. It will also install `jq`, a command-line tool that is like sed for JSON data, which makes it easy to interact with JSON output from the Salesforce CLI.

## Usage

The `sfdx` and `jq` commands are automatically added to $PATH during the startup of each Heroku process.

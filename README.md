# Heroku Buildpack for the Salesforce CLI

This is the official [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for installing the Salesforce CLI into your Heroku dyno. It will also install `jq`, a command-line tool that is like sed for JSON data, which makes it easy to interact with JSON output from the Salesforce CLI.

## Usage

On a terminal, run the following command to add an additional buildpack to your App.

````
heroku buildpacks:add https://github.com/heroku/salesforce-cli-buildpack --index 1
````

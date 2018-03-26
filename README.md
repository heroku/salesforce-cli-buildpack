# Heroku Buildpack for the Salesforce CLI

This is the official [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for installing the Salesforce CLI into your Heroku dyno. It will also install `jq`, a command-line tool that is like sed for JSON data, which makes it easy to interact with JSON output from the Salesforce CLI.

## Usage

To use `sfdx` and `jq`, you simply need to export the appropriate paths:

```
export PATH="$BUILD_DIR/vendor/sfdx/cli/bin:$PATH"
export PATH="$BUILD_DIR/vendor/sfdx/jq:$PATH"
```

The `$BUILD_DIR` is the path where your apps source is stored on the Heroku dyno.
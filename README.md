# buildpack for sfdx cli

I took this from the official buildpack, forked for stability and removed jq because I don't use it in node (node does javacript just fine)

## Usage

To use `sfdx`, you simply need to export the appropriate paths:

```
export PATH="$BUILD_DIR/vendor/sfdx/cli/bin:$PATH"
```

The `$BUILD_DIR` is the path where your apps source is stored on the Heroku dyno.
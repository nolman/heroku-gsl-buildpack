# Heroku GSL Buildpack

A buildpack to install gsl on a heroku dyno.

This buildpack downloads a compiled version of GSL so that it can be used by any buildpack that comes after it in the buildpack chain. 

## Installation

*Note :  heroku multi buildpack used to be required, but it's no longer the case. Now heroku supports multiple buildpacks natively.*

Add the buildpack to your application ; in the buildpack chain, it should appear before any other buildpack that may require it. Hence the `--index=1` option :

```
heroku buildpacks:add https://github.com/nolman/heroku-gsl-buildpack.git --index=1
```

You can check that the buildpack chain is the right order with :

```
heroku buildpacks

1. https://github.com/nolman/heroku-gsl-buildpack.git
2. heroku/ruby
```

The buildpack can be used with another buildback than `heroku/ruby`, but if your aim is to make the `gsl` gem work on heroku, you can just add `gem gsl` to your Gemfile and you should now be able to deploy.

## Compiling binaries on heroku

If you want to recompile a more recent/different version of gsl, you can find an example script that compiles binary from a source tar.gz [here](extra/build_binary)

This script relies on the fog gem to upload the binary, once compiled, to s3. You will need to add that dependency to your Gemfile. You will also need to set an ENV var for your AWS key and secret.

## Known issues

Only supports the 1.16 GSL release.
Cannot set the AWS Bucket to download dependencies via an env var.

Pull requests welcome.

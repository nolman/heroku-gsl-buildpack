# Heroku GSL Buildpack

A buildpack to install gsl on a heroku dyno.

## Installation

Use heroku multi buildpack:

https://github.com/nolman/heroku-buildpack-multi

Note: you need a variant of the buildpack multi that allows you to chain exported variables from one buildpack to the next. For now my fork will work fine (using ./export from the buildpack), in the longer term there should be a standard way to chain buildpacks together.

To set this buildpack on heroku run the following:

```
heroku config:set BUILDPACK_URL="https://github.com/nolman/heroku-buildpack-multi"
```

Then add a .buildpacks file to your app:

```
https://github.com/nolman/heroku-gsl-buildpack.git
https://github.com/heroku/heroku-buildpack-ruby.git#v119
```

You can replace the ruby buildpack with whatever you language of choice is.

## Compiling binaries on heroku

You can find an example script that compiles binary from a source tar.gz [here](extra/build_binary)

This script relies on the fog gem to upload the binary to s3. You will need to add that dependency to your Gemfile. You will also need to set an ENV var for your AWS key and secret.

## Known issues

Only supports the 1.16 GSL release.
Cannot set the AWS Bucket to download dependencies via an env var.

Pull requests welcome.

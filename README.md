# Heroku Buildpack for Heroku Integration Service Mesh

This buildpack installs [Heroku Integration Service Mesh](https://github.com/heroku/heroku-integration-service-mesh) in a Heroku app.  This buildpack, and the binary it installs, is to be used in conjunction with Heroku Integration add-on.

For more information, see [Heroku Integrations](https://devcenter.heroku.com/articles/heroku-integration).

## Installation
```sh
heroku buildpacks:add heroku/heroku-buildpack-heroku-integration-service-mesh
```

## Usage
The Heroku Integration Service Mesh binary must be configured in your Procfile web process to start your app.
```sh
web: heroku-integration-service-mesh <your app startup command>
```

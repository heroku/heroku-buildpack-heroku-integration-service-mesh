# Heroku Buildpack for Heroku Integration Service Mesh

This buildpack installs [Heroku Integration Service Mesh](https://github.com/heroku/heroku-integration-service-mesh) in a Heroku app.  This buildpack, and the binary it installs, is to be used in conjunction with Heroku Integration add-on.

For more information, see [Heroku Integrations](https://devcenter.heroku.com/articles/heroku-integration).

## Installation
```shell
heroku buildpacks:add heroku/heroku-buildpack-heroku-integration-service-mesh
```

## Usage
The Heroku Integration Service Mesh binary must be configured in your Procfile web process to start your app.
```shell
web: heroku-integration-service-mesh <your app startup command>
```
The latest Heroku Integration Service Mesh release will be installed.

To declare a specific release version or tag set `HEROKU_INTEGRATION_SERVICE_MESH_RELEASE_VERSION` config or environment variable.
```shell
HEROKU_INTEGRATION_SERVICE_MESH_RELEASE_VERSION=v1.0.0
```

During deployment, Heroku Integration Service Mesh binary is installed.
```shell
-----> Installing version "v0.1.0" of Heroku Integration Service Mesh...
       Downloading heroku-integration-service-mesh...
       Installing heroku-integration-service-mesh...
       Done!
-----> Ensure that heroku-integration-service-mesh is configured in your Procfile's web process to start your app, eg heroku-integration-service-mesh <app startup command>
```

## Run Locally
```shell
$ git clone git@github.com:heroku/heroku-buildpack-heroku-integration-service-mesh.git
...
$ cd heroku-buildpack-heroku-integration-service-mesh
$ mkdir build_dir cache_dir env_dir
$ bin/compile build_dir cache_dir env_dir/
-----> Installing version "v0.12.1" of Heroku Integration Service Mesh...
       Downloading heroku-integration-service-mesh...
       Installing heroku-integration-service-mesh...
       Done!
-----> Ensure that heroku-integration-service-mesh is configured in your Procfile's web process to start your app, eg heroku-integration-service-mesh <app startup command>
$ ls -l build_dir/vendor/heroku-integration/bin/
total 12M
-rwxrwxr-x 1 cwall cwall 12M Sep 27 07:55 heroku-integration-service-mesh

```

# Monitoring and Alerting for Heroku Integration Service Mesh Buildpack

This document describes how to monitor and alert on the usage and failures of the Heroku Integration Service Mesh buildpack.

## Cedar-Generation Monitoring

### Honeycomb Monitoring

Cedar-generation builds appear as events in the Honeycomb builds dataset (in the Honeycomb classic/legacy environment).

For this buildpack, the build system automatically populates a minimal "build report" containing:
- `heroku-integration-service-mesh.buildpack_url` - Identifies builds using this buildpack
- `heroku-integration-service-mesh.failed` - Indicates if the buildpack execution failed

#### Querying for Buildpack Usage

To find builds where this buildpack was used:
```shell
heroku-integration-service-mesh.buildpack_url exists
```

#### Monitoring Failure Rates

These queries are executed in the Honeycomb UI (https://ui.honeycomb.io/heroku/datasets/builds/) using the builds dataset:

1. Query total buildpack usage: `heroku-integration-service-mesh.buildpack_url exists`
2. Query failed builds: `heroku-integration-service-mesh.failed = true`
3. Calculate failure percentage: (failed builds ÷ total builds) × 100

You can also create a derived column in Honeycomb for this calculation or use Honeycomb's query builder to construct these metrics.



## Long-Term Analytics (DWH)

For analytics beyond Honeycomb's 60-day retention or to correlate with revenue:

1. Use `heroku.core_apps` table in DWH
   - `language_pack` field for general usage tracking
   - `buildpacks_json` field for specific buildpack URIs

2. For revenue analysis, join against invoice tables

## Fir-Generation Compatibility

Currently, this buildpack is not Fir-compatible. When Fir support is added:

1. Monitoring will shift to the `heroku-builds-production` Honeycomb dataset with full OTel traces
2. In DWH, buildpack information will be available in the `heroku.core_oci_images` table
3. The list of buildpacks will be controlled via `project.toml` rather than as API attributes

## Future Implementations/Plans

### Enhanced Monitoring with bin/report

> Note: The `bin/report` API is currently not implemented in this buildpack. It's available in some other Heroku buildpacks (e.g., Python), with plans to extend it to more buildpacks in FY26.

For richer analytics in the future, this buildpack could implement the `bin/report` API:

1. Create a `bin/report` script that outputs YAML with key-value pairs
2. This would allow tracking custom metrics specific to the buildpack

This would enable queries like:
- Distribution of service mesh versions in use
- Correlation between versions and failure rates

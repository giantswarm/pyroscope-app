# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Upgraded pyroscope chart from 2.0.1 to 2.2.0, and the pyroscope image from 1.2.1 to 2.2.0.
  The 1.x image does not understand the `-architecture.storage` and `-write-path` flags the
  2.x chart renders.
- **Migrated to the v2 storage architecture.** Upstream chart 2.0.2 made v2 the default, and
  our previous `components` layout only listed v1 components (ingester, querier,
  query-scheduler, compactor, store-gateway), so the rendered pods got v2 flags with no v2
  components behind them. We now set `architecture.microservices.enabled` and take the
  upstream `architecture.microservices.v2` component set: segment-writer, metastore,
  query-backend, compaction-worker, distributor, query-frontend, admin, tenant-settings and
  ad-hoc-profiles.
- Enabled the bundled minio by default. The v2 architecture requires an object store shared
  across components; without one every pod falls back to its own local filesystem. Set
  `pyroscope.minio.enabled=false` and point `pyroscope.pyroscope.config` at an external
  bucket to use real object storage.
- Change team annotation in `Chart.yaml` to OpenContainers format (`io.giantswarm.application.team`).
- Update PolicyExceptions to v2 and fallback to v2beta1.
- Fix ABS config to not override AppVersion in Chart.yaml

### Fixed

- Use `image.repository` instead of `image.name` in `values.yaml`. The upstream key is
  `repository`, so our override was ignored and the image resolved to the non-existent
  `gsoci.azurecr.io/grafana/pyroscope` instead of `gsoci.azurecr.io/giantswarm/pyroscope`.

## [0.2.0] - 2024-01-18

## Changed

- Upgraded pyroscope chart from 1.3.1 to 1.3.3
- Use upstream ingress instead of custom one.

## [0.1.0] - 2024-01-08

- Initial release.

[Unreleased]: https://github.com/giantswarm/pyroscope-app/compare/v0.2.0...HEAD
[0.2.0]: https://github.com/giantswarm/pyroscope-app/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/giantswarm/pyroscope-app/releases/tag/v0.1.0

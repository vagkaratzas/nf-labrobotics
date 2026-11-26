# Changelog

## [Unreleased]

### Dependencies

Development and build tools, the CI's uv setup action, the adapter's minimum FastAPI (a minor release) and httpx2 (a patch release), and a security fix in OpenTelemetry API, which FastAPI pulls in ([GHSA-mf5v-w3w3-f6cg](https://github.com/advisories/GHSA-mf5v-w3w3-f6cg); reached only when OpenTelemetry tracing is configured, which the adapter and dashboard do not do).

| Tool                    | Previous version | New version |
| ----------------------- | ---------------- | ----------- |
| astral-sh/setup-uv (CI) | 10.3.3           | 10.4.0      |
| FastAPI (adapter)       | 0.162.0          | 0.165.0     |
| Gradle wrapper          | 9.8.2            | 9.9.2       |
| httpx2 (adapter)        | 2.16.0           | 2.16.2      |
| OpenTelemetry API       | 1.45.1           | 1.45.2      |
| pytest                  | 9.1.1            | 9.2.0       |
| uv_build (adapter)      | 0.13.5           | 0.13.9      |

## [0.1.0] - 2026-10-30

First release: a prototype, built against PyLabRobot's simulated machines. Needs Nextflow 26.10.0 or later and Java 17.

### Added

- The `labrobotics` executor: a wet step never runs twice, not on retry, `-resume` or a new launch directory, and aborting a run safe-stops the robot instead of killing it mid-protocol. Each wet task's provenance (device, protocol version, samples) goes into Nextflow lineage.
- The `labrobotics {}` config scope (adapter URL, polling) and the `labPlate` function.
- The device adapter (`adapter/`): job ledger, robot pools and queues, a deck page for people at the bench, bearer-token auth (`NF_LAB_TOKEN`), lab limits for protocol parameters (`NF_LAB_LIMITS`), and bindings for every PyLabRobot 0.2.2 simulated machine. `labctl` is the client a wet task runs; `openapi.json` is the contract; the conformance kit checks any adapter against it.
- Wet modules (`wet-modules/`): 19 protocols, from `plate_transfer` and `rna_extraction` to `pcr` and `qpcr`, and 6 subworkflows that chain them, each with nf-tests.
- Example pipelines (`examples/`), including a 1000-sample RT-qPCR run, and a dashboard (`dashboard/`) with a live view of a run and scripted demos.

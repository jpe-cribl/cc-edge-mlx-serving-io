# cc-edge-mlx-serving-io

Cribl Edge pack for MLX model-serving, benchmark, and workstation telemetry.

## Installation

Build the archive from the repository root and import it in Cribl Edge:

```sh
tar -czf cc-edge-mlx-serving-io-v0.1.0.crbl default package.json README.md
```

## Usage

The pack's pipelines are loaded by id, and host configuration routes its sources to those ids.
Routes in `default/pipelines/route.yml` match when `datatype` equals the pipeline id.

Pipelines and the index and sourcetype each one sets:

- `llm_logs`: index `llm`; sourcetype `llamaswap`, `mlx:model-server` or `mlx:cluster`,
  chosen from the input and the line prefix.
- `bench_events`: index `llm`; sourcetype `mlx:bench`; stamps benchmark result rows.
- `llm_metrics`: index `llm`; sourcetype `mlx:metrics`; stamps system metric samples and adds
  `judge_process_start_time_seconds` when the process start field is present.
- `workstation_load`: index `llm`; sourcetype `mlx:metrics`; emits the five-minute load average
  as the `node_load5` metric with `host_role=workstation`, and drops events without a finite value.
- `workstation_offload`: index `workstation`; sourcetype `macos:offbox_sync`; stamps offbox sync records.
- `workstation_jobs`: index `workstation`; sourcetype `macos:local_job`; stamps local job log lines.

`workstation_load` has no route entry. It is attached to its source by pipeline id.

## Testing

CI runs Biome lint, the TypeScript typecheck, and the Vitest fixture suite against a Cribl container.
Each `tests/fixtures/<pipeline>/<case>.json` runs through its pipeline, and `<case>.expected.json`
holds the partial-match expectations.

## Release notes

See [CHANGELOG.md](CHANGELOG.md).

# cc-edge-mlx-serving-io

Cribl Edge pack for MLX model-serving, benchmark, and workstation telemetry.

This is the initial skeleton. The pack's pipelines are added on a feature branch.

## Installation

Install the pack's `.crbl` artifact in Cribl Edge. Build it locally with `tar -czf` over `default`, `package.json`, and `README.md`.

## Usage

Pipelines are referenced by pipeline id. Run the fixture suite to exercise them:

```sh
cd tests && pnpm install --frozen-lockfile
pnpm run lint
pnpm run typecheck
pnpm run test   # needs a Cribl instance on CRIBL_HOST:CRIBL_PORT
```

## Releases

Version bumps and release notes are described in the sections added with each release.

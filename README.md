# rd-fluxcd-lesson

## Stage 1

```bash
GITHUB_TOKEN=$(gh auth token) flux bootstrap github
    --owner=chornonoh-vova
    --repository=rd-fluxcd-lesson
    --branch=main
    --path=./clusters/my-cluster
    --personal
```

## Stage 2

Created the `base/` for the application manifests.

## Stage 3

Created the `overlays/development/` for the development.

Additionally, created the `infrastructure/controllers/dragonfly/` to install the
dragonfly operator.

## Stage 4

Created the `overlays/production/`.

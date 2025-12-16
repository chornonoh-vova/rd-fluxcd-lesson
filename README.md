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

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

## Stage 5

Connected flux manifests to connect development and production overlays and
dragonfly operator.

## Verification

Kustomizations syncronized with Git:

```bash
kubectl get kustomizations -A
```

Output:

```txt
NAMESPACE     NAME                     AGE    READY   STATUS
flux-system   course-app-development   133m   True    Applied revision: main@sha1:2bd906aebaa2eaa4114cc7585b1a2b98601ed06f
flux-system   course-app-production    133m   True    Applied revision: main@sha1:2bd906aebaa2eaa4114cc7585b1a2b98601ed06f
flux-system   flux-system              164m   True    Applied revision: main@sha1:2bd906aebaa2eaa4114cc7585b1a2b98601ed06f
flux-system   infrastructure           14m    True    Applied revision: main@sha1:2bd906aebaa2eaa4114cc7585b1a2b98601ed06f
```

Pods in dev environment:

```bash
kubectl get pods -n development
```

Output:

```txt
NAME                                     READY   STATUS    RESTARTS        AGE
course-app-deployment-6df599b45b-2jws6   1/1     Running   1 (2m37s ago)   3m32s
dragonfly-0                              1/1     Running   0               3m32s
```

Pods in prod environment:

```bash
kubectl get pods -n production
```

Output:

```txt
NAME                                     READY   STATUS    RESTARTS      AGE
course-app-deployment-6df599b45b-bscrq   1/1     Running   2 (16m ago)   16m
course-app-deployment-6df599b45b-c845b   1/1     Running   2 (16m ago)   16m
course-app-deployment-6df599b45b-lrzkf   1/1     Running   2 (16m ago)   16m
dragonfly-0                              1/1     Running   0             16m
dragonfly-1                              1/1     Running   0             16m
```

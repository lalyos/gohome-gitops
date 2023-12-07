
## Install

```
arkade get flux
flux install --export | kubectl apply -f -
```



## Gitops level 1 - kustomize

```
flux create source git gohome \
    --url=https://github.com/lalyos/gohome-gitops \
    --branch=master \
    --export  > flux/gitrepo.yaml


  flux create kustomization gohome \
    --source=GitRepository/gohome \
    --target-namespace=default \
    --path="./" \
    --prune=true \
    --interval=1m \
    --wait=true \
    --export > flux/kust.yaml
```

## level 1 - helm

```
  flux create source helm lalyos \
    --url=https://chart.lalyo.sh/ \
    --interval=1m \
    --export > flux/helm.yaml
```

```
  flux create hr weekend \
    --source=HelmRepository/lalyos \
    --chart=12factor \
    --values=./values-weekend.yaml \
    --export > flux/release.yaml
```
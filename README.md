
## Install

```
arkade get flux
flux install --export | kubectl apply -f -
```



## Gitops level 1

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
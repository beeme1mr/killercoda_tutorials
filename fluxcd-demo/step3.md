# Customize podinfo deployment

To customize a deployment from a repository you don’t control, you can use Flux in-line patches. The following example shows how to use in-line patches to change the `podinfo` deployment.

Add the following to the field spec of your `podinfo-kustomization.yaml` file:

```
  patches:
    - patch: |-
        apiVersion: autoscaling/v2beta2
        kind: HorizontalPodAutoscaler
        metadata:
          name: podinfo
        spec:
          minReplicas: 3             
      target:
        name: podinfo
        kind: HorizontalPodAutoscaler
```

Commit and push the `podinfo-kustomization.yaml` changes:

```
git add -A && git commit -m "Increase podinfo minimum replicas"
git push
```
After the synchronization finishes, running `kubectl get pods` should display `3` pods.
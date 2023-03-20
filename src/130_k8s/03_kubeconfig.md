* update-config

```bash
aws eks --region eu-west-2 update-kubeconfig --name jk_spinnaker_eks
```

* change default namespace

```bash
kubectl config set-context --current --namespace=<new-default-namespace>
```



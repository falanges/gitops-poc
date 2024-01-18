```bash
flux create alert-provider discord \
  --type=discord \
  --secret-ref=discord \
  --channel=gitops-lab \
  --username=FluxBot \
  --namespace=default \
  --export > notifications/providers/discord-provider.yaml

flux create alert discord-bot-alert \
  --event-severity=info \
  --event-source=GitRepository/*,Kustomization/* \
  --provider-ref=discord \
  --namespace=default \
  --export > notifications/alerts/discord-bot-alert.yaml
```

after setup run the following command in notifications directory:
```bash
kustomize create --autodetect --recursive

flux create secret git gitops-lab-deploy-auth \
  --url=https://gitlab.com/falanges/ci-gitlab-tf-poc.git \
  --namespace=default \
  --username=falanges \
  --password=your-pwd


kubectl get secrets gitops-poc-deploy-auth -o yaml | yq '.data'

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

# ArgoCD

Namespace ArgoCD в кластере может быть `argocd` или `shturval-cd`.

| Application | path | project | destination |
|-------------|------|---------|-------------|
| Ollama | `.` | `ollama` | `ollama` |
| Intel GPU plugin (опционально) | `device-plugin` | `ollama` | `ollama` |

```bash
kubectl apply -f application-device-plugin.yaml   # опционально
```

NFD не используется — нода с GPU задаётся через `TARGET_NODE` в ConfigMap.

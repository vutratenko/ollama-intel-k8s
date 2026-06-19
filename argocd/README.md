# ArgoCD manifests

Namespace ArgoCD в кластере может быть `argocd` или `shturval-cd` — подставьте свой.

## AppProject cluster-addons

### Создание (первый раз)

```bash
kubectl apply -f appproject-cluster-addons.yaml
```

### Обновление (если AppProject уже существует)

`kubectl apply` может вернуть:

```text
metadata.resourceVersion: Invalid value: 0: must be specified for an update
```

Используйте **patch** (рекомендуется):

```bash
# argocd или shturval-cd — namespace вашего ArgoCD
ARGOCD_NS=shturval-cd

kubectl patch appproject cluster-addons -n "$ARGOCD_NS" \
  --type merge \
  --patch-file appproject-cluster-addons-patch.yaml
```

Альтернативы:

```bash
# Server-side apply
kubectl apply --server-side --force-conflicts \
  -f appproject-cluster-addons.yaml

# Удалить и создать заново (если нет зависимых Applications)
kubectl delete appproject cluster-addons -n "$ARGOCD_NS"
kubectl apply -f appproject-cluster-addons.yaml
```

Проверка:

```bash
kubectl get appproject cluster-addons -n "$ARGOCD_NS" -o yaml | grep -A6 clusterResourceWhitelist
```

## NFD вне ArgoCD

Если политики кластера блокируют cluster-scoped ресурсы:

```bash
kubectl apply -k ../nfd/
```

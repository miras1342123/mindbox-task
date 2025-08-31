# Mindbox — K8s webapp

**Что делает манифест**
- Запускает несколько копий приложения (Deployment + Service).
- Днём при росте нагрузки копий становится больше (HPA по CPU), ночью — минимум 1 (экономия).
- Поды "размазываются" по разным серверам/зонам (topologySpread + anti-affinity) — выше отказоустойчивость.
- Обновления без простоя (RollingUpdate: maxUnavailable=0).
- Проверки здоровья через TCP (подходит для nginx; для своего приложения можно указать HTTP пути).

**Запуск локально (по желанию)**
```bash
# нужен kubectl и minikube или kind
kubectl apply -f webapp.yaml
kubectl -n webapp get pods
# чтобы открыть в браузере (minikube):
# minikube service -n webapp webapp --url
# или портфорвардинг:
# kubectl -n webapp port-forward svc/webapp 8080:80

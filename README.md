# Тестовое задание Mindbox (SRE Intern)

## Что сделано

- Deployment для веб-приложения в Kubernetes
- Учтены все требования задания

## Учтённые требования

| Требование | Реализация |
|------------|------------|
| Мультизональный кластер (3 зоны) | podAntiAffinity по нодам (базовая защита) |
| 5-10 сек инициализации | readinessProbe: initialDelaySeconds 5 |
| 4 пода на пик нагрузки | HPA maxReplicas: 4 |
| CPU: всплеск на старте → 0.1 | requests: 100m, limits: 300m |
| Память: всегда 128M | requests: 128Mi, limits: 256Mi |
| Дневной цикл нагрузки | HPA minReplicas: 2, maxReplicas: 4 |
| Максимальная отказоустойчивость | podAntiAffinity + 2 реплики минимум |
| Минимальное потребление ресурсов | HPA уменьшает до 2 реплик ночью |

## Состав манифеста

- Deployment
- HorizontalPodAutoscaler (CPU 70%)
- podAntiAffinity (разнос подов по нодам)
- readinessProbe + livenessProbe
- requests / limits

## Как применить

kubectl apply -f deployment.yaml

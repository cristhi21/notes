# ¿Qué es KUBECTL CLI?

# Instalación

- Windows
https://kubernetes.io/es/docs/tasks/tools/included/install-kubectl-windows/
- Linux
https://kubernetes.io/es/docs/tasks/tools/included/install-kubectl-linux/
- MacOS
https://kubernetes.io/es/docs/tasks/tools/included/install-kubectl-macos/

# Configuración

# Comandos

## Ambientes
- Asignar ambiente

```sh
aws eks update-kubeconfig --name <cluster_name>-dev --region us-east-1
aws eks update-kubeconfig --name <cluster_name>-qa --region us-east-1
aws eks update-kubeconfig --name <cluster_name>-pdn --region us-east-1
```

## Logs

- Todos los pods al mismo tiempo
  `kubectl logs -n name_namespace-pdn -f -l pod=ss-ms-device-control-pod --max-log-requests=20`
- descargar logs
 `kubectl logs -n name_namespace-pdn {nombre-pod} > {nombre del log}.log`


## Pods

- listar pods 
 `kubectl get pod -n name_namespace-qa`
- listar pods con autoescalamiento y ips
 `kubectl get pod -n name_namespace-qa -o wide -w`
- listar pods filtrando por un label
 `kubectl get pod -n name_namespace-qa -l pod=fa-ms-functional-adapter-pod`
- listar pods filtrando por un label con consumo de memoria y CPU
 `kubectl top pod -n name_namespace-qa -l pod=fa-ms-functional-adapter-pod`
- borrar pods de un microservicio
 `kubectl delete pod -n name_namespace-qa -l pod=ms-authentication-pod`
- Obtener información del pod
 `kubectl describe pod -n name_namespace-qa -l pod=ms-authentication-pod`
- Obtener los logs de todos los pods
 `kubectl logs -n name_namespace-qa -f -l app=ms-vinculation-pod --max-log-requests=20`
- Obtener la información del configmap de un microservicio
 `kubectl get configmap -n name_namespace-pdn -o json ss-ms-device-control-configmap`

# Versiones
|  Fecha| Descripción | Realizó | Aprobó |
|--|--|--|--|
| 16/02/2024 | Versión inicial | @<Fulano>  |  |

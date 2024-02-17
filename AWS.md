# AWS

## CloudWatch -> Logs Insights -> (seleccionar grupo de registros, buscar clientes, seleccionar eks-)

fields @timestamp, @message
| filter kubernetes.container_name = 'xxx-container'
| filter @message like 'Error'
| sort @timestamp desc
| limit 120
------
field limits @timestamp, interfaceId, srcAddr, srcPort, dstPort, action
| filter srcAddr = '' and dstPort = ''
| sort @timestamp
------
fields @timestamp, @message, @logStream, @log
| filter kubernetes.container_name = 'xxx-container'
| filter @message like 'Error'
| sort @timestamp desc
| limit 120
------
fields @timestamp, @message, @logStream, @log
| filter kubernetes.container_name = 'xxx-container'
| filter @message like 'Error'
| sort @timestamp desc
| limit 120
------
fields @timestamp, log, @message, @logStream, @log
| filter kubernetes.container_name = 'xxx-find-container'
| filter @message like 'Error'
| sort @timestamp desc


## COMMANS COMMONS AWS
```sh
aws eks
aws eks update-kubeconfig --name eks-clientes-qa
aws configure
aws --version
```

## Ver los pods terminal
```sh
# 1. Hacer set a las variables de entorno de AWS
# 2. aws eks update-kubeconfig --name eks-clientes-qa
# 3. Listar los pods
# siempre se debe especificar el el namespace con -n  
kubectl get pods -n stoc-qa
# 4. Borrar pods
kubectl delete pods judge-deployment-59cbcb6c46-bb9pj -n stoc-dev
```

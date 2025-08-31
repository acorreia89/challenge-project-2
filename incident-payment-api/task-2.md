2. Listar ferramentas e comandos que usaria.


Ferramentas

Categoria	Ferramenta	Uso no diagnóstico
Kubernetes CLI	kubectl	Inspeção de pods, deployments, eventos e métricas no cluster
Monitoramento	Datadog	Visualizar métricas de latência, erros, tráfego e recursos
Logs	Datadog Logs / kubectl logs	Analisar erros e timeouts na aplicação
Banco de Dados	AWS Console (RDS) / CloudWatch	Checar métricas do RDS (CPU, conexões, latência)
Rede	nc (netcat) / telnet	Testar conectividade e latência com o RDS


comandos

1. Estado geral dos pods e eventos

kubectl get pods -n payment -o wide
kubectl describe pod <nome-do-pod> -n payment
kubectl get events -n payment --sort-by=.lastTimestamp

2. Logs da aplicação
kubectl logs <nome-do-pod> -n payment --tail=200
kubectl logs <nome-do-pod> -n payment --since=10m

3. Métricas de recursos
kubectl top pods -n payment
kubectl top pod <nome-do-pod> -n payment --containers

4. Teste de conectividade com o RDS
kubectl exec -it <nome-do-pod> -n payment -- nc -vz <endpoint-rds> 5432


5. Métricas do RDS no CloudWatch
CPUUtilization
DatabaseConnections
FreeableMemory
ReadLatency / WriteLatency

6. Histórico de deploys no ArgoCD

argocd app history payment-api
argocd app get payment-api

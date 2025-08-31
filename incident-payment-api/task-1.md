# Descrever sequência de passos para diagnosticar o problema

## 🎯 Objetivo
Estabelecer uma sequência clara e estruturada de ações para diagnosticar e mitigar problemas críticos em produção.  
O foco é garantir que, durante o incidente, todas as informações relevantes — como métricas, logs, histórico e insights coletados em tempo real — sejam utilizadas para confirmar hipóteses, identificar a causa raiz e restaurar o serviço com o menor impacto possível.

## 🛠 Passos para Diagnóstico
1. **Avaliar o impacto** e comunicar imediatamente os stakeholders sobre a situação.
2. **Validar nas ferramentas de observabilidade** as principais métricas de degradação do serviço, como tempo de resposta, taxa de erros e throughput.
3. **Verificar o estado do serviço no Kubernetes**, incluindo pods, deployments e eventos.
4. **Checar recursos de infraestrutura** relacionados (EKS, RDS e rede) para identificar gargalos ou falhas.
5. **Analisar logs da aplicação e de infraestrutura** para encontrar erros, timeouts ou comportamentos anômalos.
6. **Investigar conectividade e latência** entre o serviço e o banco de dados RDS.
7. **Verificar dependências externas**, como APIs de terceiros, middlewares ou processos não mapeados que possam estar impactando o serviço.
8. **Analisar histórico recente** de incidentes e comportamento do serviço para identificar padrões.
9. **Registrar todas as evidências** coletadas para apoiar a análise da causa raiz e o postmortem.

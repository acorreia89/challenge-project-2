# Apontar hipóteses prováveis sobre a causa

## 🎯 Objetivo
Identificar e registrar as hipóteses mais prováveis para a origem do problema, com base nas evidências coletadas durante o diagnóstico inicial.  
O objetivo desta etapa é direcionar a investigação de forma estruturada, priorizando as causas mais plausíveis e permitindo que a equipe valide ou descarte cada uma delas de maneira rápida e eficiente.

---

## 🔍 Hipóteses

1. **Problema no banco RDS**
    - Latência ou indisponibilidade momentânea.
    - Conexões saturadas (`max_connections` atingido).
    - Problemas de rede (latência entre EKS e RDS).

2. **Problema de rede no cluster**
    - Latência ou falhas no **VPC CNI**.
    - Alterações recentes em **Security Groups** ou **NACLs**.

3. **Saturação de recursos no serviço**
    - *CPU/Memory throttling* nos pods.
    - Acúmulo de requisições na fila de processamento.

4. **Dependência externa degradada**
    - API de terceiros utilizada pelo `payment-api` apresentando lentidão ou indisponibilidade.

5. **Configuração inadequada do pool de conexões**
    - Pool insuficiente ou mal configurado, resultando em timeouts e falhas de conexão.

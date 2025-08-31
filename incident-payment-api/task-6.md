# 6. Documentar o incidente e as melhorias preventivas

## 🎯 Objetivo
Registrar de forma clara e estruturada as informações relacionadas ao incidente, incluindo contexto, linha do tempo, causa raiz, ações de mitigação e melhorias preventivas.  
Essa documentação serve como base para aprendizado contínuo, revisão de processos e preparação para futuras ocorrências similares.

---

# 📄 Postmortem — Incidente de Latência no `payment-api`

## 🗓 Data e Hora
- **Início:** 31/09/2025 — 09:15 BRT  
- **Resolução:** 31/09/2025 — 10:02 BRT  
- **Duração:** 47 minutos  
- **Ambiente:** Produção  
- **Serviço:** `payment-api`  
- **Detecção:** Datadog  
- **Alerta crítico:**  
  `ALERTA: Latência média da API acima de 2 segundos por 10 minutos`  
- **Impacto:**  
  - Latência média > 2 segundos por 10 minutos  
  - Timeouts em requisições ao RDS  
  - Indisponibilidade parcial do processamento de pagamentos  
  - Impacto confirmado no faturamento pela equipe de negócios

---

## 🔍 Linha do Tempo

| Horário | Evento |
|--------:|--------|
| 09:15   | Latência da API começa a subir acima de 2s |
| 09:16   | Alerta Datadog disparado |
| 09:18   | SRE confirma impacto e aciona Dev + DBA |
| 09:20   | Verificação de pods e métricas no Kubernetes — todos Running |
| 09:25   | Logs mostram timeouts ao acessar RDS |
| 09:28   | Métricas do RDS indicam conexões no limite e aumento de CPU |
| 09:30   | Escalado número de réplicas do `payment-api` de 6 para 10 |
| 09:35   | DBA aumenta temporariamente capacidade do RDS |
| 09:45   | Latência começa a cair gradualmente |
| 10:02   | Métricas normalizadas, incidente encerrado |

---

## 🧾 Causa Raiz
A aplicação de alta criticidade, estava sendo executada em um cluster padrão com recursos limitados e configuração de autoscaling inadequada. Também foi analiso que a instância do RDS apresentava capacidade subdimensionada para lidar com picos de carga. Embora na maioria do tempo o sistema operava em boas condições, mas com aumento repentino no volume de requisições houve um gargalho.
Em resumo a lentidão na resposta do autoscaling do EKS e a falta de recurso do RDS, resultou na saturação de CPU e memória nos nodes do cluster. Isso levou ao throttling dos pods e ao aumento significativo da latência no processamento das requisições, impactando diretamente a disponibilidade do serviço.

---

## 🚑 Ações Imediatas (Mitigação)
- Escalonamento horizontal dos nodes de forma manual para aliviar a carga e estabilizar o serviço.
- Aumento de da capacidade do RDS
---

## 🔧 Melhorias Preventivas
- Migrar a aplicação para outro cluster ou nodegroup com capacidade adequada à sua criticidade.
- Explorar recurso RDS com time de Banco de dados para atender melhor o ambiente nesses cenários.
- Criar dashboards com visão única das principais métricas de infraestrutura do EKS e RDS, serviço, negócio e logs.
  - Disponibilizar esses dashboards ao NOC para acompanhamento em tempo real.
  - Utilizar como suporte em futuras análises de incidentes.

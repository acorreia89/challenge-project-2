6. Documentar o incidente e as melhorias preventivas.


Objetivo

Demonstrar informações do incidente, linha do tempo, causa raiz e melhorias


# 📄 Postmortem — Incidente de Latência no payment-api

## 🗓 Data e Hora
- **Início:** 31/09/2025 — 09:15 BRT
- **Resolução:** 25/08/2025 — 10:02 BRT
- **Duração:** 47 minutos
- **Ambiente:** Produção
- **Serviço:** payment-api
- **Impacto:** Latência média > 2 segundos por 10 minutos, timeouts em requisições ao RDS, indisponibilidade parcial do processamento de pagamentos.
- **Detecção:** Datadog
- **Alerta crítico no Datadog:**  `ALERTA: Latência média da API acima de 2 segundos por 10 minutos`
- **Impacto:** Confirmado impacto no faturamento pela equipe de negócios.

## 🔍 Linha do Tempo
| Horário | Evento |
|---------|--------|
| 09:15   | Latência da API começa a subir acima de 2s |
| 09:16   | Alerta Datadog disparado |
| 09:18   | SRE confirma impacto e aciona Dev + DBA |
| 09:20   | Verificação de pods e métricas no Kubernetes — todos Running |
| 09:25   | Logs mostram timeouts ao acessar RDS |
| 09:28   | Métricas do RDS indicam conexões no limite e aumento de CPU |
| 09:30   | Escalado número de réplicas do payment-api de 6 para 10 |
| 09:35   | DBA aumenta temporariamente capacidade do RDS |
| 09:45   | Latência começa a cair gradualmente |
| 10:02   | Métricas normalizadas, incidente encerrado |

## 🧾 Causa Raiz
- A aplicação dessa criticidade estava executando em um cluster "comum" com recursos limitados e autoscalling inadequado para essa finalidade, no qual não esperava um volume de requisições tão alto, causando a saturação de recursos nos nodes do EKS (CPU ou memória),levando a throttling e aumento de latência no processamento das requisições.

## 🚑 Ações Imediatas (Mitigação)
- Escalonamento horinzontal dos nodes de forma manual.

## 🚑 Melhorias
- Mover a aplicação para outro cluster ou nodegroup adequado a sua criticidade.
- Criar dashboard com métricas de infraestrutura, serviço, negócio e logs, afim de disponibilizar ao NOC para acompanhamento em tempo real e para suporte em novos problemas.
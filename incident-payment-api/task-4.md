# Definir ações imediatas para mitigar o impacto

## 🎯 Objetivo
Apontar medidas rápidas e eficazes que podem ser adotadas para reduzir o impacto de um incidente crítico em produção, garantindo a continuidade parcial ou total do serviço enquanto a causa raiz é investigada.  
Essas ações têm como foco estabilizar o ambiente, proteger o negócio e preparar o terreno para uma análise mais aprofundada.

---

## 🚑 Ações Imediatas de Mitigação

### 1. Comunicação eficiente
- Notificar os times de desenvolvimento e DBAs sobre o incidente.
- Abrir uma *war room* para centralizar informações e decisões.
- Informar stakeholders de negócio sobre o impacto e as medidas em andamento.

---

### 2. Escalar horizontalmente o serviço
- Aumentar temporariamente o número de réplicas do `payment-api` para diluir a carga e melhorar a capacidade de resposta:

### 3. Reduzir carga no banco RDS
  - Ativar cache (se disponível) para consultas repetitivas.
  - Desabilitar ou adiar rotinas não críticas que usam o banco (jobs, relatórios).
  - Se possível, aumentar temporariamente a capacidade do RDS (scale-up).

### 4. Ajustar timeouts e retries
  - Reduzir o tempo de espera de chamadas para o RDS para evitar threads presas.
  - Garantir que o serviço degrade de forma controlada (ex.: fila, fallback).

### 5. Failover ou read replica
  - Se o RDS estiver degradado e houver read replica ou instância standby, considerar failover.
  - Validar com DBA antes para evitar perda de dados.

### 6. Monitoramento em tempo real
  - Criar painel temporário no Datadog com:
  - Latência da API
  - Erros 5xx
  - Conexões e CPU do RDS
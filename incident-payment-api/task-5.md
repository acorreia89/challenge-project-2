# 5. Especificar como comunicaria o progresso do incidente

## 🎯 Objetivo
Estabelecer um fluxo de comunicação claro, organizado e contínuo durante o gerenciamento de um incidente, evitando sobreposição de informações, ruído entre os times e garantindo alinhamento entre áreas técnicas e de negócio.  
A comunicação eficaz é essencial para manter a transparência, acelerar a tomada de decisão e reduzir o impacto operacional e estratégico.

---

## 📢 Comunicação de Progresso do Incidente

### 1. Abertura do Incidente
Utilizar o canal correto com as informações essenciais para iniciar o acompanhamento.

**Template de abertura:**
- **Problema:** Descrição objetiva do que está ocorrendo.
- **Hora de detecção:** Quando o alerta foi disparado ou o impacto começou.
- **Impacto atual:** Ex.: “Pagamentos com latência > 2s, risco de timeout”.
- **Times envolvidos:** SRE, Desenvolvimento, DBA.
- **Status:** Investigando / Mitigando / Resolvido.

---

### 2. Atualizações Periódicas
Definir a frequência das atualizações com base na criticidade do incidente (ex.: a cada 15 ou 30 minutos).

**Template de atualização:**
- **Status atual:** O que já foi verificado (ex.: “Pods estáveis, RDS com conexões no limite”).
- **Ações em andamento:** Ex.: “Escalando réplicas para 10, analisando métricas do banco”.
- **Próximos passos:** Ex.: “Testar failover do RDS se latência não cair em 10 min”.

---

### 3. Comunicação com Stakeholders de Negócio
Enviar atualizações simplificadas e objetivas, sem jargões técnicos, focando no impacto e nas ações de mitigação.

**Conteúdo sugerido:**
- Impacto no cliente ou faturamento.
- Medidas adotadas para mitigar o problema.
- Previsão de normalização ou próximos marcos.

---

### 4. Encerramento do Incidente
Comunicar oficialmente o encerramento no canal principal, com os principais pontos da resolução.

**Template de encerramento:**
- **Hora de resolução:** Quando o serviço foi estabilizado.
- **Ação que estabilizou:** Ex.: “Aumento de réplicas + ajuste no RDS”.
- **Confirmação de normalização:** Métricas voltaram ao padrão.
- **Próximos passos:** Análise da causa raiz (RCA) e ações preventivas.

---

### 5. Registro Pós‑Incidente
Criar e compartilhar o documento de **Postmortem** com os envolvidos, consolidando aprendizados e melhorias.

**Template de postmortem:**
- Linha do tempo dos eventos.
- Causa raiz identificada.
- Ações corretivas aplicadas.
- Melhorias no processo para evitar recorrência.

5. Especificar como comunicaria o progresso do incidente.

Objetivo

Ter um fluxo de organização claro e organizado da comunicação para que não tenha "overlap" de informações . 

Comunicação de Progresso do Incidente
1. Abertura do Incidente
    - Utilizar o canal correto de comunição com as informações corretas do problema, impacto, catagorização.

Template:
- Problema
- Hora de detecção
- Impacto atual (ex.: “Pagamentos com latência > 2s, risco de timeout”)
- Times envolvidos (SRE, Dev, DBA)
- Status


2. Atualizações Periódicas
Frequência: A definir de acordo com a categorização

Template 
- Status atual: o que já foi verificado (ex.: “Pods estáveis, RDS com conexões no limite”)
- Ações em andamento: (ex.: “Escalando réplicas para 10, analisando métricas do banco”)
- Próximos passos: (ex.: “Testar failover do RDS se latência não cair em 10 min”)


3. Comunicação com Stakeholders de Negócio
- Resumo simplificado com a comunicação menos técnica
- Impacto no cliente/faturamento
- Medidas para mitigar
- Previsão de normalização


4. Encerramento do Incidente
Comunicação inal no canal

Template
- Hora de resolução
- Ação que estabilizou o serviço
- Confirmação de normalização das métricas
- Próximos passos para análise da causa raiz (RCA)

5. Registro Pós‑Incidente
- Criar documento de Postmortem.

Template:
- Linha do tempo
- Causa raiz
- Ações corretivas
- Melhorias no processo

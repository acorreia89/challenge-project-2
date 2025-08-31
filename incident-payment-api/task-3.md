3. Apontar hipóteses prováveis sobre a causa.

Objetivo

Listar as principais hipoteses para o problema.


1. Problema no banco RDS 
    - Latência ou indisponibilidade momentânea
    - Conexões saturadas (max_connections)
    - Rede (latência entre EKS e RDS)

2. Problema de rede no cluster
    - Latência no VPC CNI
    - Security Groups ou NACL alterados

3.- Saturação de recursos no serviço
    - CPU/Memory throttling nos pods
    - Fila de requisições acumulando

4. Dependência externa degradada
    - API de terceiros usada pelo payment-api

5. Configuração de pool de conexões
    - Pool insuficiente ou mal configurado, causando timeouts
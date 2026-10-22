# TP1 – Integração de Sistemas de Informação (2026/27)
Autor: Rafael Rocha Matos a29343

## Descrição
ETL de telemetria de combates de um jogo (CSV + JSON + XML), com Pentaho
Data Integration, PostgreSQL e exportação do ranking de DPS por arma.

## Ficheiros
- dataintegration/tr_telemetria.ktr – transformação ETL
- dataintegration/job_principal.kjb – job que orquestra o ETL (ramo de sucesso e de falha)
- dataintegration/criar_tabela.sql – criação da tabela stats_combate
- data/input/ – jogadores.csv, catalogo.xml, telemetria.json
- data/output/ – ranking.csv e log_rejeitados.txt (exemplos)
- doc/<número>_doc.pdf – relatório

## Como executar
1. Instalar Pentaho Data Integration (Spoon) e PostgreSQL 18.
2. Criar a base de dados `trabalho_isi` e correr criar_tabela.sql.
3. Abrir job_principal.kjb no Spoon, configurar a ligação ao PostgreSQL
   (localhost:5432, utilizador/password próprios) e executar.

## Vídeo de demonstração
<link>
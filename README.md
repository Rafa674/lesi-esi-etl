TP1 – Integração de Sistemas de Informação (2026/27)

Autor: Rafael Rocha Matos (a29343)

Curso: Licenciatura em Engenharia de Sistemas Informáticos (IPCA)

Descrição do Projeto

Este projeto consiste no desenvolvimento de um processo de ETL (Extract, Transform, Load) para análise de telemetria de combates de um jogo. O sistema consome dados de fontes heterogéneas (CSV, JSON e XML), efetua a validação e limpeza dos mesmos (recorrendo a Expressões Regulares e tratamento de valores nulos), realiza o cruzamento de dados sequencial (Lookups) e calcula a média de DPS por arma. Os resultados finais são persistidos numa base de dados PostgreSQL e exportados para ficheiros estruturados.

Estrutura de Ficheiros

A solução encontra-se organizada na seguinte estrutura de diretórios:

doc/

a29343_doc.pdf: Relatório final do trabalho.

dataintegration/

tr_jogadores.ktr: Transformação responsável pela extração, validação (Regex) e limpeza dos dados dos utilizadores.

tr_combates.ktr: Transformação responsável pela leitura de JSON/XML, fusão de dados (Lookups), cálculos matemáticos (DPS), agrupamento e carga.

job_principal.kjb: Job mestre para a orquestração do fluxo, contemplando os ramos de sucesso e o tratamento e registo de falhas.

src/

script_database.sql: Script SQL para a criação da tabela stats_combate no PostgreSQL.

data/input/

jogadores.csv: Ficheiro de origem com os dados dos utilizadores.

catalogo.xml: Dicionário estruturado de armas e bosses.

telemetria.json: Registos em bruto dos combates efetuados.

data/output/

jogadores_limpos.csv: Ficheiro intermédio gerado com os utilizadores validados.

ranking.csv: Ficheiro final exportado com o ranking de DPS por arma.

log_rejeitados.txt: Ficheiro de log unificado contendo os registos invalidados durante o processo (e-mails inválidos e durações a zero).

Como Executar a Solução

1. Pré-requisitos

Instalar o Pentaho Data Integration (Spoon).

Instalar o servidor PostgreSQL 18 (com interface pgAdmin).

2. Configuração da Base de Dados

Criar uma base de dados local designada trabalho_isi no PostgreSQL.

Executar o script localizado em src/script_database.sql para criar a estrutura da tabela stats_combate.

3. Execução do Processo de ETL

Abrir o Pentaho Spoon e carregar o ficheiro orquestrador: dataintegration/job_principal.kjb.

Na transformação tr_combates.ktr, confirmar que as credenciais de acesso ao PostgreSQL (host: localhost:5432, utilizador e palavra-passe) estão corretamente configuradas no passo Table Output.

Executar o Job clicando em Run.

4. Verificação de Resultados

A tabela stats_combate na base de dados PostgreSQL deverá estar populada com as armas e o respetivo DPS médio.

Os ficheiros de relatório (ranking.csv e log_rejeitados.txt) estarão atualizados no diretório data/output/.

Vídeo de Demonstração

Link de acesso: https://drive.google.com/file/d/1PoCZxXenJ9IUvD5AxpHDPqI3ZefThgby/view?usp=sharing
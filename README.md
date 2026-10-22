# TP1 – Information Systems Integration (2026/27)

**Author:** Rafael Rocha Matos (a29343)  
**Degree:** BSc in Computer Systems Engineering (IPCA)

---

## Project Description

This project consists of developing an ETL (Extract, Transform, Load) process to analyse combat telemetry from a game. The system consumes data from heterogeneous sources (CSV, JSON and XML), validates and cleans it (using Regular Expressions and null-value handling), performs sequential data joins (Lookups) and calculates the average DPS per weapon. The final results are persisted in a PostgreSQL database and exported to structured files.

---

## File Structure

The solution is organised in the following directory structure:

- `doc/`
  - `a29343_doc.pdf`: Final report of the project.
- `dataintegration/`
  - `tr_jogadores.ktr`: Transformation responsible for extracting, validating (Regex) and cleaning the user data.
  - `tr_combates.ktr`: Transformation responsible for reading JSON/XML, merging data (Lookups), mathematical calculations (DPS), grouping and loading.
  - `job_principal.kjb`: Master job that orchestrates the flow, covering the success branches and the handling and logging of failures.
- `src/`
  - `script_database.sql`: SQL script to create the `stats_combate` table in PostgreSQL.
- `data/input/`
  - `jogadores.csv`: Source file with the user data.
  - `catalogo.xml`: Structured dictionary of weapons and bosses.
  - `telemetria.json`: Raw records of the combats performed.
- `data/output/`
  - `jogadores_limpos.csv`: Intermediate file generated with the validated users.
  - `ranking.csv`: Final exported file with the DPS ranking per weapon.
  - `log_rejeitados.txt`: Unified log file containing the records invalidated during the process (invalid e-mails and zero durations).

---

## How to Run the Solution

### 1. Prerequisites

- Install Pentaho Data Integration (Spoon).
- Install the PostgreSQL 18 server (with the pgAdmin interface).

### 2. Database Setup

- Create a local database named `trabalho_isi` in PostgreSQL.
- Run the script located at `src/script_database.sql` to create the structure of the `stats_combate` table.

### 3. Running the ETL Process

- Open Pentaho Spoon and load the orchestrator file: `dataintegration/job_principal.kjb`.
- In the `tr_combates.ktr` transformation, confirm that the PostgreSQL access credentials (host: `localhost:5432`, username and password) are correctly configured in the Table Output step.
- Run the Job by clicking Run.

### 4. Checking the Results

- The `stats_combate` table in the PostgreSQL database should be populated with the weapons and their average DPS.
- The report files (`ranking.csv` and `log_rejeitados.txt`) will be updated in the `data/output/` directory.

---

## Demo Video

Access link: https://drive.google.com/file/d/1PoCZxXenJ9IUvD5AxpHDPqI3ZefThgby/view?usp=sharing
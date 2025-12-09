# Projeto Pipeline Big Data: Suicídio e Depressão

Este projeto consiste em um pipeline de Engenharia de Dados (ETL) desenvolvido para cruzar e analisar dados públicos da Organização Mundial da Saúde (OMS). O objetivo principal é investigar a correlação entre as taxas de suicídio e os índices de depressão em diferentes regiões.

## Tecnologias Utilizadas

* **Infraestrutura:** Docker e Docker Compose
* **Processamento:** Apache Spark (PySpark versão 3.5.1)
* **Armazenamento:** HDFS (Hadoop)
* **Consulta:** Trino
* **Visualização:** Apache Superset

## Estrutura do Projeto

```text
ProjetoBigData/
├── docker/           # Configurações de imagem (Dockerfile)
├── hadoop/           # Configs do Cluster Hadoop
├── notebooks/        # Scripts ETL (Bronze, Silver, Gold)
├── trino/            # Configuração do Query Engine
├── superset_home/    # Banco de dados do Dashboard
└── docker-compose.yml # Orquestrador do ambiente
```

 ## O Pipeline de Dados (ETL)
O fluxo de dados segue a arquitetura de medalhão (Medallion Architecture):

## Camada Bronze (Ingestão)
O notebook ingestao_bronze.ipynb realiza a conexão com a API da OMS, baixa os dados brutos em formato JSON e os armazena diretamente no HDFS.

## Camada Silver (Processamento)
O notebook processamento_silver.ipynb é responsável pela limpeza e tratamento dos dados. Nesta etapa, filtramos a dimensão BOTHSEXES (ambos os sexos) para evitar duplicidade de registros e convertemos os tipos de dados para os formatos adequados (números inteiros e decimais).

## Camada Gold (Agregação)
O notebook carga_gold.ipynb gera a tabela analítica final. Ele realiza o cruzamento (join) e a pivotagem das tabelas de suicídio e depressão, deixando os dados estruturados e prontos para serem consumidos pelo Dashboard.

Como Executar
## 1. Pré-requisitos
Certifique-se de ter o Docker e o Git instalados em sua máquina.

## 2. Clonar e Rodar
Execute os seguintes comandos no terminal:

```text
git clone [https://github.com/rafaelabiaze/projetobigdata.git](https://github.com/rafaelabiaze/projetobigdata.git)
cd ProjetobigData-etl_projetobigdata
docker-compose up -d
```

## 3. Acessar os Serviços
Após a inicialização dos containers, acesse as ferramentas nos seguintes endereços:
```text
Jupyter Notebook: localhost:8888

Superset: localhost:8088

HDFS (Namenode): localhost:9870
```
Licença
Este projeto está licenciado sob a licença MIT.
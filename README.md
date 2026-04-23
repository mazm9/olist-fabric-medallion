# OLIST Data Pipeline w Microsoft Fabric

## Opis projektu
Kompletny pipeline danych zbudowany w Microsoft Fabric z wykorzystaniem Lakehouse, Apache Spark oraz orkiestracji ETL.

Architektura oparta o model Medallion:
- Bronze
- Silver
- Gold

---

## Technologie
- Microsoft Fabric
- Lakehouse
- Apache Spark
- Notebooks
- Data Pipeline
- SQL Endpoint
- Delta Tables

---

## Architektura

```mermaid
flowchart TD

    A[Źródła danych CSV<br/>customers / orders / items / payments / products]

    A --> B[Microsoft Fabric Lakehouse<br/>Files / OneLake]

    B --> C[Notebook: Bronze Ingestion<br/>PySpark Load CSV → Delta]

    C --> D1[bronze_customers]
    C --> D2[bronze_orders]
    C --> D3[bronze_order_items]
    C --> D4[bronze_payments]
    C --> D5[bronze_products]

    D1 --> E[Notebook: Silver Transform<br/>Join + Cleansing + Standardization]
    D2 --> E
    D3 --> E
    D4 --> E
    D5 --> E

    E --> F[silver_sales]

    F --> G[Notebook: Gold KPI<br/>Aggregations]

    G --> H[gold_sales_kpi]

    H --> I[SQL Endpoint]

    I --> J[Power BI / Reporting / Analytics]

    subgraph ORCHESTRATION [Fabric Pipeline]
        P1[bronze_ingestion]
        P2[silver_transform]
        P3[gold_kpi]
        P1 --> P2 --> P3
    end

    P1 -.trigger.-> C
    P2 -.trigger.-> E
    P3 -.trigger.-> G
```

---

## Struktura projektu

```text
olist-fabric-medallion/
├── data/
├── notebooks/
│   ├── nb_bronze_ingest.ipynb
│   ├── nb_silver_transform.ipynb
│   └── nb_gold_kpi.ipynb
├── screenshots/
│   ├── workspace.png
│   ├── bronze_tables.png
│   ├── silver_table.png
│   ├── gold_table.png
│   ├── pipeline.png
│   └── diagram.png
└── README.md
```

---

## Pipeline ETL

### 1. Bronze Layer
Import danych CSV do Lakehouse.

Tabele:
- bronze_customers
- bronze_orders
- bronze_order_items
- bronze_payments
- bronze_products

![Bronze](screenshots/bronze_tables.png)

---

### 2. Silver Layer
Transformacje oraz join danych.

Tabela wynikowa:
- silver_sales

![Silver](screenshots/silver_table.png)

---

### 3. Gold Layer
Agregacje KPI.

Tabela wynikowa:
- gold_sales_kpi

![Gold](screenshots/gold_table.png)

---

## Orkiestracja

Pipeline uruchamia notebooki w kolejności:

1. bronze_ingestion
2. silver_transform
3. gold_kpi

![Pipeline](screenshots/pipeline.png)


---

## Efekt końcowy

Projekt prezentuje kompletny proces Data Engineering:

- ingest danych
- transformacje Spark
- model Medallion
- orkiestracja pipeline
- dane gotowe pod BI

---

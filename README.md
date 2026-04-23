# OLIST Data Pipeline w Microsoft Fabric

Projekt wykonany w ramach zadania z przedmiotu Przetwarzanie i Orkiestracja Danych.

## Cel projektu

Celem było przygotowanie kompletnego pipeline'u danych z wykorzystaniem skalowalnego silnika przetwarzania oraz orkiestracji zadań.

Rozwiązanie zostało zbudowane w Microsoft Fabric z użyciem Spark oraz Lakehouse.

---

## Zakres rozwiązania

Pipeline przetwarza dane e-commerce pochodzące z publicznego zbioru OLIST.

Wykorzystane pliki źródłowe:

- customers
- orders
- order_items
- payments
- products

---

## Architektura rozwiązania

Zastosowano podejście Medallion Architecture:

### Bronze Layer

Warstwa surowa. Dane CSV zostały załadowane bezpośrednio do tabel Delta.

Tabela:

- bronze_customers
- bronze_orders
- bronze_order_items
- bronze_payments
- bronze_products

### Silver Layer

Warstwa transformacji i integracji danych.

Utworzona tabela:

- silver_sales

Tabela zawiera połączone dane klientów, zamówień, produktów i płatności.

### Gold Layer

Warstwa raportowa / biznesowa.

Utworzona tabela:

- gold_sales_kpi

Zawiera miesięczne KPI:

- revenue
- liczba zamówień
- średnia wartość zamówienia

---

## Orkiestracja

Całość została spięta w Data Pipeline w Microsoft Fabric.

Kolejność wykonywania:

1. Bronze ingestion  
2. Silver transform  
3. Gold KPI

Pipeline stanowi pojedynczy punkt uruchomienia całego procesu.

---

## Technologie

- Microsoft Fabric
- Apache Spark
- Lakehouse
- Delta Tables
- Data Pipeline

---

## Screenshots

Repozytorium zawiera zrzuty ekranu pokazujące:

- strukturę tabel
- pipeline
- wyniki transformacji

---

## Możliwe rozszerzenia

- incremental refresh
- dashboard Power BI
- walidacja jakości danych
- harmonogram uruchomień pipeline
- dodatkowe KPI sprzedażowe

---

## Autor

Imię Nazwisko

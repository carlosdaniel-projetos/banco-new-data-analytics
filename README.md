# Banco New | Business Intelligence Bancário

Projeto de portfólio desenvolvido em **Power BI** para analisar a atividade, a inatividade e a recuperação de clientes de um banco fictício.

> **Aviso:** Banco New é uma marca fictícia. O conjunto de dados é sintético e histórico, utilizado exclusivamente para aprendizagem e demonstração de competências em Business Intelligence. Os indicadores não representam resultados de uma instituição financeira real.

## Objetivo

Construir uma visão gerencial interativa da carteira de clientes, monitorando atividade, risco de inatividade e reativação por período, região, cidade e perfil.

## Tecnologias

- **Kaggle:** fonte do conjunto de dados sintéticos.
- **Python + KaggleHub:** download automatizado dos arquivos.
- **CSV:** arquivos de origem utilizados no relatório.
- **Power Query (M):** importação, conversão de tipos e criação de ciclos trimestrais.
- **Power BI + DAX:** modelagem, medidas e visualizações.

## Fonte dos dados

[Banking and Customer Transaction Data — Kaggle, por Yogesh Tekawade](https://www.kaggle.com/datasets/yogeshtekawade/banking-and-customer-transaction-data)

Arquivos utilizados: `customer_data.csv`, `bank_data.csv` e `transaction_data.csv`.

## Fluxo dos dados


![Fluxo completo do projeto Banco New](./fluxo-completo-banco-new-pbi.png)


## Modelo

- `dim_bank` → `dim_customer` pela coluna `Branch_ID` (1:*).
- `dim_customer` → `fat_transaction` pela coluna `Customer_ID` (1:*).
- `dim_status_cliente`: categorias auxiliares de composição da carteira.

A estrutura principal é um modelo em floco de neve (*snowflake*).

## Regras de análise

- **Ciclos:** 4 por ano, correspondentes aos trimestres (Ciclo 01: jan–mar; Ciclo 02: abr–jun; Ciclo 03: jul–set; Ciclo 04: out–dez).
- **Inativos:** clientes com mais de 90 dias sem transações na data de referência.
- **Quase inativos:** faixa de alerta definida no modelo; consultar a versão final das medidas no PBIX.
- **Novos:** primeira transação no histórico dentro da janela definida.
- **Elegíveis à recuperação:** clientes já inativos no início da janela de acompanhamento.
- **Recuperados:** clientes elegíveis que voltaram a transacionar durante a janela.
- **Taxa de reativação:** recuperados elegíveis ÷ elegíveis no início da janela.

As janelas utilizadas nos indicadores devem ser verificadas nas medidas DAX do arquivo PBIX, pois há indicadores mensais, trimestrais e de últimos 60/90 dias.

## Dashboard

Visões construídas:

- KPIs de clientes ativos, novos, recuperados, quase inativos e inativos.
- Medidores de taxa de reativação e taxa de inatividade com metas ilustrativas.
- Composição e segmentação da carteira.
- Análise por região, cidade e perfil/canal.
- Resumo da movimentação no último mês registrado.

![Dashboard Banco New](./dashboard-banco-new.png)

## Limitações

- Dados sintéticos e históricos, sem atualização bancária em tempo real.
- Identificação de clientes novos baseada na primeira transação observada, não necessariamente na abertura de conta.
- Volumes transacionados não representam receita ou lucro bancário.
- As categorias de comportamento podem se sobrepor nos cartões; uma composição de 100% exige classificação exclusiva.

## Estado do projeto


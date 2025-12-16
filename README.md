Projeto ETL Simples com CSV em Python
Este projeto demonstra um pipeline ETL (Extract, Transform, Load) usando apenas arquivos CSV e Python (pandas).
Ele lê dados fictícios de vendas, transforma os dados para gerar insights e salva os resultados em novos arquivos CSV.



📂 Estrutura do Projeto
etl-vendas-csv/
│
├── README.md
├── etl_simples.py
└── vendas.csv


Os arquivos de saída (vendas_transformadas.csv, receita_por_produto.csv, receita_por_dia.csv) serão gerados automaticamente quando você rodar o script.

🐍 Script Python (etl_simples.py)
import pandas as pd

# 1. Extração
df = pd.read_csv("vendas.csv")

# 2. Transformação
df["valor_total"] = df["quantidade"] * df["preco_unitario"]
df["produto"] = df["produto"].str.strip().str.lower()

# Receita por produto
receita_produto = df.groupby("produto")["valor_total"].sum().reset_index()

# Receita por dia
receita_dia = df.groupby("data")["valor_total"].sum().reset_index()

# 3. Carregamento
df.to_csv("vendas_transformadas.csv", index=False)
receita_produto.to_csv("receita_por_produto.csv", index=False)
receita_dia.to_csv("receita_por_dia.csv", index=False)

print("ETL concluído! Arquivos CSV gerados com sucesso.")



📊 CSV de Entrada (vendas.csv)
id_venda,produto,quantidade,preco_unitario,data
1, Camiseta ,2,50.0,2025-12-01
2,Calça,1,120.0,2025-12-01
3,camiseta,3,50.0,2025-12-02
4,Tênis,1,300.0,2025-12-02
5,calça,2,120.0,2025-12-03
6,Boné,4,30.0,2025-12-03
7,tênis,1,300.0,2025-12-03
8,Camiseta,2,50.0,2025-12-04
9,Boné,1,30.0,2025-12-04
10,calça,3,120.0,2025-12-05

📈 CSVs Gerados
vendas_transformadas.csv
id_venda,produto,quantidade,preco_unitario,data,valor_total
1,camiseta,2,50.0,2025-12-01,100.0
2,calça,1,120.0,2025-12-01,120.0
3,camiseta,3,50.0,2025-12-02,150.0
4,tênis,1,300.0,2025-12-02,300.0
5,calça,2,120.0,2025-12-03,240.0
6,boné,4,30.0,2025-12-03,120.0
7,tênis,1,300.0,2025-12-03,300.0
8,camiseta,2,50.0,2025-12-04,100.0
9,boné,1,30.0,2025-12-04,30.0
10,calça,3,120.0,2025-12-05,360.0


receita_por_produto.csv
produto,valor_total
calça,720.0
tênis,600.0
camiseta,350.0
boné,150.0


receita_por_dia.csv
data,valor_total
2025-12-01,220.0
2025-12-02,450.0
2025-12-03,660.0
2025-12-04,130.0
2025-12-05,360.0









# 📊 Portfólio de Análise de Dados com SQL

## 💡 Introdução

Este projeto simula uma análise de vendas utilizando uma base de dados fictícia. O objetivo é extrair insights relevantes sobre o comportamento dos clientes, desempenho dos produtos e receita da loja, aplicando consultas SQL para responder perguntas de negócio.

---

## 📁 Base de Dados

A base é composta por quatro tabelas relacionais:

- **clientes**: informações dos clientes (ID, nome, cidade)
- **produtos**: catálogo de produtos (ID, nome, categoria, preço unitário)
- **vendas**: dados das vendas (ID, cliente, data, total)
- **itens_venda**: produtos vendidos em cada venda (quantidade, produto)

---

## ❓ Perguntas de Negócio Respondidas

- Qual produto foi mais vendido?
- Qual cliente mais comprou?
- Qual a receita mensal da loja?
- Qual categoria teve maior faturamento?

---

## 🛠️ Ferramentas Utilizadas

- SQL (SQLite)
- Excel (Tabelas Dinâmicas e Gráficos)
- Power BI (opcional)

---

## 📊 Visualizações

### Excel  
<img width="3200" height="2400" alt="imagensexcel_graficos png" src="https://github.com/user-attachments/assets/5e461e7a-9a40-447a-8ed8-d6fbff7b2cba" />

### Power BI  
<img width="1600" height="1000" alt="imagenspowerbi_graficos png" src="https://github.com/user-attachments/assets/48a1e656-dcdf-428f-84b6-dfaf865714b4" />

---

## 🧠 Exemplos de Consultas SQL

```sql
-- 1. Qual produto foi mais vendido?
SELECT 
    p.nome_produto,
    SUM(iv.quantidade) AS total_vendido
FROM 
    itens_venda iv
JOIN 
    produtos p ON iv.produto_id = p.produto_id
GROUP BY 
    p.nome_produto
ORDER BY 
    total_vendido DESC;

-- 2. Qual cliente mais comprou?
SELECT 
    c.nome,
    SUM(v.total_venda) AS total_comprado
FROM 
    vendas v
JOIN 
    clientes c ON v.cliente_id = c.cliente_id
GROUP BY 
    c.nome
ORDER BY 
    total_comprado DESC;

-- 3. Qual a receita mensal da loja?
SELECT 
    strftime('%Y-%m', v.data_venda) AS mes,
    SUM(v.total_venda) AS receita_mensal
FROM 
    vendas v
GROUP BY 
    mes
ORDER BY 
    mes;

-- 4. Qual categoria teve maior faturamento?
SELECT 
    p.categoria,
    SUM(iv.quantidade * p.preco_unitario) AS faturamento
FROM 
    itens_venda iv
JOIN 
    produtos p ON iv.produto_id = p.produto_id
GROUP BY 
    p.categoria
ORDER BY 
    faturamento DESC;

#Conclusão
✅ Conclusão
Este projeto mostra como SQL pode ser aplicado na análise de dados para responder perguntas de negócio e gerar insights valiosos. As visualizações em Excel e Power BI complementam a análise técnica e tornam a comunicação mais clara.


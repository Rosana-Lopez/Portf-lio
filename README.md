# Portfólio de Análise de Dados com SQL

## Introdução

Este projeto simula uma análise de vendas utilizando uma base de dados fictícia. O objetivo é extrair insights relevantes sobre o comportamento dos clientes, desempenho dos produtos e receita da loja, aplicando consultas SQL para responder perguntas de negócio.

---

## Base de Dados

A base de dados é composta por quatro tabelas relacionais:

- **clientes**: informações dos clientes (ID, nome, cidade)
- **produtos**: catálogo de produtos (ID, nome, categoria, preço unitário)
- **vendas**: dados das vendas (ID, cliente, data, total)
- **itens_venda**: produtos vendidos em cada venda (quantidade, produto)

---

## Perguntas de Negócio Respondidas

- Qual produto foi mais vendido?
- Qual cliente mais comprou?
- Qual a receita mensal da loja?
- Quais produtos não foram vendidos?
- Qual categoria teve maior faturamento?

---

## Ferramentas Utilizadas

- SQL (SQLite)
- Excel para análise e visualização
- Power BI (opcional)

---

## Exemplos de Queries SQL

```sql
-- Produto mais vendido
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
    total_vendido DESC
LIMIT 10;

# 📊 Projeto: Análise de Vendas com SQL

## 💡 Objetivo

Este projeto tem como objetivo explorar os dados de uma loja fictícia para extrair insights relevantes, como produtos mais vendidos, clientes que mais compram e receita mensal. Utilizamos SQL para manipular e analisar os dados, e Excel para criar visualizações gráficas que facilitam a interpretação.

---

## 🛠️ Ferramentas Utilizadas

- SQL (SQLite)
- Excel (Tabelas Dinâmicas e Gráficos)
- Power BI (opcional)

---

## 📁 Estrutura do Projeto

# 📊 Projeto: Análise de Vendas com SQL

## 💡 Objetivo

Este projeto tem como objetivo explorar os dados de uma loja fictícia para extrair insights relevantes, como produtos mais vendidos, clientes que mais compram e receita mensal. Utilizamos SQL para manipular e analisar os dados, e Excel para criar visualizações gráficas que facilitam a interpretação.

---

## 🛠️ Ferramentas Utilizadas

- SQL (SQLite)
- Excel (Tabelas Dinâmicas e Gráficos)
- Power BI (opcional)

---

## 📁 Estrutura do Projeto

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

-- 3. Qual a receita total por mês?
-- (Formato para SQLite)
SELECT 
    strftime('%Y-%m', v.data_venda) AS mes,
    SUM(v.total_venda) AS receita_mensal
FROM 
    vendas v
GROUP BY 
    mes
ORDER BY 
    mes;

-- 4. Quais produtos não foram vendidos?
SELECT 
    p.nome_produto
FROM 
    produtos p
LEFT JOIN 
    itens_venda iv ON p.produto_id = iv.produto_id
WHERE 
    iv.produto_id IS NULL;

-- 5. Qual categoria teve mais faturamento?
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

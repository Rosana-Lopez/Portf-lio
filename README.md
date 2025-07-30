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



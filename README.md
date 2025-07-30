# Portf-lio
Utilizei uma base fictícia de vendas para responder perguntas de negócio como "qual produto mais vendido por região", "faturamento mensal", "clientes inativos", etc. Criei queries SQL para gerar insights, além de visualização com Excel/Power BI.
## 📂 Base de Dados

O projeto utiliza um banco fictício com 4 tabelas:

- **clientes**: informações de clientes (id, nome, cidade)
- **produtos**: catálogo de produtos (id, nome, categoria, preço)
- **vendas**: informações sobre cada venda (id, data, cliente, total)
- **itens_venda**: itens comprados em cada venda (quantidade, produto)

---

## ❓ Perguntas de Negócio Respondidas

- Qual produto foi mais vendido?
- Qual cliente mais comprou?
- Receita por mês
- Produtos não vendidos
- Faturamento por categoria

---

## 🧠 Exemplo de Query

```sql
SELECT nome_produto, SUM(quantidade) AS total_vendido
FROM itens_venda
JOIN produtos ON itens_venda.produto_id = produtos.produto_id
GROUP BY nome_produto
ORDER BY total_vendido DESC;


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



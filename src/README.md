### **🦆 DuckDB Quick Starter para Usuários de PostgreSQL**  

Se você já conhece **PostgreSQL**, pode usar **DuckDB** diretamente no terminal sem precisar de configuração.  
Aqui estão os principais comandos **SQL** para rodar no **DuckDB CLI**.

---

## **1️⃣ Criar e Usar um Banco de Dados**
```sql
-- Criar um banco de dados chamado "meudb.duckdb"
ATTACH 'meudb.duckdb' AS meudb;
```
Isso cria um **arquivo de banco de dados** persistente.

---

## **2️⃣ Criar uma Tabela**
```sql
CREATE TABLE meudb.usuarios (
    id INTEGER PRIMARY KEY,
    nome TEXT,
    email TEXT UNIQUE,
    idade INTEGER,
    criado_em TIMESTAMP DEFAULT now()
);
```
**📝 Observações:**  
✅ DuckDB usa `TEXT` em vez de `VARCHAR`.  
✅ `TIMESTAMP DEFAULT now()` adiciona a data e hora automaticamente.  

---

## **3️⃣ Inserir Dados**
```sql
INSERT INTO meudb.usuarios (id, nome, email, idade) VALUES
    (1, 'Alice', 'alice@email.com', 25),
    (2, 'Bob', 'bob@email.com', 30),
    (3, 'Carol', 'carol@email.com', 22);
```

✅ **No DuckDB, você pode inserir múltiplas linhas de uma vez!** 🚀  

---

## **4️⃣ Consultar os Dados**
```sql
SELECT * FROM meudb.usuarios;
```

🔹 **Filtrar por idade:**  
```sql
SELECT nome, idade FROM meudb.usuarios WHERE idade > 25;
```

🔹 **Ordenar resultados:**  
```sql
SELECT * FROM meudb.usuarios ORDER BY idade DESC;
```

🔹 **Contar registros:**  
```sql
SELECT COUNT(*) FROM meudb.usuarios;
```

---

## **5️⃣ Atualizar e Deletar Dados**
```sql
-- Atualizar a idade de Bob
UPDATE meudb.usuarios SET idade = 35 WHERE nome = 'Bob';

-- Deletar um usuário
DELETE FROM meudb.usuarios WHERE nome = 'Carol';
```

---

## **6️⃣ Trabalhando com Agregações**
🔹 **Média de idade dos usuários:**  
```sql
SELECT AVG(idade) AS idade_media FROM meudb.usuarios;
```

🔹 **Quantidade de usuários por idade:**  
```sql
SELECT idade, COUNT(*) FROM meudb.usuarios GROUP BY idade;
```

🔹 **Maior e menor idade:**  
```sql
SELECT MIN(idade) AS menor_idade, MAX(idade) AS maior_idade FROM meudb.usuarios;
```

---

## **7️⃣ Trabalhando com Datas**
🔹 **Ver usuários cadastrados nos últimos 7 dias:**  
```sql
SELECT * FROM meudb.usuarios WHERE criado_em > now() - INTERVAL '7 days';
```

🔹 **Formatar data:**  
```sql
SELECT nome, STRFTIME('%Y-%m-%d', criado_em) AS data_criacao FROM meudb.usuarios;
```

---

## **8️⃣ Exportar e Importar Dados**
🔹 **Salvar dados em CSV:**  
```sql
COPY meudb.usuarios TO 'usuarios.csv' WITH (HEADER, DELIMITER ',');
```

🔹 **Carregar CSV para o DuckDB:**  
```sql
CREATE TABLE meudb.novos_usuarios AS SELECT * FROM read_csv_auto('usuarios.csv');
```

🔹 **Ler arquivos Parquet diretamente:**  
```sql
SELECT * FROM read_parquet('dados.parquet') LIMIT 10;
```

---

## **🔥 Conclusão**
Agora você pode usar **DuckDB como um mini PostgreSQL local**, sem precisar de servidor! 🚀  
Se precisar de mais comandos ou quiser testar funções avançadas, me avise! 🔥🔥
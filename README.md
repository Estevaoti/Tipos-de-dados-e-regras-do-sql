Facsenac
# Tipos de Dados e Regras na Modelagem SQL 

##  Introdução

Quando a gente cria um banco de dados, precisa dizer **que tipo de informação** vai guardar ali dentro.
Por exemplo: números? textos? datas? imagens?
É aí que entram os **tipos de dados**.
E além disso, também temos as **regras** que garantem que os dados fiquem certinhos, sem bagunça nem erro.
Vamos ver isso na prática!

---

## 🔢 Tipos de Dados em SQL

### 1. Numéricos

São usados pra guardar **números** (óbvio).
Servem pra coisas tipo idade, preço, quantidade, etc.

| Tipo            | Pra que serve                                    | Exemplo      |
| --------------- | ------------------------------------------------ | ------------ |
| `INT`           | Número inteiro                                   | 25, 100, -10 |
| `DECIMAL(p, s)` | Número com casas decimais (p = total, s = casas) | 12.50        |
| `FLOAT`         | Número com ponto flutuante (menos preciso)       | 3.14159      |

 **Exemplo:**

```sql
CREATE TABLE produto (
  id INT,
  nome VARCHAR(100),
  preco DECIMAL(10,2)
);
```

Aqui, o `preco` aceita números tipo `49.90`.

---

### 2. Texto (Strings)

Pra guardar **palavras, frases, letras, descrições, nomes...**

| Tipo         | Pra que serve                            | Exemplo                               |
| ------------ | ---------------------------------------- | ------------------------------------- |
| `CHAR(n)`    | Texto fixo (sempre ocupa o mesmo espaço) | "PE"                                  |
| `VARCHAR(n)` | Texto variável (tamanho muda)            | "Recife"                              |
| `TEXT`       | Textos grandes                           | "Descrição completa de um produto..." |

 **Exemplo:**

```sql
CREATE TABLE cliente (
  id INT,
  nome VARCHAR(50),
  cidade CHAR(2)
);
```

---

### 3. Data e Hora ⏰

Pra guardar **datas, horários ou os dois juntos**.

| Tipo       | Pra que serve      | Exemplo               |
| ---------- | ------------------ | --------------------- |
| `DATE`     | Só data            | '2025-10-07'          |
| `TIME`     | Só hora            | '15:45:00'            |
| `DATETIME` | Data e hora juntas | '2025-10-07 15:45:00' |

 **Exemplo:**

```sql
CREATE TABLE pedido (
  id INT,
  data_pedido DATE,
  hora_entrega TIME
);
```

---

### 4. Outros tipos

Além dos básicos, SQL também tem outros tipos especiais:

| Tipo      | Uso                                             |
| --------- | ----------------------------------------------- |
| `BOOLEAN` | Verdadeiro ou falso (1/0)                       |
| `BLOB`    | Arquivos grandes (imagens, PDFs)                |
| `JSON`    | Dados em formato JSON (em bancos mais modernos) |

---

##  Regras e Restrições na Modelagem SQL

Essas **regras** servem pra garantir que os dados façam sentido e não virem bagunça.

### 1. Integridade da Entidade

Cada registro precisa ser **único**.
Ou seja, cada linha tem uma **chave primária (PRIMARY KEY)** que identifica ela.

 **Exemplo:**

```sql
CREATE TABLE aluno (
  id_aluno INT PRIMARY KEY,
  nome VARCHAR(50)
);
```

Assim, dois alunos não podem ter o mesmo `id_aluno`.

---

### 2. Integridade Referencial

Garante que uma informação **ligada a outra tabela** realmente exista.
É o que chamamos de **chave estrangeira (FOREIGN KEY)**.

 **Exemplo:**

```sql
CREATE TABLE curso (
  id_curso INT PRIMARY KEY,
  nome VARCHAR(50)
);

CREATE TABLE aluno (
  id_aluno INT PRIMARY KEY,
  nome VARCHAR(50),
  id_curso INT,
  FOREIGN KEY (id_curso) REFERENCES curso(id_curso)
);
```

Aqui, um aluno só pode estar em um curso que exista na tabela `curso`.

---

### 3. Integridade de Chave

Evita que duas linhas tenham o mesmo valor em uma coluna que deveria ser única.
É tipo uma extensão da integridade da entidade.

 **Exemplo:**

```sql
CREATE TABLE usuario (
  id INT PRIMARY KEY,
  email VARCHAR(100) UNIQUE
);
```

O `UNIQUE` impede que dois usuários usem o mesmo e-mail.

---

## 🧮 Exemplo completo de modelagem

Aqui um mini-modelo misturando tudo que vimos:

```sql
CREATE TABLE cliente (
  id_cliente INT PRIMARY KEY,
  nome VARCHAR(50),
  cpf CHAR(11) UNIQUE
);

CREATE TABLE pedido (
  id_pedido INT PRIMARY KEY,
  data_pedido DATETIME,
  valor_total DECIMAL(10,2),
  id_cliente INT,
  FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente)
);
```

👉 Temos:

* Tipos de dados variados (`INT`, `VARCHAR`, `CHAR`, `DECIMAL`, `DATETIME`);
* Regras (`PRIMARY KEY`, `UNIQUE`, `FOREIGN KEY`).

---

## 📚 Fontes e Materiais Úteis

Quer aprender mais? Dá uma olhada nesses conteúdos:

* [W3Schools - SQL Data Types](https://www.w3schools.com/sql/sql_datatypes.asp)
* [Alura - Tipos de Dados no SQL](https://www.alura.com.br/artigos/tipos-de-dados-no-sql)
* [DevMedia - Regras de Integridade no SQL](https://www.devmedia.com.br/)
* [Documentação oficial do MySQL](https://dev.mysql.com/doc/)
* [YouTube - Canal Bóson Treinamentos (Banco de Dados)](https://www.youtube.com/@bosontreinamentos)

---

##  Conclusão

Saber escolher o tipo de dado certo e aplicar as regras de integridade é o que faz seu banco de dados **ser confiável e rápido**.
Sem isso, tudo vira bagunça!
Então, da próxima vez que for criar uma tabela, lembra:
 tipo certo +  regra certa =  banco de dados organizado!

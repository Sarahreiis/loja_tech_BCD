# 🛒 Loja Tech - Banco de Dados Relacional (MySQL)

![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)

## 📋 Sobre o Projeto

O **Loja Tech** é um projeto prático de modelagem, implementação e manipulação de um banco de dados relacional voltado para um e-commerce de produtos de tecnologia e informática. 

O repositório está organizado de forma progressiva, abrangendo desde a criação da estrutura física (DDL) e carga de dados iniciais (DML), até consultas analíticas (DQL), rotinas automatizadas com **Stored Procedures** e abstração/segurança de dados com **Views** (incluindo boas práticas voltadas à LGPD).

---

## 🗂️ Estrutura do Repositório

Os scripts SQL estão numerados na ordem exata em que devem ser executados:

| Arquivo | Descrição | Conceitos Abordados |
| :--- | :--- | :--- |
| **`01.sql`** | **Estrutura e Carga Inicial** | Criação do banco `loja_tech`, definição de tabelas, chaves primárias/estrangeiras, colunas geradas (`STORED`), `ENUM`, `TIMESTAMP` e inserção de registros iniciais. |
| **`02.sql`** | **Consultas e Relatórios** | Filtros simples e compostos (`WHERE`, `LIKE`, `AND`), ordenação (`ORDER BY`), funções de agregação (`COUNT`, `SUM`), apelidos (`AS`) e junções (`INNER JOIN`). |
| **`03.sql`** | **Stored Procedures** | Criação de procedimentos armazenados sem parâmetros, com parâmetros de entrada (`IN`) para leitura, inserção e atualização, e parâmetros de saída (`OUT`). |
| **`04.sql`** | **Views (Visões)** | Criação de tabelas virtuais para mascaramento de dados sensíveis (LGPD), filtros recorrentes, simplificação de `JOINs` e agrupamentos (`GROUP BY`). |

---

## 🗄️ Arquitetura do Banco de Dados

O banco de dados `loja_tech` é composto por **6 tabelas principais**:

* **`categorias`**: Armazena os departamentos dos produtos (Notebooks, Smartphones, Periféricos, etc.).
* **`produtos`**: Catálogo de itens vinculados a uma categoria, com controle de preço, estoque atual e estoque mínimo.
* **`clientes`**: Cadastro de consumidores com restrições de unicidade (`UNIQUE`) para e-mail e CPF.
* **`pedidos`**: Cabeçalho das vendas realizadas, controlando o status (`pendente`, `processando`, `enviado`, `entregue`, `cancelado`) e valor total.
* **`itens_pedido`**: Tabela associativa que detalha os produtos de cada pedido, possuindo uma coluna calculada automaticamente (`subtotal`).
* **`log_operacoes`**: Tabela destinada à auditoria de operações executadas no sistema.

### Relacionamentos Principais
* `categorias (1) ────── (N) produtos`
* `clientes (1) ──────── (N) pedidos`
* `pedidos (1) ───────── (N) itens_pedido`
* `produtos (1) ──────── (N) itens_pedido`

---

## ⚡ Funcionalidades Destacadas

### 🔄 Stored Procedures (`03.sql`)
* `listar_categorias_ativas()`: Retorna todas as categorias ativas em ordem alfabética.
* `buscar_pedidos_por_status(p_status)`: Filtra pedidos de acordo com o status informado.
* `inserir_categoria(p_nome, p_descricao)`: Automatiza o cadastro de novas categorias.
* `atualizar_telefone_cliente(p_id_cliente, p_telefone)`: Atualiza o contato de um cliente específico.
* `contar_produtos_categoria(p_id_categoria, OUT p_total)`: Retorna a quantidade de produtos cadastrados em uma categoria via variável de saída.

### 👁️ Views (`04.sql`)
* `vw_clientes_publico`: Oculta o CPF e a data de nascimento dos clientes, permitindo consultas seguras pela equipe de marketing em conformidade com a **LGPD**.
* `vw_produtos_promocao`: Lista apenas produtos com valor abaixo de R$ 500,00.
* `vw_pedidos_pendentes`: Facilita o acompanhamento diário da equipe de atendimento/logística.
* `vw_produtos_categorias`: Abstrai o `INNER JOIN` entre produtos e categorias para relatórios gerenciais.
* `vw_total_por_cliente`: Consolida a quantidade de pedidos e o volume financeiro gasto por cada cliente.

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
* **MySQL Server** (versão 8.0 ou superior recomendada)
* Um cliente SQL de sua preferência (**MySQL Workbench**, **DBeaver**, **DataGrip** ou terminal).

### Passo a Passo
1. Clone este repositório ou baixe os arquivos `.sql`:
   ```bash
   git clone https://github.com/seu-usuario/loja-tech-db.git
   ```
2. Abra o seu cliente MySQL e conecte-se ao seu servidor local.
3. Execute os scripts rigorosamente na seguinte ordem:
   1. Execute o arquivo **`01.sql`** para criar o banco de dados, as tabelas e popular os dados iniciais.
   2. Execute o arquivo **`02.sql`** para testar as consultas de negócio.
   3. Execute o arquivo **`03.sql`** para criar e testar as *Stored Procedures*.
   4. Execute o arquivo **`04.sql`** para criar e consultar as *Views*.

---

## 🛠️ Tecnologias Utilizadas

* **MySQL** (SGBD Relacional)
* **SQL** (DDL, DML, DQL, DTL)

---

## 👤 Autor

Desenvolvido como projeto de estudo e prática em Banco de Dados Relacionais.

* **Seu Nome** – [LinkedIn](https://linkedin.com) | [GitHub](https://github.com)
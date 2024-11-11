# Banco de Dados para Sistema de Gestão de Clientes e Vendas

Este projeto consiste em um banco de dados para gerenciar clientes, funcionários, vendas, produtos, folha de pagamento e bônus. Foi desenvolvido em SQL e inclui tabelas e inserções de dados para uma estrutura inicial.

## Estrutura do Banco de Dados

### Tabelas Principais

1. **CLIENTE**: Armazena informações dos clientes, incluindo nome, endereço, telefone e status. Cada cliente pode ter uma ou mais vendas associadas.
    - **Campos**:
      - `CD_CLIENTE` (PK): Código único do cliente.
      - `NOME`: Nome do cliente.
      - `SOBRENOME`: Sobrenome do cliente.
      - `ENDERECO`: Endereço do cliente.
      - `CIDADE`: Cidade onde o cliente reside.
      - `ESTADO`: Estado do cliente.
      - `DATA_NASCIMENTO`: Data de nascimento do cliente.
      - `DATA_CADASTRO`: Data de cadastro do cliente.
      - `TELEFONE`: Número de telefone.
      - `EMAIL`: Email do cliente.
      - `SITUACAO`: Situação atual do cliente ('C', 'A', 'S', etc.).
      
2. **FUNC_LOJA**: Armazena informações dos funcionários da loja, incluindo nome, endereço, telefone, salário e datas de início e fim de contrato.
    - **Campos**:
      - `CD_FUNC` (PK): Código único do funcionário.
      - `NOME`: Nome do funcionário.
      - `SOBRENOME`: Sobrenome do funcionário.
      - `ENDERECO`: Endereço do funcionário.
      - `CIDADE`: Cidade onde o funcionário trabalha.
      - `ESTADO`: Estado do funcionário.
      - `TELEFONE`: Número de telefone do funcionário.
      - `SALARIO`: Salário do funcionário.
      - `DATA_INICIO`: Data de início do contrato.
      - `DATA_FIM`: Data de fim do contrato (ou NULL se estiver ativo).

3. **FOLHA_PAGTO**: Registra a folha de pagamento dos funcionários, incluindo salário, comissões e descontos.
    - **Campos**:
      - `NR_ITEM_PAGTO` (PK): Número do item de pagamento.
      - `ANO_MES`: Período da folha de pagamento.
      - `SALARIO`: Salário do funcionário.
      - `COMISSAO`: Comissão recebida pelo funcionário.
      - `TOTAL`: Valor total do pagamento (salário + comissão - desconto).
      - `DESCONTO`: Descontos aplicados.
      - `CD_FUNC` (FK): Código do funcionário relacionado.

4. **VENDA**: Armazena as informações sobre cada venda, incluindo o tipo de pagamento e o cliente e funcionário associados.
    - **Campos**:
      - `NR_PEDIDO` (PK): Número do pedido de venda.
      - `ST_PEDIDO`: Status do pedido.
      - `TIPO_PGTO`: Tipo de pagamento (Cartão, Dinheiro, Boleto, etc.).
      - `DATA_PEDIDO`: Data do pedido.
      - `CD_FUNC` (FK): Código do funcionário que realizou a venda.
      - `CD_CLIENTE` (FK): Código do cliente que realizou a compra.

5. **PRODUTO**: Armazena informações dos produtos disponíveis para venda.
    - **Campos**:
      - `CD_PRODUTO` (PK): Código do produto.
      - `DS_PRODUTO`: Descrição do produto.
      - `TP_PRODUTO`: Tipo do produto.
      - `VALOR`: Valor unitário do produto.

6. **ITEM_VENDA**: Relaciona os produtos às vendas específicas, indicando quantidade e status.
    - **Campos**:
      - `NR_ITEM_VENDA` (PK): Número do item da venda.
      - `QTDE_ITEM`: Quantidade do item vendido.
      - `SITUACAO_ITEM`: Situação do item (Aprovado, Pendente, etc.).
      - `NR_PEDIDO` (FK): Número do pedido.
      - `CD_PRODUTO` (FK): Código do produto vendido.

7. **BONUS**: Registra as informações de bônus por tempo de serviço dos funcionários.
    - **Campos**:
      - `NR_BONUS` (PK): Número do bônus.
      - `QT_TEMPO_CA`: Tempo de casa para aplicar o bônus (ex: "12 meses").
      - `PCT_BONUS_S`: Percentual de bônus sobre o salário.

## Relacionamentos entre as Tabelas

- **FOLHA_PAGTO**: Relaciona-se com a tabela **FUNC_LOJA** pelo campo `CD_FUNC`.
- **VENDA**: Relaciona-se com as tabelas **CLIENTE** e **FUNC_LOJA** através dos campos `CD_CLIENTE` e `CD_FUNC`, respectivamente.
- **ITEM_VENDA**: Relaciona-se com a tabela **VENDA** pelo campo `NR_PEDIDO` e com a tabela **PRODUTO** pelo campo `CD_PRODUTO`.

## Inserção de Dados

Cada tabela já inclui inserções iniciais de dados para testes. Por exemplo:

```sql
INSERT INTO CLIENTE (CD_CLIENTE, NOME, SOBRENOME, ENDERECO, CIDADE, ESTADO, DATA_NASCIMENTO, DATA_CADASTRO, TELEFONE, EMAIL, SITUACAO) 
VALUES 
(1, 'Joao', 'Silva', 'Rua A, 123', 'Cidade A', 'AA', TO_DATE('1990-JAN-01', 'YYYY-MON-DD'), SYSDATE, '1234567890', 'joao@example.com', 'C');

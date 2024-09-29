## Criando tabelas:

- Quando queremos colocar um nome com espaços podemos usar colchetes;
```SQL
CREATE TABLE [TABELA COM ESPAÇO] (/* ... */);
```

- A sintaxe de nomenclatura dos campos durante a criação é um pouco distinta:
```SQL
/* ... */
[NOME_CAMPO] [CHAR] (10)
/* ... */
```

- Existe um tipo exclusivo do SQL Server referente a valores monetários, possuindo variações de tamanho:
```SQL
[salario] [MONEY],
[preco]   [SMALLMONEY]
```

- Não existe propriamente o valor BOOLEAN/BOOL, mas sim o valor BIT (0 / 1).

- Alterando uma coluna de uma tabela:
```SQL
// Column redefinition é como se estivessemos declarando de novo a coluna
ALTER TABLE <table_name> ALTER COLUMN <column_redefinitions>;

// Adicionando restrições:
ALTER TABLE <table_name> ADD CONSTRAINT <constranit>

// Exemplos:
ALTER TABLE [clientes] ALTER COLUMN [cpf] [char] (11) NOT NULL;

ALTER TABLE [clientes] ADD CONSTRAINT pk_cliente PRIMARY KEY CLUSTERED ([cpf]);
```


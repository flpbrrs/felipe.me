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
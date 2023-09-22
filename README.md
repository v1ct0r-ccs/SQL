# SQL

## DDL - Data Definition Lenguage

É um conjunto de instruções e comandos para definição de dados.

### Comandos DDL

- CREATE TABLE
- DROP TABLE
- ALTER TABLE
- TRUNCATE

#### Sintaxe Create Table

**CREATE TABLE** *nome_tabela* (campo e tipo campo);

- **Exemplo**:
```
create table pessoa (
    id bigint,
    nome varchar (50),
    endereco text,
    telefone int
);
```
##### Tipos de dados

- Numéricos inteiros;
- Numéricos fracionários;
- Caracteres;
- Data e Hora;
- Literais;

###### Numéricos inteiros

- Tipo
    - Tamanho
        - Faixa

- smallint
    - 2 bytes
        - -32768 to +32767

- integer
    - 4 bytes
        - -2147483648 to +2147483647

- bigint
    - 8 bytes
        - -9223372036854775808 to +9223372036854775807

###### Numéricos fracionários

- Tipo
    - Tamanho
        - Faixa

- Decimal
    - variable
        - no limit

- numeric
    - variable
        - no limit

- real
    - 4 bytes
        - 6 decimal digits precison

- double precision
    - 8 bytes
        - 15 decimal digits precision

###### Caracteres

- Descrição
    - Tipo

- character varying(n)
    - comprimento variavel com limite

- varchar(n)
    - comprimento variável com limite

- character(n)
    - comprimento fixo, completado com brancos

- char(n)
    - comprimento fixo, completado com brancos

- text
    - comprimento variável não limitado

###### Data e Hora

- Descrição
    - Tipo

- Timestamp without Time Zone
    - tanto data quanto hora

- Timestamp with Time Zone (Timestamptz)
    - tanto data quanto hora

- Interval
    - intervalos de tempo

- Time without Time Zone
    - somente a hora do dia

- Time with Time Zone
    - somente a hora do dia

- Date
    - Data sem hora do dia

###### Literais

- Tipo Booleano
    - Valor

- boolean
    - 't', 'true', 'y', 'yes', '1'

- boolean
    - 'f', 'false', 'n', 'no', '0'

##### Exemplo Create Table

```
create table pessoa (
    numero_pequeno smallint,
    numero_medio int,
    numero_grande bigint,
    numero_dec decimal,
    numero_num numeric,
    numero_real real,
    numero_dou double precision,
    chv character varying(10),
    char character(10),
    val valchar(10),
    cha char(10),
    tex text,
    data1 timestamp,
    tadatz, timestamptz,
    data2 date, 
    bool boolean
);0
```

#### Sintaxe Alter Table

**ALTER TABLE** *table_name* action;

- **Alter Table** - *rename column*

Comando usado para renomear uma coluna em uma tabela existente.
```
ALTER TABLE table_name
RENAME COLUMN column_name
TO new_column_name;
```

- **Alter Table** - *add column*

Comando usado para adicionar uma coluna em uma tabela existente.

```
ALTER TABLE table_name
ADD COLUMN column_name datatype;
```
- **Alter Table** - *drop column*

Comando usado para remover uma coluna de uma tabela existente.

```
ALTER TABLE table_name
DROP COLUMN column_name;
```

- **Alter Table** - *defaults values*

Comando usado para adicionar ou remover valores defaults em uma coluna em uma tabela existente.

```
ALTER TABLE table_name
ALTER COLUMN column_name
SET DEFAULT value; | DROP DEFAULT;
```

- **Alter Table** - *constraint not null*

Comando usado para adicionar ou remover uma constraint not null(*restrição*) duma coluna de uma tabela existente.

```
ALTER TABLE tabela_name
ALTER COLUMN column_name
SET NOT NULL; | DROP NOT NULL;
```

- **Alter Table** - *constraint check*

Comando usado para adicionar ou remover uma constraint(*restrição*) em uma coluna em uma tabela existente.

```
ALTER TABLE table_name
ADD CHECK expression;
```

- **Alter Table** - *rename table*

Comando usado para renomear uma tabela existente.

```
ALTER TABLE table_name
RENAME TO new_table_name;
```

#### Truncate Table

Comando usado para limpar todos os dados de uma tabela existente.

```
TRUNCATE TABLE table_name;
```

**AVISO: Cuidado ao utilizar este comando, pois o mesmo limpa os dados da tabela e não é possivel recuperar os dados.**

- **Drop Table**

Comando usado para excluir a tabela

```
DROP TABLE table_name
```

## DML - Data Manipulation Language

Linguagem de Manipulação de Dados. São os comandos que interagem com os dados dentro das tabelas.

### Comandos DML

- INSERT
- DELETE
- UPDATE

`DQL` - Data Query Language (*Linguagem de Consulta de Dados*). São os comandos de consulta.

- **Exemplo Select**:
```
select * from pessoa;
```

#### Sintaxe Insert

**INSERT INTO** *table_name* (column_name) values (values);

- **Exemplo Insert**

```
insert into pessoa (id, nome, idade) values (1, 'Victor', 29);
insert into pessoa values (1, 'Victor', 29);
```

#### Sintaxe Update

**UPDATE** *nome_tabela* **set** *nome_campo* = valor;
**UPDATE** *nome_tabela* **set** *nome_campo* = valor **where** *nome_campo* = valor;

**AVISO: Cuidado ao atulizar pois sem o `where nome_campo = valor` ele vai atualizar todos os datos da sua tabela para o mesmo valor. Muito importante usar a cláusula **where**.

- **Exemplo Update**

```
update pessoa
set nome = 'Victor Bruno';

update pessoa
set nome = 'Victor Bruno'
where id = 1;

update pessoa
set nome = 'Victor Bruno', idade = 29
where id = 2;
```

#### Sintaxe Delete

**DELETE FROM** *nome_tabela*;
**DELETE FROM** *nome_tabela* **where** *nome_campo* = value;

## DQL - Data Manipulation Language

Linguagem de consulta de dados. São os comandos de consulta.

```
select * from pessoa;
select * from pessoa where id = 1;
select * from pessoa where nome like('V%');
```

- **Exemplos Select - like**

- *%*: Busca qualquer coincidencia sem se importar com a quantidade de caracteres
- *_*: Busca apenas um caracter
- *Not like*: Busca qualquer que nao coincida com o nome indicado
- *Upper*: Mostra todos os dados em maiusculas

```
select * from pessoa where nome like('%Victor%');
select * from pessoa where nome like('Victor');
select * from pessoa where nome like('V_');
select * from pessoa where nome like('_r');
select * from pessoa where nome like('_r%');
select * from pessoa where nome like(upper('Victor'));
select * from pessoa where nome not like('%o'));
select upper (nome) from pessoa where nome not like('%o'));
```

- **Exemplos Select - and/or**

```
select * from pessoa where idade > 1 and idade < 40;
select * from pessoa where idade > 30 or nome like ('Victor');
```

- **Exemplo Select - order by**

```
select * from pessoa order by nome;
select * from pessoa order by nome asc;
select * from pessoa order by nome desc;
```

- **Exemplo Select - distinct**

```
select distinct(nome) from pessoa;
```

- **Exemplos Select - in**

```
select * from pessoa where nome in ('Victor', 'Rodrigo');
```

- **Exemplos Select - between**

```
select * from pessoa where idade between 1 and 40;
```
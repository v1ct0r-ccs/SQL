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
);
```

#### Sintaxe Alter Table

**ALTER TABLE** *table_name* action;

- **Alter Table** - *rename column*

Comando usado para renomear uma coluna numa tabela existente.
```
ALTER TABLE table_name
RENAME COLUMN column_name
TO new_column_name;
```

- **Alter Table** - *add column*

Comando usado para adicionar uma coluna numa tabela existente.

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

Comando usado para adicionar ou remover valores defaults numa coluna numa tabela existente.

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

Comando usado para adicionar ou remover uma constraint(*restrição*) numa coluna numa tabela existente.

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

# SQL - *Parte II*

## Index

É uma ferramenta de otimização que pode aumentar a performance de consulta nas tabelas.

```
CREATE INDEX index_name ON table_name(column_name);
```

## Constraints

Sao declarações de "restrições" ou "bloquios" e têm como fundamento a imposição de alguma regra de validação aos dados.

São separadas em: **Key** e **columns** constraints.

### Key Constraints

Definem a criação de Chaves e Relacionamentos existentes entre tabelas. São eles:

- Primary Key
- Foreign Key

#### Primary Key

Automaticamente define que os valores das colunas em questão estarão presentes num índice (**INDEXED**), ocorrendo somente uma única vez (**UNIQUE**). Esse índice deve ser preliminarmente definido como não podendo ser **NULOS**. Esta _constraint_ se adequa perfeita e absolutamente ao conceito de chave primária para uma tabela.

```
create table tb_pessoa (
    id bigint not null,
    nome varchar(50) not null,
    idade integer constraint check_idade CHECK (idade > 0 and idade < 120),
    sexo varchar(1) not null CHECK (sexo IN ('M', 'F')),
    constraint pk_id_pessoa primary key (id)
);
```

```
alter table tb_pessoa
add constraint pk_id_pessoa primary key (id);
```

#### Foreign Key

Automaticamente define que os valores das colunas em questão obrigatoriamente estarão presentes no índice da **PRIMARY KEY** da tabela a que se refere. Uma ou mais colunas que sofrem esta imposição pode admitir valores Nulos (**NULLABLE**) e quando tiverem valor, geralmente ele se repete ao longo da tabela.

```
create table tb_pessoa (
id bigint not null,
nome varchar(50) not null,
idade integer constraint check_idade CHECK (idade > 0 and idade < 120),
sexo varchar(1) not null CHECK (sexo IN ('M', 'F')),
constraint pk_id_pessoa primary key (id)
constraint fk_id_estado_pessoa foreign key (id_estado) references tb_estado(id)
);
```

```
alter table tb_pessoa
add constraint fk_id_estado_pessoa foreign key (id_estado) references tb_estado(id);
```

## Constraints(_Unique_) e Sequences

### Column constraints

Bloqueios (restrições) a valores operados numa coluna. São eles:

- **NOT NULL**: Impõe a obrigatoriedade de ocorrência de valor para a coluna;
- **DEFAULT**: Aplica uma constante quando da não ocorrência de valor para uma coluna;
- **CHECK**: Valida o valor a ser admitido por uma coluna, contra uma regra (expressão/equação);
- **Unique**: Impõe à coluna que não serão admitidos valores repedtidos nela;
    - ```
      alter table tb_pessoa add constraint uq_cpf_pessoa unique (cpf);
      ```
- **INDEX**: Impõe à coluna que os seus valores participarãoade um índice;

### Sequences

É uma sequência de valores que pode ser utilizado em colunas com autoincremento de valores.

```
CREATE SEQUENCE sq_pessoa
START 1
INCREMENT 1
OWNED BY tb_pessoa.id;

SELECT nextval ('sq_pessoa');

SELECT curval ('sq_pessoa');

insert intro tb_pessoa (id, nome, idade, sexo, cpf)
values (nextval('sq_pessoa'),'Victor', 29,'M', 1054627);
```

## DQL - Joins

Join é uma forma de consulta juntando as informações de duas ou mais tabelas num único resultado. São elas:

- Inner join
- Left join
- Right join
- Full join
- Cross join

### Inner Join

O Inner join combina os valores da tabela 1 e da tabela 2, compara a coluna em questão no sql e verifica se os valores são iguais. Caso seja igual, é feita uma junção das duas informações e os valores que não são iguais são ignorados e não são retorados na consulta.

```
select *
from tb_pessoa p, tb_estado e
where p.id_estado = e.id;

select p.id, p.nome pessoa, e.id, e.nome estado
from tb_pessoa p, tb_estado e
where p.id_estado = e.id;

select *
from tb_pessoa p
inner join tb_estado e on e.id = p.id_estado;
```

### Left Join

O Left join combina os valores da tabela 1 e tabela 2, compara a coluna em questão no sql e verifica se os valores são iguais. Caso seja é feita uma junção das duas informações e os resultados que nõa sao iguais, são retornados mesmo assim, mas com valores da correspondência da outra tabela como nulos. Esses valores retornados são da tabela da esquerda e os valores nulos ficam do lado da tabela da direita.

```
select *
from tb_pessoa p
left join tb_estado e on e.id = p.id_estado;
```

### Right Join

O Right join combina os valores da tabela 1 e da tabela 2, compara a coluna em questão no sql e verifica se os valores são iguais. Caso seja, é feita uma junção das duas informações e os resultados que não são iguais, são retornados mesmo assim, mas com os valores da correspondência da outra tabela como nulos. Esses valores são retornados são da tabela da direita e os valores nulos ficam do lado esquerdo da tabela.

```
select *
from tb_pessoa p
right join tb_estado e on e.id = p.id_estado;
```

### Full Join

O Full join é parecido com o left e right, trazendo todos os registros e os que não tiverem par, iram ficar nulos ou do lado esquerdo, ou do lado direito.

```
select *
from tb_pessoa p
full join tb_estado e on e.id = p.id_estado;
```

### Cross Join

O Cross join é um dos mais perigosos para se ultilizar, pois ele tràs todos os registros da tabela do join repetindo as informações para cada colula dos dois lados.

```
select *
from tb_pessoa
cross join tb_estado;
```
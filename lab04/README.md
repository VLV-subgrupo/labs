# Modelo Lógico Relacional - Banco de Dados Nutricional

## Tabela NUTRIENTE

```sql
CREATE TABLE NUTRIENTE (
    Nome VARCHAR(255) PRIMARY KEY,
    Tipo VARCHAR(255)
);
```
## Tabela INGREDIENTE_ELEMENTAR

```sql
CREATE TABLE INGREDIENTE_ELEMENTAR (
    Nome VARCHAR(255) PRIMARY KEY,
    CaloriaPorGrama DECIMAL(10, 2)
);
```
## Tabela INGREDIENTE

```sql
CREATE TABLE INGREDIENTE (
    Nome VARCHAR(255) PRIMARY KEY
);
```
## Tabela COMPOSICAO_INGREDIENTE

```sql
CREATE TABLE COMPOSICAO_INGREDIENTE (
    NomeIngrediente VARCHAR(255),
    NomeIngredienteElementar VARCHAR(255),
    QuantidadeIngredienteElementar DECIMAL(10, 2),
    PRIMARY KEY (NomeIngrediente,              NomeIngredienteElementar),
    FOREIGN KEY (NomeIngrediente) REFERENCES INGREDIENTE(Nome),
    FOREIGN KEY (NomeIngredienteElementar) REFERENCES INGREDIENTE_ELEMENTAR(Nome)
);
```
## Tabela PERFIL_NUTRICIONAL_INGREDIENTE

```sql
CREATE TABLE PERFIL_NUTRICIONAL_INGREDIENTE (
    NomeIngrediente VARCHAR(255),
    NomeNutriente VARCHAR(255),
    QuantidadePorGrama DECIMAL(10, 2),
    PRIMARY KEY (NomeIngrediente, NomeNutriente),
    FOREIGN KEY (NomeIngrediente) REFERENCES INGREDIENTE(Nome),
    FOREIGN KEY (NomeNutriente) REFERENCES NUTRIENTE(Nome)
);
```

## Tabela PORCAO

```sql
CREATE TABLE PORCAO (
    TipoPorcao VARCHAR(255),
    NomeIngrediente VARCHAR(255),
    QuantidadeEscolhida DECIMAL(10, 2),
    QuantidadeRejeitada DECIMAL(10, 2),
    PRIMARY KEY (TipoPorcao, NomeIngrediente),
    FOREIGN KEY (TipoPorcao) REFERENCES COMPOSICAO_CARDAPIO(TipoPorcao),
    FOREIGN KEY (NomeIngrediente) REFERENCES COMPOSICAO_CARDAPIO(NomeIngrediente)
);
```

## Tabela CARDAPIO

```sql
CREATE TABLE CARDAPIO (
    Data DATE,
    Periodo VARCHAR(255),
    EhVegano BOOLEAN,
    PRIMARY KEY (Data, Periodo, EhVegano)
);
```
## Tabela COMPOSICAO_CARDAPIO

```sql
CREATE TABLE COMPOSICAO_CARDAPIO (
    Data DATE,
    Periodo VARCHAR(255),
    EhVegano BOOLEAN,
    TipoPorcao VARCHAR(255),
    NomeIngrediente VARCHAR(255),
    PRIMARY KEY (Data, Periodo, EhVegano, TipoPorcao, NomeIngrediente),
    FOREIGN KEY (Data, Periodo, EhVegano) REFERENCES CARDAPIO(Data, Periodo, EhVegano),
    FOREIGN KEY (TipoPorcao, NomeIngrediente) REFERENCES PORCAO(TipoPorcao, NomeIngrediente)
);
```
## Tabela CATEGORIA

```sql
CREATE TABLE CATEGORIA (
    Nome VARCHAR(255) PRIMARY KEY
);
```
## Tabela TIPO_DE_INGREDIENTE

```sql
CREATE TABLE TIPO_DE_INGREDIENTE (
    NomeCategoria VARCHAR(255),
    NomeIngredienteElementar VARCHAR(255),
    PRIMARY KEY (NomeCategoria, NomeIngredienteElementar),
    FOREIGN KEY (NomeCategoria) REFERENCES CATEGORIA(Nome),
    FOREIGN KEY (NomeIngredienteElementar) REFERENCES INGREDIENTE_ELEMENTAR(Nome)
);
```
## Tabela ALUNO

```sql
CREATE TABLE ALUNO (
    Ra VARCHAR(255) PRIMARY KEY
);
```
## Tabela CONSUMO

```sql
CREATE TABLE CONSUMO (
    Data DATE,
    RaAluno VARCHAR(255),
    TipoPorcao VARCHAR(255),
    NomeIngrediente VARCHAR(255),
    PRIMARY KEY (Data, RaAluno, TipoPorcao, NomeIngrediente),
    FOREIGN KEY (RaAluno) REFERENCES ALUNO(Ra),
    FOREIGN KEY (TipoPorcao, NomeIngrediente) REFERENCES PORCAO(TipoPorcao, NomeIngrediente),
    FOREIGN KEY (Data) REFERENCES CARDAPIO(Data)
);
```
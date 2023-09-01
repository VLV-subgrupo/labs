# Apresentação do Lab03 - Modelo Lógico Relacional de Refeições em um Restaurante

# Equipe `LAMEV`

# Subgrupo `B`
* `Luiz Guilherme Sousa Nascimento` - `230667`
* `Victor Wu` - `231467`
* `Vítor Paziam Magalhães` - `238316`

## Modelo Conceitual ER Revisado

<img src="images/ER-lab03.png" width="1000px" height="auto">

*Diagrama ER Revisado*

## Mapeamento -> o Modelo Lógico Relacional

~~~
NUTRIENTE(_Nome_, Tipo)

INGREDIENTE_ELEMENTAR(_Nome_, CaloriaPorGrama)
INGREDIENTE(_Nome_)
COMPOSIÇÃO_INGREDIENTE(_NomeIngrediente_, _NomeIngredienteElementar_, _QuantidadeIngredienteElementar_)
    NomeIngrediente: chave estrangeira -> INGREDIENTE
    NomeIngredienteElementar: chave estrangeira -> INGREDIENTE_ELEMENTAR

PERFIL_NUTRICIONAL_INGREDIENTE (_NomeIngrediente_ , _NomeNutriente_, _QuantidadePorGrama_)
    NomeIngrediente: chave estrangeira -> INGREDIENTE
    NomeNutriente: chave estrangeira -> NUTRIENTE

PORÇÃO(_TipoPorção_, _NomeIngrediente_,  QuantidadeEscolhida, QuantidadeRejeitada)
    NomeIngrediente: chave estrangeira -> INGREDIENTE

CARDÁPIO(_Data_, _Período_, _EhVegano_)
COMPOSIÇÃO_CARDÁPIO(_Data_, _Período_, _EhVegano_, _TipoPorcao_, _NomeIngrediente_)
    Data: chave estrangeira -> CARDÁPIO
    Período: chave estrangeira -> CARDÁPIO
    EhVegano: chave estrangeira -> CARDÁPIO
    TipoPorcao: chave estrangeira -> PORÇÃO
    NomeINgrediente: chave estrangeira -> PORÇÃO

CATEGORIA(_Nome_)
TIPO_DE_INGREDIENTE(_NomeCategoria_, _NomeIngredienteElementar_)
    NomeCategoria: chave estrangeira -> CATEGORIA
    NomeIngredienteElementar: chave estrangeira -> INGREDIENTE_ELEMENTAR

ALUNO(_Ra_)

CONSUMO(_Data_, _RaAluno_, _TipoPorcao_, _NomeIngrediente_, _Data_, _Período_, _EhVegano_)
    RaAluno: chave estrangeira -> ALUNO
    TipoPorção: chave estrangeira -> PORÇÃO
    NomeIngrediente: chave estrangeira -> PORÇÃO
    Data: chave estrangeira -> CARDÁPIO
    Período: chave estrangeira -> CARDÁPIO
    EhVegano: chave estrangeira -> CARDÁPIO
~~~
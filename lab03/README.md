# Modelo para Apresentação do Lab03 - Modelagem Conceitual de Refeições em um Restaurante

# Equipe `<nome da equipe>`

# Subgrupo `<letra do subgrupo>`
* `<nome completo>` - `<RA>`
* `<nome completo>` - `<RA>`
* `<nome completo>` - `<RA>`

## Modelo Conceitual ER Revisado

<img src="images/ER-lab03.png" width="400px" height="auto">

*Diagrama ER Revisado*

## Mapeamento para o Modelo Relacional

~~~
PESSOA(_Código_, Nome, Telefone)
ARMÁRIO(_Código_, Tamanho, Ocupante)
  Ocupante chave estrangeira -> PESSOA(Código)
~~~
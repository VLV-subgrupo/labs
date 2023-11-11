## Exercício

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
~~~cypher
MATCH (p1:Pathology)<-[]-(d:Drug)-[]->(p2:Pathology)
MERGE (p1)<-[r:Relates]->(p2)
ON CREATE SET r.weight=1
ON MATCH SET r.weight=r.weight+1
~~~
~~~cypher
MATCH (p1:Pathology)<-[:Relates]->(p2:Pathology)
RETURN p1, p2
LIMIT 20
~~~

# Trabalhando com Efeitos Colaterais

Considere o seguinte arquivo que indica um conjunto de pessoas (identificadas por código) e as drogas que elas usam:

[https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv]

Considere este outro arquivo que indica as mesmas pessoas e efeitos colaterais que elas experimentaram:

[https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv]

## Exercício

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
~~~cypher
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' AS drug_use
MERGE (p1:Person {code: drug_use.idperson})
MERGE (d1:Drug {code: drug_use.codedrug})
MERGE (p1)-[u:Utilizes {pathologyCode: drug_use.codepathology}]->(d1)

~~~
~~~cypher
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' AS side_effect
MERGE (p2:Person {code: side_effect.idPerson})
MERGE (q2:Pathology {code: side_effect.codePathology})
MERGE (p2)-[g:Gets]->(q2)

~~~
~~~cypher
MATCH (q:Pathology)<-[:Gets]-(:Person)-[:Utilizes]->(d:Drug)
MERGE (d)-[c:Causes]->(q)
ON CREATE SET c.weight=1
ON MATCH SET c.weight=c.weight+1
~~~

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução
A _query_ escolhida identifica as 10 drogas da base de dados com o maior número de efeitos colaterais. Tal informação pode contribuir na confiabilidade e eficácia de novos tratamentos médicos. Sendo assim, um conhecimento relevante para profissionais de saúde, ao permitir decisões mais seguras na prescrição de medicamentos e facilitando o monitoramento de reações adversas.

**Obs:** É necessário executar as celulas anteriores primeiro.
~~~cypher
MATCH (d:Drug)-[c:Causes]->(p:Pathology)
WITH d, COUNT(p) AS numSideEffects
RETURN d, numSideEffects
ORDER BY numSideEffects DESC
LIMIT 10;
~~~
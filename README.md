# DIO - Trilha .NET - Banco de Dados
www.dio.me

## Desafio Concluído
Realizei o desafio proposto durante o módulo de banco de dados da trilha .NET da DIO.

## Contexto
Fui responsável pelo banco de dados de um site de filmes, onde armazenei dados sobre os filmes e seus atores. A consulta no banco de dados foi realizada para trazer informações específicas para análise.

## Proposta
Foram realizadas 12 consultas ao banco de dados, cada uma retornando um tipo de informação. O banco de dados utilizado possui a seguinte modelagem:

![Diagrama banco de dados](Imagens/diagrama.png)

As tabelas são descritas da seguinte forma:

**Filmes**

Tabela responsável por armazenar informações dos filmes.

**Atores**

Tabela responsável por armazenar informações dos atores.

**Generos**

Tabela responsável por armazenar os gêneros dos filmes.

**ElencoFilme**

Tabela responsável por representar um relacionamento do tipo muitos para muitos entre filmes e atores, ou seja, um ator pode trabalhar em muitos filmes, e filmes podem ter muitos atores.

**FilmesGenero**

Tabela responsável por representar um relacionamento do tipo muitos para muitos entre filmes e gêneros, ou seja, um filme pode ter mais de um gênero, e um gênero pode fazer parte de muitos filmes.

## Banco de Dados Pronto
Executei o arquivo **Script Filmes.sql** em meu banco de dados SQL Server, presente na pasta Scripts deste repositório ([clique aqui para acessar](Script%20Filmes.sql)). Esse script criou um banco chamado **Filmes**, contendo as tabelas e os dados necessários para o desafio.

## Resultado
Criei diversas consultas para retornar os dados solicitados. Abaixo estão os pedidos e o retorno esperado, sendo que meu resultado foi igual ao apresentado na imagem do desafio.


## 1 - Buscar o nome e ano dos filmes

![Exercicio 1](Imagens/1.png)

---
## Resposta

```sql
SELECT 
	Nome,
	Ano
FROM Filmes
```

---
## 2 - Buscar o nome e ano dos filmes, ordenados por ordem crescente pelo ano

![Exercicio 2](Imagens/2.png)

---
## Resposta

```sql
SELECT 
    Nome,
    Ano,
	Duracao
FROM Filmes
ORDER BY Ano ASC;
```

---

## 3 - Buscar pelo filme de volta para o futuro, trazendo o nome, ano e a duração

![Exercicio 3](Imagens/3.png)

---
## Resposta

```sql
SELECT 
    Nome,
    Ano,
    Duracao
FROM Filmes
WHERE Nome = 'De Volta para o Futuro';
```

---

## 4 - Buscar os filmes lançados em 1997

![Exercicio 4](Imagens/4.png)

---
## Resposta

```sql
SELECT 
    Nome,
    Ano,
    Duracao
FROM Filmes
WHERE Ano = '1997';
```

---

## 5 - Buscar os filmes lançados APÓS o ano 2000

![Exercicio 5](Imagens/5.png)

---
## Resposta

```sql
SELECT 
    Nome,
    Ano,
    Duracao
FROM Filmes
WHERE Ano > '2000';
```

---

## 6 - Buscar os filmes com a duracao maior que 100 e menor que 150, ordenando pela duracao em ordem crescente

![Exercicio 6](Imagens/6.png)

---
## Resposta

```sql
SELECT 
    Nome,
    Ano,
    Duracao
FROM Filmes
WHERE Duracao > 100 AND Duracao < 150
ORDER BY Duracao ASC;
```

---

## 7 - Buscar a quantidade de filmes lançadas no ano, agrupando por ano, ordenando pela duracao em ordem decrescente

![Exercicio 7](Imagens/7.png)

---
## Resposta

```sql
SELECT 
    Ano,
    COUNT(*) as QuantidadeFilmes,
    MAX(Duracao) as DuracaoMaxima
FROM Filmes
GROUP BY Ano
ORDER BY DuracaoMaxima DESC;
```

---


## 8 - Buscar os Atores do gênero masculino, retornando o PrimeiroNome, UltimoNome

![Exercicio 8](Imagens/8.png)

---
## Resposta

```sql
SELECT 
	Id,
    PrimeiroNome,
    UltimoNome,
	Genero
FROM Atores
WHERE Genero = 'M';
```

---

## 9 - Buscar os Atores do gênero feminino, retornando o PrimeiroNome, UltimoNome, e ordenando pelo PrimeiroNome

![Exercicio 9](Imagens/9.png)

---
## Resposta

```sql
SELECT 
	Id,
    PrimeiroNome,
    UltimoNome,
	Genero
FROM Atores
WHERE Genero = 'F'
ORDER BY PrimeiroNome ASC;
```

---

## 10 - Buscar o nome do filme e o gênero

![Exercicio 10](Imagens/10.png)

---
## Resposta

```sql
SELECT
    F.Nome AS NomeFilme,
    G.Genero
FROM
    Filmes F
JOIN
    FilmesGenero FG ON F.Id = FG.IdFilme
JOIN
    Generos G ON FG.IdGenero = G.Id;
```

---

## 11 - Buscar o nome do filme e o gênero do tipo "Mistério"

![Exercicio 11](Imagens/11.png)

---
## Resposta

```sql
SELECT 
    F.Nome AS NomeFilme,
    G.Genero
FROM Filmes AS F
JOIN FilmesGenero AS FG ON F.Id = FG.IdFilme
JOIN Generos AS G ON FG.IdGenero = G.Id
WHERE G.Genero = 'Mistério';
```

---

## 12 - Buscar o nome do filme e os atores, trazendo o PrimeiroNome, UltimoNome e seu Papel

![Exercicio 12](Imagens/12.png)

---
## Resposta

```sql
SELECT
    F.Nome AS NomeFilme,
    A.PrimeiroNome,
    A.UltimoNome,
    EF.Papel
FROM
    Filmes F
JOIN
    ElencoFilme EF ON F.Id = EF.IdFilme
JOIN
    Atores A ON EF.IdAtor = A.Id;
```

---


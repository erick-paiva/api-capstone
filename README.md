 
<img src="https://kenzie.com.br/images/logoblue.svg" width="200px" />

# Entrega CAPSTONE

## Introdução

A api tem um total de **“12”** Endpoints, criada para plataforma onde os usuários que desejam podem cadastrar suas dúvidas e ao mesmo tempo poder acessar as duvidas já solucionadas por outros usuários, além de também poder comentar qualquer duvida postadas por outros usuários e respostas de usuários qualificados a responderem. 

**O url base da API:**

 [https://api-stack-kenzie.herokuapp.com](https://api-stack-kenzie.herokuapp.com)

**Os endpoints estão mockados com dados fictícios:**

[Dados mockados](https://www.notion.so/Dados-mockados-8321fb1819cd45c8ba98611191a22790)

## **Endpoints**

- Registrar ⇒ “/register”
- Login ⇒ “/login”
- Questões ⇒ “/questions”
- Respostas ⇒ “/answers”
- Comentários ⇒ “/comments”

## EndPoint ⇒ Registrar um usuário

`POST /register - FORMATO DA REQUISIÇÃO`

Endpoint para cadastrar usuários na api, sendo coach ou aluno.

```
{
  "email": "johndoe@email.com",
  "password": "123456",
  "name": "John Doe",
  "bio": "aprendendo React",
  "module": "q2",
  "coach": false
}

```

Caso dê tudo certo, a resposta será assim:

```
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6IjEyM3NrYXRlc2s4QG1haWwuY29tIiwiaWF0IjoxNjQyMDk0NjQ4LCJleHAiOjE2NDIwOTgyNDgsInN1YiI6IjIifQ.ruCsRqvBHQpxdOYBTA592GI99LykAKXX_895sZq9Boc",
  "user": {
    "email": "johndoe@email.com",
    "password": "123456",
    "name": "John Doe",
    "bio": "aprendendo React",
    "module": "q2",
    "coach": false
  }
}

```

## Possíveis erros

`POST /register FORMATO DA RESPOSTA - STATUS 400`

Caso você esqueça de colocar o email ou senha a reposta do erro será assim: No exemplo a requisição foi feita faltando o email.

`"Email and password are required"`

Email ja cadastrado:

```
{
  "status": "error",
  "message": "Email already exists"
}

```

## EndPoint Login

`POST /login - FORMATO DA REQUISIÇÃO`

EndPoint para logar no site. Login feito com usuário comun.

```
{
  "email": "johndoe@email.com",
  "password": "123456"
}

```

Caso dê tudo certo, a resposta será assim:

```
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6IjEyM3NrYXRlc2s4QG1haWwuY29tIiwiaWF0IjoxNjQyMDk3NTA5LCJleHAiOjE2NDIxMDExMDksInN1YiI6IjIifQ.O7t0sbgb8PvDjtDTrYIqHE-qE-jjvYsKsQ7gbcTNGwU",
  "user": {
    "email": "johndoe@email.com",
    "password": "123456",
    "name": "John Doe",
    "bio": "aprendendo React",
    "module": "q2",
    "coach": false
  }
}

```

Nessa requisição são disponibilizados o usuário e o token respectivo. 

**Dica:** *dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.*

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição (o campo "Authorization"), dessa forma:

> Authorization: Bearer {token}
> 

Após o usuário estar logado, conseguirá postar duvidas, comentar em duvidas de outros usuários, dar like em qualquer duvida resolvida e em qualquer comentário.

## EndPoint questions

`POST /questions - FORMATO DA REQUISIÇÃO`

Endpoint para postar suas duvidas. Você devera informar os respectivos itens a sua questão:

1 - o "**userId**" do criador da questão, 

2 - um objeto chamado "**date**" que terá as propriedades: day, month, year, hour e minutes 

3 - um objeto chamado “**question**” que terá as propriedades: title, body e likes.

Caso dê tudo certo, a resposta será assim:

```
{
  "userId": 1,
  "date": {
    "day": 25,
    "month": 1,
    "year": 2022,
    "hour": 8,
    "minutes": 21
  },
  "question": {
    "title": "duvida em redux",
    "body": "tentei fazer um loop for",
    "likes": 0
  },
  "id": 4
}
```

## Deletando questōes

`DELETE /questions/:these_id - FORMATO DA REQUISIÇÃO`

Também é possível deletar uma questão, basta passar como query o id da questão.

Lembrando que apenas o dono poderá deletar uma questão.

```
Não é necessário um corpo da requisição.
```

## EndPoint comentarios.

`POST /comments - FORMATO DA REQUISIÇÃO`

Endpoint para criar comentários.  

```
{
  "userId": 1,
  "postId": 4,
  "date": {
    "day": 25,
    "month": 1,
    "year": 2022,
    "hour": 8,
    "minutes": 21
  },
  "comment": "eu tambem testei outra coisa que deu certo"
}

```

Você devera informar os respectivos itens ao seu comentario:

1 - o “**userId**” do criador do comentário 

2 - o “**postId**” da questão a ser comentada. 

3 - um objeto chamado "**date**" que terá as propriedades: day, month, year, hour e minutes 

4 - o “**comment**” em si.

Caso dê tudo certo, a resposta será assim:

```
{
  "userId": 1,
  "postId": 4,
  "date": {
    "day": 25,
    "month": 1,
    "year": 2022,
    "hour": 8,
    "minutes": 21
  },
  "comment": "eu tambem testei outra coisa que deu certo",
	"id": 1
}

```

## Deletando comentario.

`DELETE /comments/:comment_id - FORMATO DA REQUISIÇÃO`

Também é possível deletar um comentário, basta passar como query o id do comentário.

Lembrando que apenas o dono poderá deletar o comentário.

```
Não é necessário um corpo da requisição.

```

## EndPoint respostas

`POST /answers - FORMATO DA REQUISIÇÃO`

Este endpoint servira para postar respostas das questões.

```
{
	"userId": 1,
	"postId": 6,
	"date": {"day": 25, "month": 1, "year": 2022, "hour": 8, "minutes": 21},
	"title": "voce esta esquecendo de fechar o loop for",
	"body": "quando o loop for ...",
	"likes": 0
}
```

Você devera informar os respectivos itens a resposta do coach:

1 - o "**userId**" do coach que respondeu 

2 - o "**postId**" da questão 

3 - um objeto chamado "**date**" que terá as propriedades: day, month, year, hour e minutes 

4 - o "**title**" da resposta 5 - o "**body**" da resposta 6 - a quantidade de **likes** que o coach tem

Caso dê tudo certo, a resposta será assim:

```
{
  "userId": 1,
  "postId": 6,
  "date": {
    "day": 25,
    "month": 1,
    "year": 2022,
    "hour": 8,
    "minutes": 21
  },
  "title": "voce esta esquecendo de fechar o loop for",
  "body": "quando o loop for ...",
  "likes": 0,
  "id": 2
}
```

## Deletando um resposta

`DELETE /answers/:answer_id - FORMATO DA REQUISIÇÃO`

Também é possível deletar uma resposta, basta passar como query o id da resposta.

Lembrando que apenas o dono poderá deletar a resposta.

```
Não é necessário um corpo da requisição.

```

## Rotas que não necessitam de autorização

## Obtendo todas questões

`GET /questions - FORMATO DA RESPOSTA - STATUS 200`

```
[
  {
    "userId": 1,
    "date": {
      "day": 25,
      "month": 1,
      "year": 2022,
      "hour": 8,
      "minutes": 21
    },
    "postId": 6,
    "question": {
      "title": "duvida em python",
      "question": "tentei fazer um loop for",
      "likes": 0
    },
    "id": 3
  }
]

```

## Obtendo todos os comentários:

`GET /comments - FORMATO DA RESPOSTA - STATUS 200`

```
[
  {
    "userId": 1,
    "postId": 4,
    "date": {
      "day": 25,
      "month": 1,
      "year": 2022,
      "hour": 8,
      "minutes": 21
    },
    "comment": "eu tambem testei meu redux e deu ruin",
    "id": 7
  }
]

```

by Erick Paiva 🕵🏽‍♀️

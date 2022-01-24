<h1 align="center">
  <img alt="KenzieHub" title="KenzieHub" src="https://kenzie.com.br/images/logoblue.svg" width="100px" />
</h1>

<h1 align="center">
  Entrega Kenzie Hub JSON Server
</h1>

## **Endpoints**
A api tem um total de 7 endPoints, sendo voltada aos usuarios que desejam cadastrar as linguagens de programaçao que dominam atualmente e poder compartilhar quais cursos estao fazendo no momento com os outros usuarios.

O JSON para utilizar no Insomnia é este aqui -> 

<h2 align ='center'> Registrar um usuário </h2>

`POST /register -  FORMATO DA REQUISIÇÃO`

```json
{
	"email": "johndoe@email.com",
	"password":"123456",
	"name": "John Doe",
	"age": 18
}

```
Caso dê tudo certo, a resposta será assim:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6IjEyM3NrYXRlc2s4QG1haWwuY29tIiwiaWF0IjoxNjQyMDk0NjQ4LCJleHAiOjE2NDIwOTgyNDgsInN1YiI6IjIifQ.ruCsRqvBHQpxdOYBTA592GI99LykAKXX_895sZq9Boc",
  "user": {
    "email": "johndoe@email.com",
    "name": "John Doe",
    "age": 18,
    "id": 1
  }
}

```
<h2 align ='center'> Possíveis erros </h2>

Caso você esqueça de colocar o email ou senha a reposta do erro será assim:
No exemplo a requisição foi feita faltando o email.


`"Email and password are required"`

Email ja cadastrado:

`POST /register FORMATO DA RESPOSTA - STATUS 400`

```json
{
  "status": "error",
  "message": "Email already exists"
}
```

<h2 align ='center'> Fazer o Login </h2>


`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
    "email": "johndoe@email.com",
    "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6IjEyM3NrYXRlc2s4QG1haWwuY29tIiwiaWF0IjoxNjQyMDk3NTA5LCJleHAiOjE2NDIxMDExMDksInN1YiI6IjIifQ.O7t0sbgb8PvDjtDTrYIqHE-qE-jjvYsKsQ7gbcTNGwU",
  "user": {
    "email": "johndoe@email.com",
    "name": "John Doe",
    "age": 18,
    "id": 1
  }
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir informar as tecnologias que ele aprendeu até agora.

<h2 align ='center'> Informa qual curso esta fazendo no momento </h2>

`POST /courses - FORMATO DA REQUISIÇÃO`
```json
[
  {
    "nameOfCourse": "Kenzie Academy",
    "duration": "12 months",
    "userId": 2
  }
]
```
Você devera informar os respectivos itens ao seu curso
    1. O nome do curso
    2. a duraçao do curso
    3. o id do usuario

Caso dê tudo certo, a resposta será assim:

```json
{
  "nameOfCourse": "Kenzie Academy",
  "duration": "12 months",
  "userId": 2,
  "id": 1
}
```
<h2 align ='center'> Informar quais Liguagens de programação você domina atualmente </h2>

`POST /programmingLanguages - FORMATO DA REQUISIÇÃO`
```json
{
	"languageName": "python",
	"nivel": "junior"
}
```

Você devera informar os respectivos itens a liguagem de Programação
    1. O nome da linguagem
    2. O seu nivel de senioridade nessa liguagem

Caso dê tudo certo, a resposta será assim:

```json
{
  "languageName": "python",
  "nivel": "junior",
  "id": 4
}
```

Obtendo as liguagens de programação que você cadastrou

`GET /programmingLanguages - FORMATO DA REQUISIÇÃO`

Caso dê tudo certo, a resposta será assim:

```json[
{
    "languageName": "python",
    "nivel": "junior",
    "id": 1
}
]
```

Também é possível deletar uma linguagem da sua lista

`DELETE /programmingLanguages/:language_id - FORMATO DA REQUISIÇÃO`

```
Não é necessário um corpo da requisição.
```

## Rotas que não necessitam de autorização

<h2 align ='center'> Obtendo os cursos de outras pessoas </h2>

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os devs já cadastrados na plataforma, na API podemos acessar a lista dessa forma:

`GET /courses -  FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "nameOfCourse": "Kenzie Academy",
    "duration": "12 months",
    "userId": 2,
    "id": 1
  }
]
```


by Erick Paiva :chrome_dynosaur:
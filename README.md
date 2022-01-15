<h1 align="center"><strong>To Do List - API</strong></h1>

Está é uma fake API criada utilizando as bibliotecas json-server e json-server-auth, para que usuários possam se cadastrar e fazer login, cadastrar novas tarefas, atualizá-las e deletá-las.

<br/>
<br/>

<h2 align="center"><strong>Endpoints</strong></h2>

Esta API possui um total de 7 endpoints destinados a cadastro e login de usuários, criar, editar e deletar tarefas, além de podem listar tanto todas as tarefas como tarefas de um usuário específico.

<br/>
<br/>

<h2 align="center">Endpoints que não necessitam de autenticação</h2>

## _Criação de usuário_

-> POST /register - Formato da requisição:

```json
{
  "email": "rafael@mail.com",
  "password": "123456",
  "name": "Rafael",
  "age": 34
}
```

-> Status code 201 - Formato da resposta:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRoYXRpQG1haWwuY29tIiwiaWF0IjoxNjQyMjgyNjgxLCJleHAiOjE2NDIyODYyODEsInN1YiI6IjMifQ.Zv81yyypXVCArmT7-UEN-lX-yOPtRH0vFHMuh55BqTU",
  "user": {
    "email": "thati@mail.com",
    "name": "Thatiane",
    "age": 34,
    "id": 3
  }
}
```

-> Possíveis erros

- "Email already exists" -> Email já cadastrado;
- "Email and password are required" -> Caso o campo de email ou senha não esteja presente no campo da requisição.

<br/>
<br/>

## _Login_

-> POST /login - Formato da requisição:

```json
{
  "email": "rafael@mail.com",
  "password": "123456"
}
```

-> Status code 200 - Formato da resposta:

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InJhZmFlbEBtYWlsLmNvbSIsImlhdCI6MTY0MjI4Mjc2MywiZXhwIjoxNjQyMjg2MzYzLCJzdWIiOiIyIn0.riiZMj6D1eQiXFCZ3buczTebwH5-DaLHlpb6MTCRe9g",
  "user": {
    "email": "rafael@mail.com",
    "name": "Rafael",
    "age": 34,
    "id": 2
  }
}
```

-> Possíveis erros

- "Cannot find user" -> Email não cadastrado ou digitado incorretamente;
- "Incorrect password" -> Senha digitada incorretamente.

<br/>
<br/>

<h2 align="center">Endpoints que necessitam de autenticação</h2>

<br/>
<br/>

## _Criação de nova tarefa_

-> POST /users/:userId/tasks - Formato da requisição:

```json
{
  "title": "Beber Vinho",
  "description": "Beber 1 cálice de vinho",
  "frequency": "Diariamente"
}
```

-> Status code 201 - Formato da resposta:

```json
{
  "title": "Beber Água",
  "description": "Beber 2 litros de água",
  "frequency": "Diariamente",
  "userId": "2",
  "id": 4
}
```

<br/>
<br/>

## _Atualização de tarefa_

-> PUT ou PATCH /users/:userId/tasks - Formato da requisição:

```json
{
  "title": "Beber Vinho",
  "description": "Beber 1 cálice de vinho",
  "frequency": "Diariamente"
}
// Utilizar somente os campos que sofrerão alteração
```

-> Status code 200 - Formato da resposta:

```json
{
  "title": "Beber Água",
  "description": "Beber 2 litros de água",
  "frequency": "Diariamente",
  "userId": "2",
  "id": 4
}
```

<br/>
<br/>

## _Deletar tarefa_

-> DELETE /tasks/:taskId - Formato da requisição:

```json
{
  "userId": 2
}
```

-> Status code 200 - Formato da resposta: Sem corpo

<br/>
<br/>

## _Listar tarefas do usuário logado_

-> GET /users/:userId/tasks - Formato da requisição: sem corpo

-> Status code 200 - Formato da resposta:

```json
[
  {
    "title": "Beber Água",
    "description": "Beber 2 litros de água",
    "frequency": "Diariamente",
    "userId": "2",
    "id": 3
  },
  {
    "title": "Fazer caminhadas",
    "description": "Caminhar 5 quilômetros",
    "frequency": "Diariamente",
    "userId": "2",
    "id": 4
  }
]
```

<br/>
<br/>

## _Listar tarefas do todos os usuários cadastrados_

-> GET /tasks - Formato da requisição: sem corpo

-> Status code 200 - Formato da resposta:

```json
[
  {
    "title": "Beber Água",
    "description": "Beber 2 litros de água",
    "frequency": "Diariamente",
    "userId": "1",
    "id": 1
  },
  {
    "title": "Beber Café",
    "description": "Beber 1 caneca de café",
    "frequency": "Diariamente",
    "userId": "1",
    "id": 2
  },
  {
    "title": "Beber Água",
    "description": "Beber 2 litros de água",
    "frequency": "Diariamente",
    "userId": "2",
    "id": 3
  },
  {
    "title": "Fazer caminhadas",
    "description": "Caminhar 5 quilômetros",
    "frequency": "Diariamente",
    "userId": "2",
    "id": 4
  }
]
```

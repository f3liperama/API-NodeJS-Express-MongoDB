# API-NodeJS-Express-MongoDB

## Descrição

API para gerenciamento de projetos e tarefas realizadas por cada usuário.

## Principais recursos

*  Cadastro de usuário
*  Autenticação de usuário com JWT (JSON Web Token)
*  Recuperação de senha com NodeMailer
*  CRUD e relacionamentos com MongoDB

## Endpoints

### Autenticação

**Rota para registrar um novo usuário.**

    POST {{ base_url  }}/auth/register

JSON

``` json
{
	"name": "Nome",
	"email": "example@email.com",
	"password": "123456"
}
```

RESPOSTA

``` json
{
  "user": {
    "_id": "5d938d0ff0975544808dfcf2",
    "name": "Nome",
    "email": "example@email.com",
    "createdAt": "2019-10-01T17:29:51.418Z",
    "__v": 0
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVkOTM4ZDBmZjA5NzU1NDQ4MDhkZmNmMiIsImlhdCI6MTU2OTk1MDk5MSwiZXhwIjoxNTcwMDM3MzkxfQ.NoPA9ntqdvcnaUTJqkc1M_qGzQ4qzchaSB-NubVkmww"
}
```

**Rota para autenticar um usuário.**

    POST {{ base_url  }}/auth/authenticate

JSON

``` json
{
	"email": "example@email.com",
	"password": "123456"
}
```

RESPOSTA

``` json
{
  "user": {
    "_id": "5d938778a604a342f45981e5",
    "name": "Nome",
    "email": "example@email.com",
    "createdAt": "2019-10-01T17:06:00.598Z",
    "__v": 0
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjVkOTM4Nzc4YTYwNGEzNDJmNDU5ODFlNSIsImlhdCI6MTU2OTk1NzY1OSwiZXhwIjoxNTcwMDQ0MDU5fQ.0-fooqhJ_nurRBXsjsTzBPNCjSqbEVhCnsIhbjnDeBc"
}
```

**Rota para solicitar alteração de senha.**

    POST {{ base_url  }}/auth/forgot_password

JSON

``` json
{
	"email": "example@email.com"
}
```

RESPOSTA VIA E-MAIL

``` html
<p>Você esqueceu sua senha? Não tem problema, utilize esse token: {{ token }}</p>
```

**Rota para alterar senha.**

    POST {{ base_url  }}/auth/reset_password

JSON

``` json
{
	"email": "example@email.com",
	"token": "5086d1cfba74a7f84023c5d0ac45ae541aab7cdc",
	"password": "12345678"
}
```

### Projetos

**Rota para listar todos os projetos.**

    GET {{ base_url  }}/projects

RESPOSTA

``` json
{
  "projects": [
    {
      "tasks": [
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44126",
          "title": "Task 1",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.993Z",
          "__v": 0
        },
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44127",
          "title": "Task 2",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.995Z",
          "__v": 0
        }
      ],
      "_id": "5d93b8fa12c27e2ab0e44125",
      "title": "Title",
      "description": "Description",
      "user": {
        "_id": "5d938778a604a342f45981e5",
        "name": "Nome",
        "email": "example@email.com",
        "createdAt": "2019-10-01T17:06:00.598Z",
        "__v": 0
      },
      "createdAt": "2019-10-01T20:37:14.838Z",
      "__v": 1
    }
  ]
}
```

**Rota para listar um único projeto.**

    GET {{ base_url  }}/projects/{{ projectId }}

RESPOSTA

``` json
{
  "project": [
    {
      "tasks": [
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44126",
          "title": "Task 1",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.993Z",
          "__v": 0
        },
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44127",
          "title": "Task 2",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.995Z",
          "__v": 0
        }
      ],
      "_id": "5d93b8fa12c27e2ab0e44125",
      "title": "Title",
      "description": "Description",
      "user": {
        "_id": "5d938778a604a342f45981e5",
        "name": "Nome",
        "email": "example@email.com",
        "createdAt": "2019-10-01T17:06:00.598Z",
        "__v": 0
      },
      "createdAt": "2019-10-01T20:37:14.838Z",
      "__v": 1
    }
  ]
}
```

**Rota para criar um novo projeto.**

    POST {{ base_url  }}/projects

JSON

``` json
{
	"title": "New project",
	"description": "New description",
	"tasks": [
		{
			"title": "New task 1",
			"assignedTo": "5d938778a604a342f45981e5"
		},
		{
			"title": "New task 2",
			"assignedTo": "5d938778a604a342f45981e5"
		}
	]
}
```

RESPOSTA

``` json
{
  "project": [
    {
      "tasks": [
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44126",
          "title": "New task 1",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.993Z",
          "__v": 0
        },
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44127",
          "title": "New task 2",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.995Z",
          "__v": 0
        }
      ],
      "_id": "5d93b8fa12c27e2ab0e44125",
      "title": "New project",
      "description": "New description",
      "user": {
        "_id": "5d938778a604a342f45981e5",
        "name": "Nome",
        "email": "example@email.com",
        "createdAt": "2019-10-01T17:06:00.598Z",
        "__v": 0
      },
      "createdAt": "2019-10-01T20:37:14.838Z",
      "__v": 1
    }
  ]
}
```

**Rota para alterar um projeto específico.**

    PUT {{ base_url  }}/projects/{{ projectId }}

JSON

``` json
{
	"title": "New project (Updated)",
	"description": "New description (Updated)",
	"tasks": [
		{
			"title": "New task 1 (Updated)",
			"assignedTo": "5d938778a604a342f45981e5"
		},
		{
			"title": "New task 2 (Updated)",
			"assignedTo": "5d938778a604a342f45981e5"
		}
	]
}
```

RESPOSTA

``` json
{
  "project": [
    {
      "tasks": [
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44126",
          "title": "New task 1 (Updated)",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.993Z",
          "__v": 0
        },
        {
          "completed": false,
          "_id": "5d93b8fd12c27e2ab0e44127",
          "title": "New task 2 (Updated)",
          "assignedTo": "5d938778a604a342f45981e5",
          "project": "5d93b8fa12c27e2ab0e44125",
          "createdAt": "2019-10-01T20:37:17.995Z",
          "__v": 0
        }
      ],
      "_id": "5d93b8fa12c27e2ab0e44125",
      "title": "New project (Updated)",
      "description": "New description (Updated)",
      "user": {
        "_id": "5d938778a604a342f45981e5",
        "name": "Nome",
        "email": "example@email.com",
        "createdAt": "2019-10-01T17:06:00.598Z",
        "__v": 0
      },
      "createdAt": "2019-10-01T20:37:14.838Z",
      "__v": 1
    }
  ]
}
```

**Rota para deletar um projeto específico.**

    DELETE {{ base_url  }}/projects/{{ projectId }}


# API-NodeJS-Express-MongoDB

## Principais recursos
-  Cadastro de usuário
-  Autenticação de usuário com JWT (JSON Web Token)
-  Recuperação de senha com NodeMailer
-  CRUD e relacionamentos com MongoDB

## Endpoints

### Autenticação

**Rota para registrar um novo usuário.**

    POST {{ base_url  }}/auth/register

JSON
```json
{
	"name": "Nome",
	"email": "example@email.com",
	"password": "123456"
}
```

RESPOSTA
```json
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
```json
{
	"email": "example@email.com",
	"password": "123456"
}
```

RESPOSTA
```json
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
```json
{
	"email": "example@email.com"
}
```

RESPOSTA VIA E-MAIL
```html
<p>Você esqueceu sua senha? Não tem problema, utilize esse token: {{ token }}</p>
```

**Rota para alterar senha.**

    POST {{ base_url  }}/auth/reset_password

JSON
```json
{
	"email": "example@email.com",
	"token": "5086d1cfba74a7f84023c5d0ac45ae541aab7cdc",
	"password": "12345678"
}
```

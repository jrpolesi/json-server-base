# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

# Endpoints sem autenticação

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

## Cadastro

| Método | Endpoint  |
| ------ | --------- |
| `POST` | /register |
| `POST` | /signup   |
| `POST` | /users    |

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

#### `Formato da requisição`

```json
{
  "email": "teste@email.com",
  "password": "12345678"
}
```

#### `Formato da resposta - status 201`
<strong>O token tem validade de 1 hora</strong>

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQGVtYWlsLmNvbSIsImlhdCI6MTY0NjYyNDcwOCwiZXhwIjoxNjQ2NjI4MzA4LCJzdWIiOiIyIn0.GEM2hrOWkniuRoo3WRzPiQrfJt77Ur1tLzbe4mL7b5Y",
  "user": {
    "email": "teste@email.com",
    "id": 2
  }
}
```

## Login

| Método | Endpoint |
| ------ | -------- |
| `POST` | /login   |
| `POST` | /signin  |

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

#### `Formato da requisição`

```json
{
  "email": "teste@email.com",
  "password": "12345678"
}
```

#### `Formato da resposta - status 200`
<strong>O token tem validade de 1 hora</strong>

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQGVtYWlsLmNvbSIsImlhdCI6MTY0NjYyNDkxMiwiZXhwIjoxNjQ2NjI4NTEyLCJzdWIiOiIyIn0.YpavmpzoLkH8tbz8G13QYHmBuyjO8L3cI-DaqHrXUxs",
	"user": {
		"email": "teste@email.com",
		"id": 2
	}
}
```
<br>
<br>

# Endpoints com autenticação
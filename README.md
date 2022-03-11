# Pet-shop API
**BASE URL:** `https://first-json-serve-fake-api.herokuapp.com/` 

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

## Produtos

Utilize essa rota para receber os produtos disponíveis.

| Método | Endpoint  |
| ------ | --------- |
| `GET`  | /products |

#### `Formato da resposta - status 200`

```json
[
  {
    "description": "Ração para gato 1kg",
    "price": 19.9
  },
  {
    "description": "Ração para cachorro 1kg",
    "price": 16.95
  },
  {
    "description": "Frango de borracha",
    "price": 9.98
  }
]
```

<br>

# Endpoints com autenticação

Para utilizar as rotas abaixo é necessário enviar o token nas requisições.

Utilize o padrão **Bearer Authorization** para enviar o token.

## Cadastro de pets

Para cadastrar o pet de um usuário utilize a rota abaixo.

| Método | Endpoint |
| ------ | -------- |
| `POST` | /pets    |

#### `Formato da requisição`

```json
{
  "userId": 2,
  "animal": "cat",
  "name": "Gatinho",
  "age": 3
}
```

#### `Formato da resposta - status 201`

```json
{
  "userId": 2,
  "animal": "cat",
  "name": "Gatinho",
  "age": 3,
  "id": 2
}
```

## Pets

Utilize essa rota para listar todos os pets.

| Método | Endpoint |
| ------ | -------- |
| `GET`  | /pets    |

#### `Formato da resposta - status 200`

```json
[
  {
    "userId": 2,
    "animal": "cat",
    "name": "Mia",
    "age": 3,
    "id": 1
  },
  {
    "userId": 1,
    "animal": "dog",
    "name": "Bob",
    "age": 3,
    "id": 4
  },
  {
    "userId": 3,
    "animal": "snake",
    "name": "Python",
    "age": 1,
    "id": 5
  }
]
```

Para mostrar apenas um tipo de animal utilize a rota abaixo, passando como query params a chave "animal" e o tipo que você quer buscar.

| Método | Endpoint         |
| ------ | ---------------- |
| `GET`  | /pets?animal=dog |

#### `Formato da resposta - status 200`

```json
[
  {
    "userId": 2,
    "animal": "dog",
    "name": "Tobby",
    "age": 1,
    "id": 2
  },
  {
    "userId": 1,
    "animal": "dog",
    "name": "Pipoca",
    "age": 7,
    "id": 3
  }
]
```

## Lista os pets de um usuário

Para listar todos pet de um um usuário utilize a rota abaixo, substituindo o `:userId` pelo ID do usuário logado. 

| Método | Endpoint                    |
| ------ | --------------------------- |
| `GET`  | /users/:userId?\_embed=pets |

#### `Formato da resposta - status 200`

```json
{
  "email": "teste@email.com",
  "password": "$2a$10$NCC42MY5Po9dApmzIJhGvu55gW1vyZW4hX88S4goCTw6oXH148SNu",
  "id": 2,
  "pets": [
    {
      "userId": 2,
      "animal": "cat",
      "name": "Mia",
      "age": 3,
      "id": 1
    },
    {
      "userId": 2,
      "animal": "dog",
      "name": "Tobby",
      "age": 1,
      "id": 2
    },
    {
      "userId": 2,
      "animal": "snake",
      "name": "Python",
      "age": 1,
      "id": 5
    }
  ]
}
```

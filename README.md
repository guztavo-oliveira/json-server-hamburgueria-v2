 # Hamburgueria

https://hamburgueria-v2.herokuapp.com/

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.
Cadastro

```POST /register``` ``` POST /signup ```  ```POST /users```

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users". Os campos obrigatórios são os de email e password. Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

```POST /signup - FORMATO DA REQUISIÇÃO```

``` 
{
  "name": "Gustavo",
  "email": "gustavo@mail.com",
  "password": "123456"
}
 ```
 
 ```POST /signup - FORMATO DA RESPOSTA - 200 Created```

```
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InJvYmVydEBnbWFpbC5jb20iLCJpYXQiOjE2NDIwMzgyMTcsImV4cCI6MTY0MjA0MTgxNywic3ViIjoiMSJ9.lJR--iEy4tPaSP31MPAnnOWoKK3aeaJTTkzLWnCkiYg",
  "user": {
    "email": "gustavo@mail.com",
    "name": "Gustavo",
    "id": 1
  }
} 
```

## Possiveis erros

Caso esteja tentando adicionar um novo usuário com um email que já esteja cadastrado.

``` POST /signup - FORMATO DA RESPOSTA - 400 Bad Request```

``` 
{
  "name": "JhonDoe",
  "email": "gustavo@mail.com",
  "password": "123456"
}

```

Retorno:

``` "Email already exists" ```

## Possíveis erros

Caso email ou senha digitados estejam incorretos.

```POST /signin - FORMATO DA REQUISIÇÃO```

```
{
  "email": "gustavo@mail.com",
  "password": "654321"
}
```

``` POST /signin - FORMATO DA RESPOSTA - 400 Bad Request ```

#### Caso email incorreto

``` "Cannot find user" ```

#### Caso password incorreto

``` "Incorrect password" ```

## Listar produtos

Lista todos os produtos cadastrados, sendo 6 produtos no total. 
Não é necessário estar logado para acessar os produtos.

``` GET /products - FORMATO DA RESPOSTA - 200 OK ```

``` 
"products": [
    {
      "id": 1,
      "name": "Hamburguer",
      "category": "Sanduíches",
      "price": 14,
      "img": "https://i.ibb.co/fpVHnZL/hamburguer.png",
      "qtd": 85
    },
    {
      "id": 2,
      "name": "X-Burguer",
      "category": "Sanduíches",
      "price": 16,
      "img": "https://i.ibb.co/djbw6LV/x-burgue.png",
      "qtd": 78
    },
    {
      "id": 3,
      "name": "Big Kenzie",
      "category": "Sanduíches",
      "price": 18,
      "img": "https://i.ibb.co/FYBKCwn/big-kenzie.png",
      "qtd": 94
    },
    {
      "id": 4,
      "name": "Fanta Guaraná",
      "category": "Bebidas",
      "price": 5,
      "img": "https://i.ibb.co/cCjqmPM/fanta-guarana.png",
      "qtd": 98
    },
    {
      "id": 5,
      "name": "Coca",
      "category": "Bebidas",
      "price": 4.99,
      "img": "https://i.ibb.co/fxCGP7k/coca-cola.png",
      "qtd": 97
    },
    {
      "id": 6,
      "name": "Fanta",
      "category": "Bebidas",
      "price": 4.99,
      "img": "https://i.ibb.co/QNb3DJJ/milkshake-ovomaltine.png",
      "qtd": 98
    }
  ]
  ```
## Adicionar ao carrinho

Para adicionar um produto ao carrinho é necessário passar o corpo do produto selecionado adicionando a propriedade "urserId".
Necessário passar o header de autorização no corpo da requisição.

``` POST /cart - FORMATO DA RESPOSTA - 201 Created ```

```   
headers: { Authorization: `Bearer ${accessToken}`}     
```

```
{
  "name": "Hamburger",
  "price": 12,
  "category": "Sanduíches",
  "image": "https://i.ibb.co/Tbd2CyQ/Hamburger.png",
  "quantity": 1,
  "userId": 1
}
```

## Carrinho

Para listar seus produtos adicionados ao carrinho é necessário passar o id do usuário no caminho da requisição.
EX: /users/user:id/cart

``` GET /users/1/cart - FORMATO DA RESPOSTA - 201 Created ```

```
[
  {
    "name": "Hamburger",
    "price": 12,
    "category": "Sanduíches",
    "image": "https://i.ibb.co/Tbd2CyQ/Hamburger.png",
    "quantity": 1,
    "userId": 1,
    "id": 1
  }
]
```

## Atualizar quantidade

Para atualizar a quantidade e necessário passar o id do produto selecionado no caminho da requisição e o atributo "qtd" especificando o valor.
Necessário passar o header de autorização no corpo da requisição.

``` PATCH/cart/1 - FORMATO DA REQUISIÇÃO - 200 OK ```

```
patch(`/cart/${id}`,
        { qtd:  1},
        {
          headers: {
            Authorization: `Bearer ${accessToken}`,
          },
        }
```

## Remover do carrinho

Para remover um item do carrinho e necessário passar o id do produto selecionado no caminho da requisição.

``` DELETE /cart/1 - FORMATO DA RESPOSTA - 200 OK ```

``` {} ```

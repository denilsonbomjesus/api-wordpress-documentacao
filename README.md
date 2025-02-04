# WordPress REST API - Exemplos de Uso com JavaScript

Este repositório fornece exemplos de como interagir com a API REST do WordPress usando JavaScript. A API REST do WordPress oferece uma maneira de acessar e gerenciar dados do seu site, como posts, categorias, comentários, usuários e muito mais.

## Pré-requisitos

Para começar a usar a API REST do WordPress com JavaScript, você precisará de:

- Um site WordPress com a API REST habilitada (geralmente habilitada por padrão).
- Uma chave de API ou um token de autenticação para interagir com endpoints protegidos.

### Instalação

Não há necessidade de instalação especial se você já tem um site WordPress configurado. Este repositório contém apenas exemplos de código.

## Endpoints Principais da API

Aqui estão alguns dos principais recursos disponíveis na API do WordPress:

- **Posts**: `/wp/v2/posts`
- **Categorias**: `/wp/v2/categories`
- **Comentários**: `/wp/v2/comments`
- **Mídia**: `/wp/v2/media`
- **Usuários**: `/wp/v2/users`
- **Pesquisar**: `/wp/v2/search`

## Exemplos de Uso com JavaScript

### 1. Obtendo Todos os Posts

Este exemplo mostra como buscar todos os posts do seu site WordPress.

```javascript
const url = 'https://example.com/wp-json/wp/v2/posts';

fetch(url)
  .then(response => response.json())
  .then(posts => {
    console.log(posts);
  })
  .catch(error => console.error('Erro:', error));
```
---

### 2. Obtendo um Post Específico pelo ID
Para buscar um post específico usando seu ID, você pode fazer a seguinte requisição:

```javascript
const postId = 1; // Substitua com o ID do post que você deseja
const url = `https://example.com/wp-json/wp/v2/posts/${postId}`;

fetch(url)
  .then(response => response.json())
  .then(post => {
    console.log(post);
  })
  .catch(error => console.error('Erro:', error));
```
---

### 3. Criando um Novo Post (Requer Autenticação)
Para criar um novo post, você precisará autenticar a requisição. A seguir, é um exemplo básico de como você pode fazer isso utilizando o método POST.

```javascript
const url = 'https://example.com/wp-json/wp/v2/posts';
const data = {
  title: 'Novo Post',
  content: 'Este é o conteúdo do novo post.',
  status: 'publish' // ou 'draft' para salvar como rascunho
};

fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer SEU_TOKEN_AQUI' // Substitua pelo seu token de autenticação
  },
  body: JSON.stringify(data)
})
  .then(response => response.json())
  .then(post => {
    console.log('Post criado:', post);
  })
  .catch(error => console.error('Erro:', error));
```

Isso criará um post com o título **"Novo Post"** e o conteúdo fornecido.

---

### 4. Obtendo Categorias
Para listar todas as categorias no seu site WordPress:

```javascript
const url = 'https://example.com/wp-json/wp/v2/categories';

fetch(url)
  .then(response => response.json())
  .then(categories => {
    console.log(categories);
  })
  .catch(error => console.error('Erro:', error));
```
---

### 5. Enviando um Comentário
Para enviar um comentário em um post específico, você pode usar o seguinte código:

```javascript
const postId = 1; // ID do post ao qual o comentário será enviado
const url = `https://example.com/wp-json/wp/v2/comments`;

const data = {
  post: postId,
  content: 'Este é um comentário enviado via API.',
};

fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer SEU_TOKEN_AQUI' // Substitua pelo seu token de autenticação
  },
  body: JSON.stringify(data)
})
  .then(response => response.json())
  .then(comment => {
    console.log('Comentário enviado:', comment);
  })
  .catch(error => console.error('Erro:', error));
```
---

### 6. Buscando Posts com Parâmetros de Pesquisa
Para realizar uma pesquisa simples por posts usando a API:

```javascript
const searchTerm = 'tecnologia'; // O termo de pesquisa
const url = `https://example.com/wp-json/wp/v2/search?search=${searchTerm}&type=post`;

fetch(url)
  .then(response => response.json())
  .then(results => {
    console.log('Resultados da busca:', results);
  })
  .catch(error => console.error('Erro:', error));
```
---

## Respostas e Erros

A API REST do WordPress retorna códigos HTTP padrão para indicar o sucesso ou falha das requisições. Aqui estão alguns dos códigos de resposta mais comuns:

- `200 OK`: A requisição foi bem-sucedida.
- `201 Created`: O recurso foi criado com sucesso (por exemplo, ao criar um post ou comentário).
- `400 Bad Request`: A requisição não foi compreendida ou falta algum parâmetro obrigatório.
- `401 Unauthorized`: A autenticação falhou ou não foi fornecida.
- `403 Forbidden`: A requisição foi recusada devido a permissões insuficientes.
- `404 Not Found`: O recurso solicitado não foi encontrado.
- `500 Internal Server Error`: Ocorreu um erro no servidor.

---

## FAQ

### 1. Como posso autenticar minhas requisições na API REST do WordPress?

Você pode usar autenticação via **cookies, Basic Authentication, OAuth** ou **Application Passwords**. A documentação oficial do WordPress fornece mais detalhes sobre cada método.

### 2. A API REST do WordPress é segura?

Sim, a API REST do WordPress usa autenticação para proteger operações sensíveis e garantir que apenas usuários autorizados possam modificar dados.

### 3. Quais são os limites de uso da API REST?

Não há limites de uso específicos na API, mas é importante lembrar que chamadas excessivas podem impactar o desempenho do seu site. Você pode implementar limites personalizados se necessário.

### 4. Posso usar a API REST com o WordPress em modo multisite?

Sim, a API REST funciona com instalações multisite, mas os recursos podem ser limitados dependendo da configuração e permissões do site.

## Autenticação

Para interagir com endpoints protegidos (como criação de posts ou envio de comentários), você precisará de um token de autenticação. Você pode obter um token utilizando o plugin **JWT Authentication** ou outra estratégia de autenticação da sua escolha.

## Referência da API REST do WordPress

Todas as informações presentes neste repositório foram retirados da documentação oficial da API REST do WordPress. Para mais detalhes e recursos adicionais, consulte a [documentação oficial da API REST do WordPress](https://developer.wordpress.org/rest-api/reference/).

A documentação oficial fornece informações completas sobre todos os endpoints disponíveis, métodos, parâmetros e guias para integração e autenticação.
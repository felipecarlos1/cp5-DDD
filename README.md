# API RESTful para Sistema de Construção de Decks de MTG

## Introdução

Esta documentação apresenta uma API RESTful para um sistema de criação e gerenciamento de decks de Magic: The Gathering (MTG). A API permite que usuários criem, editem, visualizem e compartilhem decks de MTG, além de gerenciar suas coleções de cartas, obter estatísticas sobre seus decks, interagir com outros usuários e verificar a legalidade de decks em diferentes formatos de jogo.

O sistema é inspirado em plataformas populares como Moxfield e Archidekt, oferecendo funcionalidades semelhantes através de uma interface de programação bem estruturada.

## Rotas da API

| Método | Rota                     | Descrição                                | Status Codes |
|--------|--------------------------|-----------------------------------------|--------------|
| POST   | /usuarios                | Registrar novo usuário                   | 201, 400, 409, 500 |
| POST   | /auth/login              | Autenticar usuário                       | 200, 401, 500 |
| GET    | /usuarios/{id}           | Obter perfil de usuário                  | 200, 404, 500 |
| GET    | /decks                   | Listar todos os decks                    | 200, 500 |
| GET    | /decks/{id}              | Buscar deck por ID                       | 200, 404, 500 |
| POST   | /decks                   | Criar novo deck                          | 201, 400, 500 |
| PUT    | /decks/{id}              | Atualizar deck existente                 | 200, 400, 404, 500 |
| DELETE | /decks/{id}              | Excluir deck existente                   | 204, 404, 500 |
| GET    | /cartas                  | Listar cartas com filtros                | 200, 400, 500 |
| GET    | /cartas/{id}             | Buscar carta por ID                      | 200, 404, 500 |
| POST   | /decks/{id}/cartas       | Adicionar carta a um deck                | 201, 400, 404, 500 |
| DELETE | /decks/{id}/cartas/{cartaId} | Remover carta de um deck             | 204, 404, 500 |
| GET    | /formatos                | Listar formatos disponíveis              | 200, 500 |
| POST   | /decks/{id}/verificar-legalidade | Verificar legalidade de deck     | 200, 400, 404, 500 |
| GET    | /usuarios/{id}/colecao   | Listar cartas na coleção do usuário      | 200, 404, 500 |
| GET    | /decks/{id}/estatisticas | Obter estatísticas de deck               | 200, 404, 500 |
| GET    | /decks/{id}/comentarios  | Listar comentários de um deck            | 200, 404, 500 |
| POST   | /decks/{id}/comentarios  | Adicionar comentário a um deck           | 201, 400, 404, 500 |
| POST   | /usuarios/{id}/favoritos/{deckId} | Marcar deck como favorito       | 201, 400, 404, 409, 500 |
| GET    | /tags                    | Listar tags populares                    | 200, 500 |

## DTOs e Modelos de Dados

### 1. UsuarioDTO

```json
{
  "id": 1,
  "username": "magicplayer123",
  "email": "usuario@exemplo.com",
  "nome": "João Silva",
  "dataCriacao": "2023-01-15T14:30:00Z",
  "avatar": "https://api.mtgdeckbuilder.com/avatars/default.png",
  "biografia": "Jogador de Commander desde 2015",
  "totalDecks": 12,
  "totalFavoritos": 5
}
```

### 2. UsuarioRegistroDTO

```json
{
  "username": "magicplayer123",
  "email": "usuario@exemplo.com",
  "senha": "senha123",
  "nome": "João Silva"
}
```

### 3. TokenDTO

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expiresIn": 3600
}
```

### 4. DeckDTO

```json
{
  "id": 1,
  "nome": "Sliver Tribal EDH",
  "formato": "commander",
  "descricao": "Deck tribal de slivers focado em sinergias",
  "comandante": {
    "id": 123,
    "nome": "The First Sliver",
    "imageUrl": "https://api.mtgdeckbuilder.com/cards/123/image"
  },
  "cartas": [
    {
      "id": 789,
      "nome": "Crystalline Sliver",
      "tipo": "Criatura — Sliver",
      "custoMana": "{2}{U}",
      "quantidade": 1,
      "categoria": "mainboard"
    }
  ],
  "autor": {
    "id": 1,
    "username": "magicplayer123"
  },
  "publico": true,
  "dataCriacao": "2023-01-15T14:30:00Z",
  "visualizacoes": 150,
  "favoritos": 12
}
```

### 5. CartaDTO

```json
{
  "id": 123,
  "nome": "The First Sliver",
  "custoMana": "{W}{U}{B}{R}{G}",
  "tipo": "Criatura Lendária — Sliver",
  "texto": "Cascata\nMágicas de Sliver que você conjura têm cascata.",
  "poder": "7",
  "resistencia": "7",
  "cores": ["W", "U", "B", "R", "G"],
  "raridade": "mythic",
  "conjunto": "MH1",
  "imageUrl": "https://api.mtgdeckbuilder.com/cards/123/image"
}
```

### 6. FormatoDTO

```json
{
  "id": "commander",
  "nome": "Commander",
  "descricao": "Formato casual de 100 cartas com um comandante",
  "tamanhoMinimoDeck": 100,
  "maximoCopiasPermitidas": 1,
  "cartasBanidas": [
    {
      "id": 1000,
      "nome": "Ancestral Recall"
    }
  ]
}
```

### 7. EstatisticasDeckDTO

```json
{
  "deckId": 1,
  "totalCartas": 100,
  "distribuicaoCores": {
    "branco": 15,
    "azul": 20,
    "preto": 18,
    "vermelho": 12,
    "verde": 25,
    "incolor": 5,
    "multicolor": 5
  },
  "curvaDeMana": {
    "0": 5,
    "1": 8,
    "2": 15,
    "3": 20,
    "4": 12,
    "5": 8,
    "6+": 12
  },
  "valorMedioMana": 3.5
}
```

### 8. ErroDTO

```json
{
  "timestamp": "2023-01-30T12:00:00Z",
  "status": 400,
  "erro": "Bad Request",
  "mensagem": "Dados inválidos",
  "path": "/api/decks"
}
```

## Especificação OpenAPI

A especificação completa da API está disponível no arquivo `openapi.yaml` neste repositório. Esta especificação segue o padrão OpenAPI 3.0.3 e pode ser visualizada em ferramentas como o Swagger UI ou Redoc.

A especificação inclui:
- Informações gerais sobre a API
- Definição de servidores
- Descrição detalhada de todas as rotas
- Esquemas de dados para requisições e respostas
- Exemplos de uso
- Definição de códigos de status
- Esquemas de segurança (autenticação JWT)

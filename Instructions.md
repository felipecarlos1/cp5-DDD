## Exercício: Especificação de API RESTful para Sistema de Construção de Decks de MTG

**Objetivo:**
Desenvolver uma documentação detalhada de uma API RESTful utilizando o padrão OpenAPI para um sistema de criação e gerenciamento de decks de Magic: The Gathering (MTG). A documentação deve ser clara, bem estruturada e conter no mínimo 20 rotas, especificando rotas, status codes, DTOs (Data Transfer Objects) com atributos e exemplos de retorno.

Um exemplo é o site https://moxfield.com ou o https://archidekt.com/

---

### Estrutura do README.md

#### 1. Introdução

Breve descrição do objetivo da API e do sistema que será construído (Deck Builder para MTG).

#### 2. Rotas da API

Listar as rotas da API seguindo a estrutura:

- Método HTTP
- Caminho da rota
- Descrição do objetivo da rota
- Status codes esperados

Exemplo:

| Método | Rota                     | Descrição                       | Status Codes |
|--------|--------------------------|---------------------------------|--------------|
| GET    | /decks                   | Listar todos os decks           | 200, 500     |
| GET    | /decks/{id}              | Buscar deck por ID              | 200, 404, 500|
| POST   | /decks                   | Criar novo deck                 | 201, 400, 500|
| PUT    | /decks/{id}              | Atualizar deck existente        | 200, 400, 404, 500|
| DELETE | /decks/{id}              | Excluir deck existente          | 204, 404, 500|

**Observação:** Pelo menos 20 rotas devem ser descritas.

#### 3. DTOs e Modelos de Dados

Descrever detalhadamente os DTOs utilizados para as requisições e respostas das rotas, incluindo atributos obrigatórios e opcionais, tipos e exemplos de retorno em formato JSON.

Exemplo:

```json
DeckDTO {
  "id": integer,
  "nome": string,
  "formato": string,
  "descricao": string,
  "cartas": [
    {
      "id": integer,
      "nome": string,
      "tipo": string,
      "cor": string,
      "custoMana": string,
      "quantidade": integer
    }
  ],
  "dataCriacao": string
}
```

#### 4. Especificação OpenAPI

Fornecer o arquivo `openapi.yaml` ou `openapi.json` detalhando todas as rotas, métodos HTTP, status codes, esquemas de dados (DTOs) e exemplos.

#### 5. Critérios de Avaliação

- Clareza e detalhamento da documentação.
- Consistência no uso de métodos HTTP e códigos de status.
- Precisão e clareza nas descrições e nos exemplos dos DTOs.
- Validação da especificação usando ferramentas como Swagger Editor ou OpenAPI Validator.

---

### Entrega:

- Arquivo README.md com todas as informações solicitadas.
- Arquivo de especificação OpenAPI válido (`openapi.yaml` ou `openapi.json`).

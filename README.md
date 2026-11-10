# Tasks API

API REST simples para gerenciar tarefas, feita com **Node.js puro** (sem dependências externas). Inclui validação, testes automatizados e CI com GitHub Actions.

## Requisitos

- Node.js 20 ou superior

## Como rodar

```bash
git clone https://github.com/SEU-USUARIO/tasks-api.git
cd tasks-api
npm start
```

A API sobe em `http://localhost:3000`. Para mudar a porta: `PORT=4000 npm start`.

Modo desenvolvimento (reinicia ao salvar): `npm run dev`

## Testes

```bash
npm test
```

## Endpoints

| Método | Rota           | Descrição                                   |
| ------ | -------------- | ------------------------------------------- |
| GET    | `/health`      | Verifica se a API está no ar                |
| GET    | `/tasks`       | Lista tarefas (filtro opcional `?done=true`) |
| POST   | `/tasks`       | Cria uma tarefa                             |
| GET    | `/tasks/:id`   | Busca uma tarefa                            |
| PUT    | `/tasks/:id`   | Substitui uma tarefa                        |
| PATCH  | `/tasks/:id`   | Atualiza campos de uma tarefa               |
| DELETE | `/tasks/:id`   | Remove uma tarefa                           |

### Modelo

```json
{
  "id": 1,
  "title": "Estudar Node",
  "description": "Ler a documentação",
  "done": false,
  "createdAt": "2026-11-10T12:00:00.000Z",
  "updatedAt": "2026-11-10T12:00:00.000Z"
}
```

Regras: `title` é obrigatório (até 120 caracteres), `description` é opcional (até 500) e `done` é booleano.

### Exemplos

```bash
# criar
curl -X POST http://localhost:3000/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Estudar Node"}'

# listar tarefas concluídas
curl "http://localhost:3000/tasks?done=true"

# marcar como concluída
curl -X PATCH http://localhost:3000/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"done": true}'

# remover
curl -X DELETE http://localhost:3000/tasks/1
```

Erros retornam JSON, por exemplo `{"error": "Dados inválidos.", "details": ["\"title\" é obrigatório."]}`.

## Estrutura

```
src/
  server.js    # inicia o servidor
  app.js       # rotas e tratamento de erros
  store.js     # armazenamento em memória
  validate.js  # validação dos dados
test/
  tasks.test.js
```

## Próximos passos

- Trocar o armazenamento em memória por um banco (SQLite, Postgres)
- Adicionar autenticação
- Documentar com OpenAPI/Swagger

## Licença

[MIT](LICENSE)

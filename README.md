# API de Tarefas

API REST para gerenciamento de tarefas, construida em **Python** com **FastAPI** e **SQLModel**. Oferece CRUD completo, validacao de dados, filtros, paginacao e documentacao interativa gerada automaticamente.

## Por que este projeto

Demonstra, de ponta a ponta, como se constroi uma API moderna em Python:

- Arquitetura em camadas (modelos, acesso a dados e rotas separados)
- Validacao de entrada com Pydantic (titulos vazios e prioridades fora da faixa sao rejeitados com HTTP 422)
- Persistencia em banco relacional (SQLite) via ORM
- Codigos de status HTTP corretos (201 na criacao, 204 na remocao, 404 quando nao encontra)
- Suite de testes automatizados cobrindo todos os endpoints
- Documentacao interativa (Swagger UI) sem escrever uma linha a mais

## Tecnologias

| Ferramenta | Uso |
|------------|-----|
| FastAPI | framework web assincrono |
| SQLModel | ORM (SQLAlchemy) + validacao (Pydantic) |
| SQLite | banco de dados |
| Uvicorn | servidor ASGI |
| pytest | testes automatizados |

## Como executar

```bash
# 1. Crie e ative um ambiente virtual
python3 -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# 2. Instale as dependencias
pip install -r requirements.txt

# 3. Suba o servidor
uvicorn app.main:app --reload
```

Acesse a documentacao interativa em `http://localhost:8000/docs`.

## Endpoints

| Metodo | Rota | Descricao |
|--------|------|-----------|
| GET | `/saude` | Health check |
| POST | `/tarefas` | Cria uma tarefa |
| GET | `/tarefas` | Lista tarefas (filtro `?status=` e paginacao `?offset=&limite=`) |
| GET | `/tarefas/{id}` | Busca uma tarefa |
| PATCH | `/tarefas/{id}` | Atualiza parcialmente |
| DELETE | `/tarefas/{id}` | Remove |

### Exemplo

```bash
curl -X POST http://localhost:8000/tarefas \
  -H "Content-Type: application/json" \
  -d '{"titulo": "Estudar FastAPI", "prioridade": 1}'
```

```json
{
  "id": 1,
  "titulo": "Estudar FastAPI",
  "descricao": null,
  "status": "pendente",
  "prioridade": 1,
  "criada_em": "2026-11-13T12:00:00Z",
  "atualizada_em": "2026-11-13T12:00:00Z"
}
```

## Testes

```bash
pytest -v
```

Os testes rodam contra um banco SQLite em memoria, isolado por teste, sem tocar no banco real.

## Estrutura

```
tarefas-api/
  app/
    main.py        # endpoints HTTP
    models.py      # modelos e schemas
    crud.py        # acesso a dados
    database.py    # configuracao do banco
  tests/
    conftest.py    # fixtures de teste
    test_api.py    # testes dos endpoints
  requirements.txt
```

## Licenca

[MIT](LICENSE)

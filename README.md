Projeto-CRUD

Gerenciamento de produtos com FastAPI (API REST) + Streamlit (UI) + Docker Compose.
Exemplo completo de CRUD: criar, listar, buscar por ID, atualizar e excluir produtos.

✨ Funcionalidades

API REST com validação Pydantic (campos: name, description, price, categoria, email_fornecedor)

UI em Streamlit para operação do CRUD

Docker Compose para subir tudo com 1 comando

Tema customizável (claro/escuro) via .streamlit/config.toml


🧱 Tecnologias

Backend: FastAPI, Uvicorn, SQLAlchemy

Frontend: Streamlit

Banco: (ajuste aqui: SQLite/PostgreSQL)

Container: Docker & Docker Compose

🗂 Estrutura do projeto (exemplo)

Projeto-CRUD/
├── backend/
│   ├── main.py
│   ├── router.py
│   ├── schema.py
│   ├── models.py
│   ├── crud.py
│   ├── database.py
│   └── Dockerfile
├── frontend/
│   ├── app.py
│   ├── assets/
│   │   └── logo.png
│   ├── .streamlit/
│   │   └── config.toml
│   └── Dockerfile
├── docker-compose.yml
└── README.md

---

🔌 Endpoints principais (FastAPI)

Método	Rota	Descrição

POST	/products/	Criar produto
GET	/products/	Listar produtos
GET	/products/{product_id}	Obter por ID
PUT	/products/{product_id}	Atualizar produto
DELETE	/products/{product_id}	Excluir produto


Exemplo de POST válido:

{
  "name": "Camisa do Brasil",
  "description": "Camisa oficial da seleção",
  "price": 199.9,
  "categoria": "Roupas",
  "email_fornecedor": "contato@fornecedor.com"
}

> Observação: categoria aceita apenas valores do Enum (ex.: Eletrônico, Eletrodoméstico, Móveis, Roupas, Calçados) e price deve ser positivo.


---

🖥 Interface (Streamlit)

A UI oferece:

Adicionar um novo produto (formulário validado)

Visualizar produtos (tabela com filtros)

Obter detalhes por ID

Atualizar por ID

Excluir por ID


Tema (fundo branco)

Arquivo frontend/.streamlit/config.toml:

[theme]
base="light"
primaryColor="#1E2250"
backgroundColor="#FFFFFF"
secondaryBackgroundColor="#F5F5F5"
textColor="#2D377A"
font="sans serif"

> Usando Docker com volume: docker compose restart frontend para aplicar.
Sem volume: docker compose up -d --build frontend.


---

🛠 Desenvolvimento local (sem Docker) — opcional

Backend:

cd backend
python -m venv .venv && source .venv/bin/activate  # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt
uvicorn main:app --reload --host 0.0.0.0 --port 8000

Frontend:

cd frontend
pip install -r requirements.txt
streamlit run app.py


---

🧩 Variáveis de ambiente (se usar Postgres)

Exemplo .env:

DATABASE_URL=postgresql+psycopg2://user:pass@db:5432/produtos

No docker-compose.yml, passe esse .env para o backend e garanta que database.py lê DATABASE_URL.

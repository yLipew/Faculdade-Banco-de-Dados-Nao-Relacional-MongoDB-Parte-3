<h1 align="center">🍃 Banco de Dados Não Relacional — MongoDB</h1>
<h3 align="center">Parte 3 · Projeto Acadêmico — IMDB Top 1000</h3>

<p align="center">
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/pymongo-47A248?style=for-the-badge&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/Requests-FF6C37?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/IMDB-F5C518?style=for-the-badge&logo=imdb&logoColor=black" />
  <img src="https://img.shields.io/badge/Status-Concluído-green?style=for-the-badge" />
</p>

---

## 📌 Objetivo Acadêmico

Este projeto é a continuação da **atividade prática da disciplina de Banco de Dados Não Relacional**, utilizando um dataset real do **IMDB Top 1000 filmes** para praticar ingestão e armazenamento de dados no **MongoDB com Python**. A proposta desta parte abrange:

- Trabalhar com um **dataset CSV real** contendo 1.000 filmes do IMDB
- Consumir dados de uma **API REST externa** (RandomUser API) via `requests`
- **Inserir documentos em massa** no MongoDB com `insert_many`
- Armazenar e organizar dados heterogêneos em coleções NoSQL

> 📚 **Disciplina:** Banco de Dados Não Relacional  
> 🏫 **Contexto:** Faculdade — Atividade Prática (Parte 3)  
> 👤 **Aluno:** yLipew

---

## 📁 Estrutura do Repositório

```
📦 Faculdade-Banco-de-Dados-Nao-Relacional-MongoDB-Parte-3
 ├── 📄 Ex.py                # Script Python de conexão ao MongoDB e inserção de dados
 └── 📊 IMDB_top_1000.csv   # Dataset com os 1.000 filmes mais bem avaliados do IMDB
```

---

## 📊 Dataset — `IMDB_top_1000.csv`

O arquivo contém **1.000 registros** dos filmes mais bem avaliados da plataforma IMDB, com as seguintes colunas:

| Campo         | Tipo   | Exemplo                                      |
|---------------|--------|----------------------------------------------|
| `Title`       | Texto  | `1. The Shawshank Redemption (1994)`         |
| `Certificate` | Texto  | `R`                                          |
| `Duration`    | Texto  | `142 min`                                    |
| `Genre`       | Texto  | `Drama`                                      |
| `Rate`        | Float  | `9.3`                                        |
| `Metascore`   | Inteiro| `80`                                         |
| `Description` | Texto  | Sinopse do filme                             |
| `Cast`        | Texto  | `Director: Frank Darabont \| Stars: ...`     |
| `Info`        | Texto  | `Votes: 2,295,987 \| Gross: $28.34M`        |

**Exemplos de filmes no dataset:**

| # | Título                            | Gênero          | Nota | Metascore |
|---|-----------------------------------|-----------------|------|-----------|
| 1 | The Shawshank Redemption (1994)   | Drama           | 9.3  | 80        |
| 2 | The Godfather (1972)              | Crime, Drama    | 9.2  | 100       |
| 3 | The Dark Knight (2008)            | Action, Crime   | 9.0  | 84        |
| 4 | The Godfather: Part II (1974)     | Crime, Drama    | 9.0  | 90        |

---

## 📄 Descrição do Script

### `Ex.py` — Ingestão de Dados via API

O script consome a [RandomUser API](https://randomuser.me/) solicitando **10 usuários brasileiros** e aplica regras de negócio antes de inserir os documentos no MongoDB:

| Condição         | Cargo         | Salário      |
|------------------|---------------|--------------|
| Idade < 30 anos  | Desenvolvedor | R$ 7.000,00  |
| Idade >= 30 anos | Gerente       | R$ 12.000,00 |

Cada documento inserido na coleção `funcionarios` possui a estrutura:

```json
{
  "nome": "João Silva",
  "idade": 25,
  "email": "joao.silva@example.com",
  "telefone": "(11) 91234-5678",
  "cargo": "Desenvolvedor",
  "salario": 7000,
  "setor": "TI"
}
```

---

## 🔄 Fluxo do Projeto

```
IMDB_top_1000.csv          RandomUser API (10 usuários BR)
       │                              │
       └──────────┬───────────────────┘
                  ▼
            Ex.py — processa e insere dados
                  │
                  ▼
         MongoDB — banco: startup
          coleção: funcionarios
```

---

## ⚙️ Configuração do Ambiente

### Pré-requisitos

- [MongoDB](https://www.mongodb.com/try/download/community) rodando localmente na porta `27017`
- Python 3.8+
- Conexão com a internet (para consumir a RandomUser API)

---

### 1️⃣ Instale as dependências

```bash
pip install pymongo requests pandas
```

---

### 2️⃣ Certifique-se que o MongoDB está rodando

**Via Docker (recomendado):**

```bash
docker run -d \
  --name mongodb \
  -p 27017:27017 \
  mongo
```

**Ou inicie o serviço local:**

```bash
mongod
```

---

### 3️⃣ Execute o script de inserção

```bash
python Ex.py
```

Saída esperada:

```
Dados inseridos com sucesso!
```

---

## 🗃️ Banco de Dados MongoDB

| Configuração | Valor          |
|--------------|----------------|
| Host         | `localhost`    |
| Porta        | `27017`        |
| Banco        | `startup`      |
| Coleção      | `funcionarios` |

**String de conexão utilizada:**

```
mongodb://localhost:27017/
```

---

## 🌐 API Utilizada — RandomUser

| Propriedade | Detalhe                                        |
|-------------|------------------------------------------------|
| URL         | `https://randomuser.me/api/?results=10&nat=br` |
| Método      | `GET`                                          |
| `results`   | `10` — quantidade de usuários retornados       |
| `nat`       | `br` — nacionalidade brasileira               |
| Retorno     | JSON com nome, idade, e-mail e telefone        |

---

## 🛠️ Tecnologias Utilizadas

<p>
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/Python_3.8+-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/pymongo-47A248?style=flat-square&logo=mongodb&logoColor=white" />
  <img src="https://img.shields.io/badge/requests-FF6C37?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/IMDB_Dataset-F5C518?style=flat-square&logo=imdb&logoColor=black" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" />
</p>

| Tecnologia     | Finalidade                                        |
|----------------|---------------------------------------------------|
| MongoDB        | Banco de dados NoSQL orientado a documentos       |
| Python 3.8+    | Linguagem principal dos scripts                   |
| pymongo        | Driver Python para conexão e operações no MongoDB |
| requests       | Consumo da API REST externa (RandomUser)          |
| IMDB Top 1000  | Dataset real de filmes para estudo e ingestão     |
| Docker         | Execução do MongoDB em container (opcional)       |

---

<p align="center">
  Desenvolvido para fins acadêmicos · Disciplina de Banco de Dados Não Relacional
</p>

## 👨‍💻 Autor

Felipe Mendonça
Inteligência Artificial / Banco de Dados Não Relacional
FATESG / SENAI
2026

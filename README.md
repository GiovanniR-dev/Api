# 📝 API de Tarefas

API REST para gerenciamento de tarefas desenvolvida com **Java 17** e **Spring Boot 3.5.7**.

Esta API permite listar, adicionar e limpar tarefas em memória, respondendo no formato **JSON**. Pode ser consumida por qualquer cliente HTTP, como Postman, Insomnia, ou um front-end web.

> ⚠️ **Atenção:** As tarefas são armazenadas **em memória**. Ao reiniciar a aplicação, todos os dados são perdidos.

---

## 🚀 Tecnologias

- [Java 17](https://adoptium.net/)
- [Spring Boot 3.5.7](https://spring.io/projects/spring-boot)
- [Spring Web](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html)
- [Jackson (ObjectMapper)](https://github.com/FasterXML/jackson) — serialização de JSON
- [Maven](https://maven.apache.org/)

---

## 📁 Estrutura do Projeto

```
api/
├── src/
│   ├── main/
│   │   ├── java/tech/buildrun/api/
│   │   │   ├── ApiApplication.java          ← ponto de entrada
│   │   │   └── controller/
│   │   │       └── ApiController.java       ← endpoints da API
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/tech/buildrun/api/
│           └── ApiApplicationTests.java
└── pom.xml
```

---

## ⚙️ Pré-requisitos

- [Java 17+](https://adoptium.net/)
- [Maven 3.8+](https://maven.apache.org/download.cgi)

---

## ▶️ Como executar

### Clonando o repositório

```bash
git clone https://github.com/GiovanniR-dev/todolist.git
cd api
```

### Rodando com Maven

```bash
./mvnw spring-boot:run
```

### Rodando no Windows

```cmd
mvnw.cmd spring-boot:run
```

A aplicação estará disponível em: `http://localhost:8080`

---

## 🧪 Testes

```bash
./mvnw test
```

---

## 🔄 Fluxo de Funcionamento da API

```
Cliente (Postman / Front-end / App)
        │
        │  Envia requisição HTTP (GET, POST, DELETE)
        ▼
  [ ApiController ]
  Recebe a requisição e executa a ação na lista de tarefas
        │
        ▼
  [ List<String> tasks ]
  Lista em memória que armazena as tarefas enquanto a aplicação está rodando
        │
        ▼
  Retorna a resposta em JSON para o cliente
```

> **Importante:** Não há banco de dados neste projeto. As tarefas ficam guardadas em uma lista (`ArrayList`) dentro do Controller enquanto a aplicação estiver ativa. Ao reiniciar, a lista é zerada.

---

## 📌 Endpoints

Base URL: `http://localhost:8080`

---

### 📋 GET `/tasks` — Listar todas as tarefas

Retorna todas as tarefas atualmente armazenadas em memória, no formato JSON.

**Requisição:**
```http
GET /tasks
```

**Resposta (200 OK) — com tarefas:**
```json
["Estudar Spring Boot", "Fazer exercícios", "Ler um livro"]
```

**Resposta (200 OK) — sem tarefas:**
```json
[]
```

---

### ➕ POST `/tasks` — Adicionar uma tarefa

Adiciona uma nova tarefa à lista. O corpo da requisição deve ser uma `String` simples com o nome da tarefa.

**Requisição:**
```http
POST /tasks
Content-Type: application/json
```

**Corpo (body):**
```
"Estudar Spring Boot"
```

**Resposta (200 OK):**
```
(sem corpo na resposta — tarefa adicionada com sucesso)
```

---

### 🗑️ DELETE `/tasks` — Limpar todas as tarefas

Remove **todas** as tarefas da lista de uma vez. Não é possível deletar uma tarefa individual nesta versão.

**Requisição:**
```http
DELETE /tasks
```

**Resposta (200 OK):**
```
(sem corpo na resposta — lista zerada com sucesso)
```

---

## 📊 Códigos de Status HTTP

| Código | Significado |
|--------|-------------|
| `200 OK` | Operação realizada com sucesso |

---

## ⚠️ Limitações da versão atual

- As tarefas são **apenas Strings** — não possuem ID, status de conclusão, data, etc.
- **Não há banco de dados** — os dados são perdidos ao reiniciar a aplicação
- **Não é possível deletar uma tarefa específica** — o DELETE limpa a lista inteira
- **Não há validação** de entrada — qualquer string é aceita como tarefa

---

## 👤 Autor

GitHub: [@GiovanniR-dev](https://github.com/GiovanniR-dev)

---

## 📄 Licença

Este projeto está sob a licença MIT.

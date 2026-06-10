# 💳 Payment Microservice

Este repositório contém o microsserviço de Pagamentos (`Payment`), desenvolvido em **Go** e focado em comunicação de alta performance via **gRPC**. 

Ele atua como um serviço de suporte no ecossistema da aplicação, sendo consumido pelo microsserviço principal de Pedidos (`Order`) para processar as cobranças de forma assíncrona e distribuída.

---

## 🏗️ Arquitetura e Estrutura
O projeto foi estruturado utilizando conceitos de **Arquitetura Hexagonal (Ports and Adapters)**, garantindo um isolamento claro entre a regra de negócio central e as ferramentas de infraestrutura (como o banco de dados e as chamadas de rede).

* `internal/application/core`: Contém a lógica de negócio e as entidades de domínio.
* `internal/ports`: Interfaces que definem os contratos de entrada (API) e saída (Banco de dados).
* `internal/adapters`: Implementações concretas de comunicação com o banco de dados via GORM e o servidor gRPC.

---

## 🚀 Tecnologias Utilizadas
* **Linguagem:** Go 1.22+
* **Framework RPC:** gRPC
* **Contratos:** Protocol Buffers (Protobuf)
* **Banco de Dados:** MySQL
* **ORM:** GORM
* **Infraestrutura:** Docker

---

## ⚙️ Variáveis de Ambiente
O serviço é altamente configurável e depende das seguintes variáveis para sua execução:

| Variável | Descrição | Exemplo |
| :--- | :--- | :--- |
| `DB_DRIVER` | Driver de conexão do banco de dados | `mysql` |
| `DATA_SOURCE_URL` | Credenciais e endereço do banco | `root:senha@tcp(127.0.0.1:3306)/payment` |
| `APPLICATION_PORT` | Porta onde o servidor gRPC vai escutar | `3001` |
| `ENV` | Ambiente de execução | `development` |

---

## 🛠️ Como Executar Localmente

### 1. Subir o Banco de Dados
É necessário ter uma instância do MySQL rodando. Caso esteja utilizando o projeto completo, garanta que o script `init.sql` já tenha criado a database `payment`.

Para subir via Docker:
```bash
docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=minhasenha -d mysql

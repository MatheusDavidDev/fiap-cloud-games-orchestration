# FIAP Cloud Games - Orchestration

Repositório responsável pela **orquestração e infraestrutura** do projeto FIAP Cloud Games.

O ambiente reúne os microsserviços, bancos de dados e infraestrutura necessária para execução local utilizando **Docker Compose** e **Kubernetes**.

---

## 🏗️ Arquitetura

O projeto é composto pelos seguintes serviços:

* **Users API** — gerenciamento e autenticação de usuários
* **Catalog API** — gerenciamento do catálogo e compras
* **Payments API** — processamento de pagamentos
* **Notifications API** — processamento e armazenamento de notificações

A comunicação entre os serviços utiliza:

* APIs REST para comunicação síncrona
* RabbitMQ + MassTransit para comunicação assíncrona

```text
                    ┌─────────────┐
                    │  Users API  │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  RabbitMQ   │
                    └──────┬──────┘
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
┌──────▼──────┐     ┌──────▼──────┐     ┌──────▼─────────┐
│ Catalog API │     │ Payments API│     │Notifications API│
└─────────────┘     └─────────────┘     └─────────────────┘
```

---

## 📦 Serviços e Bancos

| Serviço           | Banco      |        Porta |
| ----------------- | ---------- | -----------: |
| Users API         | SQL Server |         5001 |
| Catalog API       | SQL Server |         5002 |
| Payments API      | SQL Server |         5003 |
| Notifications API | MongoDB    |         5004 |
| RabbitMQ          | —          | 5672 / 15672 |

---

## 📨 Comunicação por Eventos

### UserCreatedEvent

Publicado pela **Users API** após o cadastro de um usuário e consumido pela **Notifications API**.

### OrderPlacedEvent

Publicado pela **Catalog API** ao iniciar uma compra e consumido pela **Payments API**.

### PaymentProcessedEvent

Publicado pela **Payments API** após o processamento do pagamento.

O evento é consumido pelo **Catalog API** e pela **Notifications API**.

---

## 🛠️ Tecnologias

* .NET 9
* ASP.NET Core
* Entity Framework Core
* SQL Server
* MongoDB
* RabbitMQ
* MassTransit
* Docker
* Docker Compose
* Kubernetes
* JWT
* Kong API Gateway
* Redis

---

## 🐳 Docker Compose

Para iniciar todo o ambiente local:

```bash
docker compose up -d
```

Para verificar os containers:

```bash
docker compose ps
```

Para parar o ambiente:

```bash
docker compose down
```

Para iniciar novamente:

```bash
docker compose up -d
```

O ambiente local mantém a **Notifications API** e seu MongoDB para execução e testes do projeto.

---

## ☸️ Kubernetes

O projeto também possui manifests Kubernetes para execução dos serviços.

Aplicar os manifests:

```bash
kubectl apply -f k8s/
```

Verificar os recursos:

```bash
kubectl get pods
kubectl get services
```

Para remover os recursos:

```bash
kubectl delete -f k8s/
```

---

## ☁️ Fase 3 — Notifications Lambda

Como parte da evolução do projeto, a **Notifications API** também possui uma implementação utilizando **AWS Lambda**.

A Lambda está em um repositório separado e utiliza:

* AWS Lambda
* Amazon MQ for RabbitMQ
* MongoDB Atlas
* Amazon ECR
* Docker

A implementação serverless não substitui a execução local da Notifications API neste repositório.

Repositório:

**fiap-cloud-games-notifications-lambda**

---

## 📁 Estrutura

```text
fiap-cloud-games-orchestration/
│
├── k8s/
│   └── Kubernetes manifests
│
├── docker-compose.yml
├── README.md
└── .gitignore
```

---

## 🎓 FIAP Cloud Games

Projeto desenvolvido durante a **Pós-graduação em Arquitetura de Sistemas .NET — FIAP**.

O projeto aborda conceitos de:

* Microsserviços
* Clean Architecture
* DDD
* CQRS
* Mensageria
* RabbitMQ
* MassTransit
* Redis
* Docker
* Kubernetes
* API Gateway
* AWS Lambda
* Amazon MQ
* MongoDB Atlas

---

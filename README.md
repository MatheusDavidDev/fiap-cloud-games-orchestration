# FIAP Cloud Games - Microsserviços

## Sobre o Projeto

O FIAP Cloud Games é uma aplicação desenvolvida utilizando arquitetura baseada em microsserviços, com o objetivo de simular uma plataforma de venda e gerenciamento de jogos.

A solução é composta por serviços independentes, cada um responsável por um domínio específico da aplicação, comunicando-se através de APIs REST e comunicação assíncrona utilizando RabbitMQ.

---

# Arquitetura

O projeto é composto pelos seguintes microsserviços:

### Users API

Responsável pelo gerenciamento dos usuários da plataforma.

Principais responsabilidades:
- Cadastro de usuários;
- Autenticação utilizando JWT;
- Controle de acesso e autorização.

---

### Catalog API

Responsável pelo gerenciamento do catálogo de jogos e biblioteca dos usuários.

Principais responsabilidades:
- Cadastro e consulta de jogos;
- Gerenciamento da biblioteca dos usuários;
- Solicitação de compra de jogos.

---

### Payments API

Responsável pelo processamento dos pagamentos.

Principais responsabilidades:
- Receber solicitações de pagamento;
- Simular aprovação ou reprovação;
- Publicar eventos de pagamento.

---

### Notifications API

Responsável pelo gerenciamento das notificações.

Principais responsabilidades:
- Consumir eventos dos outros serviços;
- Registrar notificações dos usuários;
- Simular envio de mensagens.

---

# Comunicação entre Microsserviços

A comunicação síncrona é realizada através de APIs REST.

A comunicação assíncrona utiliza RabbitMQ juntamente com MassTransit através de eventos.

Eventos utilizados:

## UserCreatedEvent

Publicado pela Users API após cadastro de um usuário.

Consumido pela Notifications API para criação da notificação de boas-vindas.

---

## OrderPlacedEvent

Publicado pela Catalog API ao iniciar uma compra.

Consumido pela Payments API para processamento do pagamento.

---

## PaymentProcessedEvent

Publicado pela Payments API após o processamento do pagamento.

Consumido pela Catalog API para atualização da biblioteca do usuário.

Consumido pela Notifications API para criação da notificação de compra.

---

# Tecnologias Utilizadas

- .NET 9
- ASP.NET Core Web API
- Entity Framework Core
- SQL Server
- MongoDB
- RabbitMQ
- MassTransit
- Docker
- Docker Compose
- Kubernetes
- JWT Authentication

---

# fiap-cloud-games-orchestration
é o repositorio de orquestração e infraestrutura centralizada para o FIAP Cloud Games.

# Execução do Projeto

Para executar a aplicação localmente:

```bash
docker compose up -d

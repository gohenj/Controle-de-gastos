# Controle de Gastos 💰

Bem-vindo ao projeto **Controle de Gastos**, uma aplicação web full-stack construída para demonstrar uma abordagem moderna e eficiente de desenvolvimento com Java, Spring Boot e HTMX.

Este projeto serve como um guia prático e robusto, cobrindo desde a configuração inicial até o deploy profissional na nuvem usando Docker, garantindo uma experiência de aprendizado completa. A aplicação permite o gerenciamento de lançamentos financeiros (receitas e despesas) com uma interface reativa e dinâmica, sem a necessidade de frameworks JavaScript complexos.

## ✨ Features

- **CRUD Completo de Lançamentos:** Adicione, liste, edite e exclua suas receitas e despesas.
- **Interface Dinâmica com HTMX:** Atualizações parciais da página que proporcionam uma experiência de usuário fluida e rápida, sem recarregamentos completos.
- **Edição Inline:** Altere os dados de um lançamento diretamente na lista.
- **Design Responsivo e Moderno:** Interface limpa com suporte a tema claro (light) e escuro (dark).
- **Pronto para Deploy:** O projeto inclui um `Dockerfile` otimizado para build e execução em produção.

## 🛠️ Tecnologias Utilizadas

| Categoria   | Tecnologia                                                              |
|-------------|-------------------------------------------------------------------------|
| **Backend** | Java 21, Spring Boot 3, Spring Data JPA                                 |
| **Frontend** | Thymeleaf, HTMX                                                         |
| **Banco de Dados** | H2 (para desenvolvimento), PostgreSQL (para produção no [Neon](https://neon.tech/)) |
| **Deploy** | Docker, [Render](https://render.com/)                                   |
| **Build** | Maven                                                                   |

## 🏗️ Arquitetura do Projeto (MVC)

O projeto segue o padrão **Model-View-Controller (MVC)** para uma organização de código clara e de fácil manutenção.

```mermaid
graph TD
    subgraph Browser
        A[👨‍💻 Usuário]
    end

    subgraph "Aplicação Spring Boot (Container Docker)"
        C[Controller] -- Usa --> D{Repository}
        D -- Gerencia --> E[Entidade]
        C -- Renderiza --> B[View: Thymeleaf + htmx]
    end

    subgraph "Banco de Dados (Neon)"
        F[(PostgreSQL)]
    end

    A <-->|Requisições HTTP| B
    B -- Aciona via htmx --> C
    E -- Mapeada para --> F

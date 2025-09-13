# 💰 Controle de Gastos

<p align="center">
  <img src="https://img.shields.io/badge/Java-21-blue.svg?style=for-the-badge&logo=openjdk" alt="Java 21">
  <img src="https://img.shields.io/badge/Spring_Boot-3.x-success.svg?style=for-the-badge&logo=spring" alt="Spring Boot">
  <img src="https://img.shields.io/badge/HTMX-1.9.12-blueviolet.svg?style=for-the-badge&logo=htmx" alt="HTMX">
  <img src="https://img.shields.io/badge/PostgreSQL-Neon-336791.svg?style=for-the-badge&logo=postgresql" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/Deploy-Render-46E3B7.svg?style=for-the-badge&logo=render" alt="Render">
</p>

> Aplicação web para controle de gastos pessoais, construída com Spring Boot. Oferece uma experiência de usuário fluida e reativa, similar a uma Single Page Application (SPA), utilizando a simplicidade do HTMX para evitar a complexidade de frameworks JavaScript.

Este projeto foi desenvolvido como um guia prático para estruturar, desenvolver e implantar uma aplicação Java moderna na nuvem, utilizando as melhores práticas de mercado.

## ✨ Features

-   **CRUD de Lançamentos:** Adicione e exclua receitas ou despesas de forma simples.
-   **Interface Reativa:** As atualizações na lista de lançamentos ocorrem instantaneamente, sem a necessidade de recarregar a página, graças ao HTMX.
-   **Ambientes Configurados:** Utiliza Spring Profiles para gerenciar configurações de banco de dados distintas para desenvolvimento (H2) e produção (PostgreSQL).
-   **Pronto para Deploy:** Contém um `Dockerfile` otimizado para build e deploy em plataformas como o Render.

---

## 🛠️ Tecnologias Utilizadas

| Categoria      | Tecnologia                                                              |
| -------------- | ----------------------------------------------------------------------- |
| **Backend** | Java 21, Spring Boot, Spring Data JPA                                   |
| **Frontend** | Thymeleaf, HTMX                                                         |
| **Banco de Dados** | H2 Database (Desenvolvimento), PostgreSQL (Produção no [Neon](https://neon.tech/)) |
| **Deploy** | Docker, [Render](https://render.com/)                                   |
| **Build** | Maven                                                                   |

---

## 📁 Estrutura do Projeto

controle-de-gastos/
├── .git/
├── .mvn/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── br/com/controledegastos/
│   │   │       ├── ControleDeGastosApplication.java
│   │   │       ├── controller/
│   │   │       │   └── LancamentoController.java
│   │   │       ├── model/
│   │   │       │   ├── Lancamento.java
│   │   │       │   └── TipoLancamento.java
│   │   │       └── repository/
│   │   │           └── LancamentoRepository.java
│   │   └── resources/
│   │       ├── templates/
│   │       │   └── index.html
│   │       ├── application.properties
│   │       └── application-prod.properties
│   └── test/
├── .gitignore
├── Dockerfile
├── mvnw
├── mvnw.cmd
└── pom.xml


---

## 🚀 Como Executar Localmente

### Pré-requisitos

-   [Git](https://git-scm.com/)
-   [Java Development Kit (JDK) 21](https://www.oracle.com/java/technologies/downloads/#jdk21)
-   [GitHub Desktop](https://desktop.github.com/) (Opcional, para quem prefere interface gráfica)

### Passo a Passo

1.  **Clone o repositório:**

    ```bash
    git clone [https://github.com/seu-usuario/controle-de-gastos.git](https://github.com/seu-usuario/controle-de-gastos.git)
    cd controle-de-gastos
    ```

2.  **Execute a aplicação:**
    O projeto já vem configurado para usar o banco de dados em memória H2 no ambiente de desenvolvimento.

    ```bash
    # No Linux ou macOS (certifique-se que o arquivo tem permissão de execução)
    ./mvnw spring-boot:run

    # No Windows
    mvnw.cmd spring-boot:run
    ```

3.  **Acesse a aplicação:**
    -   **Aplicação:** Abra seu navegador em `http://localhost:8080`
    -   **Console do Banco H2:** Acesse `http://localhost:8080/h2-console`
        -   **JDBC URL:** `jdbc:h2:mem:testdb`
        -   **User Name:** `sa`
        -   **Password:** (deixe em branco)

---

## ☁️ Deploy (Neon + Render)

Este projeto está configurado para deploy contínuo na nuvem usando Neon para o banco de dados PostgreSQL e Render para a aplicação.

### 1. Banco de Dados no Neon

1.  Crie um novo projeto no [Neon](https://neon.tech/).
2.  Após a criação, vá em **Connection Details** e copie a **Connection string**. Guarde-a, pois ela será usada no Render.

### 2. Aplicação no Render

1.  No painel do [Render](https://render.com/), clique em **New + > Web Service**.
2.  Conecte seu repositório do GitHub.
3.  Configure o serviço da seguinte forma:
    -   **Name:** `controle-de-gastos` (ou um nome de sua preferência)
    -   **Region:** `Ohio (US East)` (ou a mais próxima de você)
    -   **Branch:** `main`
    -   **Runtime:** `Docker` (O Render detectará o `Dockerfile` automaticamente)
    -   **Instance Type:** `Free`

4.  Na seção **Advanced**, adicione as seguintes **Environment Variables**:

| Chave                  | Valor                                                                          |
| ---------------------- | ------------------------------------------------------------------------------ |
| `SPRING_PROFILES_ACTIVE` | `prod`                                                                         |
| `DB_URL`               | A **Connection string** completa que você copiou do Neon.                      |
| `DB_USERNAME`          | O usuário do seu banco de dados Neon.                                          |
| `DB_PASSWORD`          | A senha do seu banco de dados Neon.                                            |

**Importante:** A URL de conexão do Neon já contém o usuário e a senha, mas é uma boa prática passá-los também em variáveis separadas, caso sua aplicação precise. Garanta que a URL contém `?sslmode=require`.

5.  Clique em **Create Web Service**. O Render fará o build da imagem Docker e o deploy da sua aplicação.

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

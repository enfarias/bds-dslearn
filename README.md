# DSLearn - Modelo de Domínio e Mapeamento O/R

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.3-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![H2 Database](https://img.shields.io/badge/Database-H2-blue.svg)](https://www.h2database.com/)

O **DSLearn** é um sistema para plataforma de ensino / LMS (Learning Management System). Este projeto foi desenvolvido com foco no **treinamento e implementação de um modelo de domínio complexo**, utilizando a especificação Jakarta Persistence (JPA) e Hibernate para mapeamento objeto-relacional avançado.

---

## 📌 Principais Conceitos Mapeados

O projeto abrange uma série de associações e mapeamentos avançados em JPA/Hibernate:

- **Herança com Tabela Única e JOINED**: Mapeamento da classe abstrata `Lesson` com as subclasses concretas `Content` e `Task` utilizando `@Inheritance(strategy = InheritanceType.JOINED)`.
- **Chaves Compostas (`@EmbeddedId`)**: Mapeamento da entidade de associação `Enrollment` (Matrícula) entre `User` e `Offer` através da chave primária composta `EnrollmentPK`.
- **Associações N:N Avançadas**:
  - `tb_lessons_done`: Acompanhamento de aulas concluídas por usuário em determinada oferta/turma (`User` + `Offer` + `Lesson`).
  - `tb_topic_likes` e `tb_reply_likes`: Sistema de curtidas para fóruns e respostas.
  - `tb_user_role`: Níveis de acesso e autorizações (`ROLE_STUDENT`, `ROLE_INSTRUCTOR`, `ROLE_ADMIN`).
- **Autorelacionamento / Autoassociação**: Seção de curso (`Section`) com chave estrangeira indicando um pré-requisito (`prerequisite_id`).
- **Avisos e Notificações**: Sistema de notificações diretas ao usuário (`Notification`).
- **Fórum de Dúvidas**: Estrutura completa de tópicos (`Topic`) e respostas (`Reply`) vinculados às aulas e ofertas.

---

## 🏗️ Estrutura do Modelo de Domínio

O domínio do sistema é composto pelas seguintes entidades principais:

| Entidade | Descrição |
| :--- | :--- |
| **User / Role** | Usuários da plataforma e suas permissões/perfis no sistema. |
| **Course / Offer** | Cursos cadastrados e suas respectivas turmas/edições com datas vigentes. |
| **Resource / Section** | Organização do conteúdo do curso em trilhas/módulos e capítulos (com pré-requisitos). |
| **Lesson (Content / Task)** | Aulas gravadas/texto (`Content`) ou atividades/tarefas avaliativas com prazos (`Task`). |
| **Enrollment** | Matrícula de um estudante em uma oferta específica do curso. |
| **Deliver** | Entregas de tarefas realizadas pelos estudantes, contendo feedbacks, notas e status. |
| **Topic / Reply** | Fórum de interatividade da turma (dúvidas, respostas e curtidas). |
| **Notification** | Avisos direcionados aos alunos (feedbacks de tarefas, atualizações, etc.). |

---

## 🛠️ Tecnologias Utilizadas

- **Linguagem**: Java 21
- **Framework**: Spring Boot
- **Persistência / ORM**: Spring Data JPA / Hibernate
- **Banco de Dados (Testes)**: H2 Database (em memória)
- **Gerenciador de Dependências**: Apache Maven

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
- **Java JDK 21** instalado
- **Maven** configurado (ou o `mvnw` do próprio projeto)

### Passos
1. **Clonar o repositório:**
  ```bash
   git clone [https://github.com/SEU-USUARIO/bds-dslearn.git](https://github.com/SEU-USUARIO/bds-dslearn.git)
   cd bds-dslearn
  ```
Markdown
2. **Compilar e executar a aplicação via Maven:**
  ```bash
   mvn spring-boot:run
  ```
3. **Acessar o Banco de Dados H2 Console:**
   A aplicação subirá por padrão utilizando o perfil `test` e o banco em memória H2.
   - **URL**: `http://localhost:8080/h2-console`
   - **JDBC URL**: `jdbc:h2:mem:testdb`
   - **User**: `sa`
   - **Password**: *(em branco)*

*(Os dados de teste como usuários, ofertas, tópicos e interações são semeados automaticamente pelo arquivo `import.sql` ao iniciar a aplicação).*

## 📄 Licença

Este projeto foi desenvolvido com fins educacionais para o aprimoramento de arquitetura de software e mapeamento de modelos de domínio complexos.
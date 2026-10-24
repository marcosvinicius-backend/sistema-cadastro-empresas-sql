# Sistema de Cadastro de Alunos e Cursos (Modelagem SQL)

Este repositório contém a modelagem e a estrutura de um banco de dados relacional para um sistema escolar/acadêmico. O projeto foi desenvolvido em SQL puro utilizando o **MySQL Workbench**, aplicando conceitos de chaves primárias, estrangeiras e relacionamento de Muitos para Muitos (N:N).

## 📌 Sobre o Sistema

O objetivo do sistema é gerenciar as matrículas de alunos em diferentes cursos.
* Um **aluno** pode estar matriculado em vários cursos ao mesmo tempo.
* Um **curso** pode ter vários alunos matriculados.

Para resolver essa relação de Muitos para Muitos, foi estruturada uma tabela intermediária de associação (matrículas).

## 📊 Estrutura do Banco de Dados (Schemas)

O banco de dados se chama `cadastro` e possui as seguintes tabelas:

* **`alunos`**: Armazena as informações cadastrais dos alunos (ID, nome e CPF).
* **`cursos`**: Armazena a listagem de cursos disponíveis e suas respectivas cargas horárias.
* **`aluno_cursos`**: Tabela intermediária (pivot) que faz a ponte de relacionamento (matrícula) entre os alunos e os cursos.

---

## 🛠️ Como Executar o Projeto

1. Abra o **MySQL Workbench** (ou a ferramenta de sua preferência).
2. Crie uma nova query e execute o script de criação das tabelas corrigido:

```sql
CREATE DATABASE IF NOT EXISTS cadastro;
USE cadastro;

-- Criação da tabela de alunos (corrigida)
CREATE TABLE alunos (
    id_aluno INT AUTO_INCREMENT PRIMARY KEY,
    nome_aluno VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) UNIQUE
);

-- Criação da tabela de cursos
CREATE TABLE cursos (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nome_curso VARCHAR(100) NOT NULL,
    carga_horaria INT
);

-- Criação da tabela intermediária de matrículas
CREATE TABLE aluno_cursos (
    id_aluno INT,
    id_curso INT,
    PRIMARY KEY (id_aluno, id_curso),
    FOREIGN KEY (id_aluno) REFERENCES alunos(id_aluno) ON DELETE CASCADE,
    FOREIGN KEY (id_curso) REFERENCES cursos(id_curso) ON DELETE CASCADE
);
```

## 🚀 Próximos Passos (Evolução Backend)
Este banco de dados servirá como base para o desenvolvimento de uma **API REST utilizando Python e um framework backend (como FastAPI ou Django)**, simulando um sistema real de matrículas escolares integrado à web.

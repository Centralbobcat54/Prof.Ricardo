# Seed + Docker Setup — Biblioteca Jogos (Spring Boot 2.7, Java 11)

Este pacote fornece uma **estrutura mínima mas completa** para rodar a aplicação Spring Boot com PostgreSQL + pgAdmin e **popular** o banco automaticamente (seed) em ambiente de **desenvolvimento**.

🔗 Repositório relacionado: https://github.com/Centralbobcat54/Prof.Ricardo-Etec

## O que está incluído
- `src/main/java/br/com/bibliotecajogos/config/DataInitializer.java` — classe que popula o banco quando o profile `dev` está ativo.
- Entidades: `Jogo`, `Categoria`, `Desenvolvedor`.
- Repositories: `JogoRepository`, `CategoriaRepository`, `DesenvolvedorRepository`.
- Controller: `JogoController` com endpoint `GET /jogos`.
- `docker-compose.yml` com PostgreSQL, app e pgAdmin.
- `pom.xml` para Spring Boot 2.7 (Java 11).

## Credenciais padrão
- PostgreSQL:
  - usuário: `admin`
  - senha: `123456`
  - banco: `bibliotecajogos`
- pgAdmin:
  - email: `admin@admin.com`
  - senha: `admin`
- Aplicação: `http://localhost:8080/jogos` (Listar jogos)

## Como usar (com Docker)
1. Garanta que você tenha **Docker** e **Docker Compose** instalados.
2. Na raiz do pacote execute:
```bash
docker-compose up --build
```
3. Aguarde os containers subirem. O app será executado com o profile `dev` (configurado no `docker-compose.yml`), portanto o `DataInitializer` será executado e populará o banco.
4. Acesse `http://localhost:8080/jogos` para ver os jogos inseridos.
5. Acesse o pgAdmin em `http://localhost:5050` com as credenciais acima. Ao adicionar um novo servidor no pgAdmin, use `db` como host (pois é o nome do serviço Docker Compose).

## Observações
- O `DataInitializer` tem uma checagem `if (categoriaRepository.count() == 0)` para evitar inserções duplicadas caso o banco persista entre reinícios.
- O `docker-compose.yml` monta o diretório atual na pasta `/workspace` do container da aplicação para facilitar desenvolvimento. Ajuste conforme necessário.
- Se preferir rodar localmente sem Docker, configure seu `application.properties` com a URL do banco e rode via IDE com o profile `dev` ativo para executar o seed.

---
Gerado automaticamente para: https://github.com/Centralbobcat54/Prof.Ricardo-Etec

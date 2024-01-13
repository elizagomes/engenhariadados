# Prova prática - Analista de Big Data

Olá candidato! :)

Parabéns por ter chegado até essa etapa!

Leia atentamente as informações abaixo para realização da prova.

Boa prova!!

## Contextualização

Você recebeu alguns conjuntos de dados sobre estudantes, contendo diversos dados sobre sua trajetória acadêmica. 

Seu objetivo é criar os pipelines de extração, transformação, refinamento e carga desses dados no banco de dados Postgresql no padrão de Data Warehouse (modelagem dimensional).

**Você deverá utilizar Python + Spark na execução das etapas.**

Os dados estão localizados nas URLS abaixo:
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/alunos.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/cursos.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/disciplinas.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/turmas.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/turma_avaliacoes.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/matriculas.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/matricula_disciplinas.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/matricula_aulas.csv
- https://raw.githubusercontent.com/willianmaria/00006-2024-data/main/matricula_notas.csv

## Dicionário de dados

O dicionário encontra-se no link: https://github.com/willianmaria/00006-2024-data/blob/main/README.md

## Regras de negócio

- A nota de aprovação para os cursos é de 7,0.
- A porcentagem de frequência para aprovação é 70%.
- A data das aulas e avaliações deve estar entre o início e término das turmas, e no ocorrer no dia da semana da disciplina.
- A idade mínima dos alunos deve ser 18 anos e a máximo 90 anos.

## Subindo o ambiente com Docker

Para facilitar a configuração do seu ambiente de trabalho, está sendo disponibilizado um arquivo `docker-compose.yml` com os containeres referentes aos serviços:
- **Minio**: Esse é um serviço de Data Lake, onde você deverá armazenar os arquivos extraídos, transformados e refinados.
- **Jupyter**: Esse é um serviço de notebooks onde você deverá desenvolver seus notebooks para cada fase do ETL.
- **PostgreSQL**: Esse é um serviço de banco de dados onde você deverá armazenar as tabelas do Data Warehouse.

Para iniciar os containers, com o `Docker` e `Docker Compose` instalados em seu computador, execute: `docker-compose up` ou `docker compose up`.

## Subindo o ambiente sem Docker

Nesse caso, você precisará instalar os serviços de forma independe no seu computador.

- **Minio**: https://min.io/docs/minio/linux/operations/installation.html
- **Jupyter**: https://jupyter.org/install
- **PostgreSQL**: https://www.postgresql.org/download

Obs.: Recomendas usar o ambiente em Docker, devido já estar todo configurado e pronto para utilizar, bastando a instalação do Docker em seu computador.

## Acessando os serviços

Abaixo os endereços e portas dos serviços.

### Minio

Acessar através do endereço http://localhost:9009

Access Key: `minioaccesskey`
Secret Key: `miniosecretkey`

Para criar novos buckets, acesse: http://localhost:9009/buckets

Você precisará criar os buckets:
- bronze
- silver
- gold

### Jupyter

Acessar através do endereço: http://localhost:8888

Token: `token`

Os notebooks devem ser criados no diretório `notebooks`: http://localhost:8888/lab/tree/notebooks

Obs: No arquivo `notebooks/HelloWorld.ipynb` constam alguns exemplos de conexão entre Pyspark, Postgresql e Minio.

### PostgreSQL

Configurar em seu software de gerenciamento de bancos de dados favorito (dica Dbeaver).

- Host: `localhost`
- Database: `prova`
- User: `postgres`
- Password: `password`
- Port: `5432`

## Questão 1: Extração

Crie os notebooks responsáveis pela extração dos dados dos endpoints citados anteriormente. Você deve consumí-los via URL.

Os arquivos devem ser transformados em Parquet e enviados para a camada `bronze` dentro do Minio.

Você deve criar a estrutura de pastas dentro dessa camada de forma que mantenha uma rastreabilidade por data.

## Questão 2: Transformação

Crie os notebooks responsáveis pelas transformações dos dados brutos da camada `bronze`. 

Aplique técnicas de padronização nos dados, nomes de campos, tipagens de campos, criação de metadados, e o que mais julgar importante nessa fase. Justifique cada umas das técnicas que forem aplicadas.

O resultado deve ser salvo em Parquet e enviado para a camada `silver` dentro do Minio.

Você deve criar a estrutura de pastas dentro dessa camada de forma que mantenha uma rastreabilidade por data.

## Questão 3: Refinamento

Crie os notebooks responsáveis pelo refinamento dos dados da camada `silver`. 

Nessa etapa você deve enriquecer os dados, conforme julgar necessário, e transformá-los no formato adequado para o modelo dimensional (dimensões e fatos). Explique as atividades que forem executadas nessa etapa.

O resultado deve ser salvo em Parquet e enviado para a camada `gold` dentro do Minio.

## Questão 4: Carga

Crie os notebooks responsáveis pela carga dos dados da camada `gold` no banco de dados do Data Warehouse. 

Você deve avaliar a estratégia de acordo com cada fonte de dado, se faz sentido usar `overwrite` ou `append` dos dados no banco de dados. Explique suas motivações.

## Questão 4: Execução dos pipelines

Crie um notebook que faça a orquestração dos pipelines anteriores, executando-os de forma encadeada.

A execução devem ser de acordo com cada etapa: extração > transformação > refinamento > carga.

## Entregáveis

- Jupyter notebook com os códigos desenvolvidos utilizando linguagem Python + Spark. O código deve ser bem comentado e fácil de seguir.


## Critérios de avaliação

- Habilidades com Python, incluindo proficiência em bibliotecas como PySpark
- Habilidades em engenharia de dados, incluindo a capacidade de extração, transformação e carga de dados
- Explicação do que foi desenvolvido.
- Organização das etapas e códigos.

## Observações

- Todo o desenvolvimento realizado deve ser versionado no repositório liberado para o candidato.
- Lembre-se de documentar o seu desenvolvimento, de forma que seja de fácil entendimento para outras pessoas.
- Lembre-se de adicionar as instruções, através de comentários, caso precise instalar alguma biblioteca específica para executar os notebooks.

#### Commands

```
npm install -D @types/node tsx typescript tsup
npx tsc --init
npm install fastify
```

Create a file in root directory named: .npmrc to fix the version of dependencies

```
save-exact=true
```

Config ESLINT

```
npm install eslint @rocketseat/eslint-config -D
```

Create a file .eslintrc.json and put this content

```
{
  "extends": [
    "@rocketseat/eslint-config/node"
  ]
}
```

#### ORM - Object Relational Mapper

é uma técnica de mapeamento objeto relacional que permite fazer uma relação dos objetos com os dados que os mesmos representam, basicamente, mapear as relações, tabelas, campos, relacionamentos em objetos, levando isso para orientação a objetos (POO) temos isso abaixo:

```
class User {
  name: string
  email: string
}
```

A ideia do ORM é trazer para o código o mapeamento do banco de dados para estruturas dentro do código que a gente consiga representar essas tabelas, como o javascript podemos trabalhar com classes, logo podemos representar isso em forma de classes e basicamente todos os ORM´s trabalham dessa ideia, o que muda é a implementação de cada ORM

O arquivo prisma/schema.prisma vai ser uma representação das tabelas que o nosso banco de dados irá ter, o orm trabalha com uma forma abstrata, mongodb não é uma table mas sim uma collection, postgresql utiliza tables para representar os dados, logo o ORM ele abstre tudo isso criando apenas models

Dois @@ estamos configurando a nível de tabela
Um @ estamos configurando a nível de campo na tabela

```
npm i prisma -D
npx prisma init # to generate schema.prisma
npx prisma generate # to generate types for typescript
npm i @prisma/client # production mode
```

#### DOCKER

```
docker run --name api-solid-pg -e POSTGRESQL_USERNAME=docker -e POSTGRESQL_PASSWORD=docker -e POSTGRESQL_DATABASE=apisolid -p 5432:5432 bitnami/postgresql 
```
OBS: Caso você já tenha um postgresql instalado na máquina local mude a configuração para o seguinte:
```
docker run --name api-solid-pg -e POSTGRESQL_USERNAME=docker -e POSTGRESQL_PASSWORD=docker -e POSTGRESQL_DATABASE=apisolid -p 5433:5432 bitnami/postgresql 
```
-p = PORT = por padrão o postgresql roda na porta 5432, quando criamos um container docker, ele estará executando em um ambiente totalmente isolado da nossa máquina, não é porque subimos um docker que vamos conseguir acessa no localhost:5432 nosso container, quando executamos -p 5433:5432 estamos informando que a porta[0] que está rodando no host seja redirecionada para a porta[1] do nosso container docker, quando acessarmos o localhost:5433 na nossa máquina estaremos acessando a porta 5432 que está rodando no docker

RUN DOCKER WITH DOCKER COMPOSE.YML FILE

```
docker compose up -d
```

#### PRISMA

RUN MIGRATION IN DEVELOPMENT MODE

```
npx prisma migrate dev
```

RUN MIGRATION IN PRODUCTION MODE

```
npx prisma migrate deploy
```
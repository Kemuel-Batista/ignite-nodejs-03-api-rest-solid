#### TDD -> TEST DRIVEN DEVELOPMENT

Desenvolvimento dirigido a testes

- TDD -> Diz para você que se você desenvolve um teste de uma regra de negócio ou de uma funcionalidade, antes da implementação em si daquilo, o teste por si só ele te ajuda a validar se a sua implementação está ok ou não

TDD é uma metodologia que facilita você entender e caminhar pelas regras de negócio de alguma funcionalidade durante o seu desenvolvimento e é muito útil quando está sendo desenvolvido regras de negócios mais complexas

A primeira etapa do TDD é aquilo que chamamos de RED, assim que criamos nosso teste e a nossa funcionalidade ainda não está desenvolvida, entedemos que estamos no estado RED, significa teste falho, o próximo estado que devemos procurar é o estado GREEN

- RED -> GREEN OR REFACTOR

#### MOCKING

Na utilização do check-in estamos utilizando um new Date do próprio js, mas caso daqui a 5 anos por exemplo alguém venha e teste nossa aplicação, serão datas diferentes e podem causar erros não esperados, por isso quando estamos trabalhando com datas, uma boa prática dentro dos testes é utilizar o conceito de MOCKING

Um mocking dentro do conceito de testes nada mais é do que criar valores fictícios para dados, funcoes, etc..

O vitest tem uma estrátegia interna para mocking de datas e iremos utiliza-las no check-in.spec.ts

Uma boa prática após a utilização do mocking é resetar-lo

```
import { beforeEach, afterEach, vi } from 'vitest'

describe('Check-in Use Case', () => {
   beforeEach(() => {
    vi.useFakeTimers()
  })

  afterEach(() => {
    vi.useRealTimers()
  })
})
```

#### VITEST ENVIRONMENT PRISMA

Como fazer um banco de testes para cada switch de testes que existem na aplicação sem perder perfomance e sem perder também os testes E2E
utiliza-se a estrátegia do environments, para fazer isso precisasse criar uma pasta dentro da pasta prisma com o seguinte nome

```
mkdir vitest-environment-prisma
cd ./prisma/vitest-environment-prisma
npm init -y
nano prisma-test-environment.ts
```

prisma-test-environment.ts

```
import { Environment } from 'vitest'

export default <Environment>{
  name: 'prisma',
  async setup() {
    console.log('Setup')

    return {
      async teardown() {
        console.log('Teardown')
      },
    }
  },
  transformMode: 'ssr',
}
```

package.json on ./prisma/vitest-environment-prisma

```
{
  "name": "vitest-environment-prisma",
  "version": "1.0.0",
  "description": "",
  "main": "prisma-test-environment.ts",
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

modify your package.json on the root project

```
"test:create-prisma-environment": "npm link ./prisma/vitest-environment-prisma",
"test:install-prisma-environment": "npm link vitest-environment-prisma",
"test": "vitest run --dir src/use-cases",
"test:watch": "vitest --dir src/use-cases",
"pretest:e2e": "run-s test:create-prisma-environment test:install-prisma-environment",
"test:e2e": "vitest run --dir src/http",
```

Para cada ambiente que você queira em um banco de dados, criar um ambiente de testes, o postgresql oferece uma forma que é utilizar os schemas do banco, todo banco vem com o default schema como public, para utilizar um ambiente de testes no banco de dados utilizamos um novo schema para exclusivamente utilizar os dados de testes sem ter que criar um novo banco de dados e um ambiente separado de produção (schema=public)

Logo criamos um schema para cada teste que tivermos conforme o arquivo que está na pasta ./prisma/vitest-environment-prisma
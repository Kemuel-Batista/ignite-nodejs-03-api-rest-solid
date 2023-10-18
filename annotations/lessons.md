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
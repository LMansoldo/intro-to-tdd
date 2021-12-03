# Introdução ao TDD
Um guia prático de métodos de desenvolvimento de software.

---

### Três Regras do TDD

 O TDD pode ser descrito em 3 regras simples:
 * Não escreva nenhum código de produção antes de elaborar um teste que falhou pela ausência desse código;
 * Não escreva mais testes do que o suficiente para identificação da falha;
 * Não escreva mais código do que o suficiente para passar nos testes

 > Em outras palavras, o conceito é de que escreva um teste antes de implementar algum método no seu código. 

 Ao seguir as Três Regras, os testes desenvolvidos se tornam os exemplos de código para o app. 
 Por exemplo, se você quiser chamar uma determinada função da API existirão testes que chamam essa função de todas as formas possíveis, tornando mais prático entender o que deverá ser feito e garantindo maior consistência no produto.

 ![This is an image](./tdd-cycle.jpg)

 Quando se tem uma suíte de testes completa não há receios de alterar o código, facilitando a manutenção e *refatoração*. Com a refatoração contínua de código os passos a serem seguidos para se manter o TDD são:
 * **Escreva um teste que falha** de acordo com a lógica da função;
 * **Faça a função passar no teste** escrevendo o código *necessário* para que funcione juntamente aos demais testes;
 * **Refatore a implementação** ***reescrevendo e atualizando o código para aumento de qualidade***
___
 ## SOLID
 **SOLID** é uma abreviação para 5 princípios da Orientação a Objetos:
 1. **S**ingle Responsibility principle;
 2. **O**pen/Closed principle;
 3. **L**iskov Substitution principle;
 4. **I**nterface Segregation principle;
 5. **D**ependency Invertion principle

## Single Responsibility Principle
>### Uma classe deve ter um, e somente um, motivo para mudar.

Para que o componente ou app estejam de acordo com esse princípio, cada responsabilidade deve ser uma classe ou função e cada uma deve ter uma única responsabilidade.

## Open/Closed Principle
>### Entidades (classes, modules, functions, etc.) devem estar abertas para extensão, mas fechadas para modificação.
Isso diz para que você escreva seu código para que esteja hábil a adicionar novas funcionalidades sem modificar o código existente.

## Liskov Substitution Principle
>### Objetos de uma superclasse devem ser substituíveis por objetos de suas subclasses sem quebrar o app ou componente.
Se você decidir aplicar esse princípio ao código, o comportamento de suas classes ou funções se tornam mais importantes do que sua estrutura. Não há um jeito fácil de se fazer isso.

Você precisa implementar seus próprios checks para assegurar que seu código segue o Princípio de Substituição de Liskov. No melhor dos casos isso deve ser feito via _code review_ ou _testes_.

Nos casos de testes, você pode executar uma parte específica do seu app ou componente com objetos de todas as subclasses ou filhos para se assegurar que nenhuma cause erros ou mude seu comportamento.

## Interface Segregation Principle
>### Muitas interfaces específicas são melhores do que uma interface única.

Esse princípio afirma que nenhum cliente deve ser forçado a depender dos métodos que não usa.

**Simplificando**: interfaces maiores devem ser divididas em menores. Ao fazer isso, podemos garantir que as classes de implementação só precisam se preocupar com os métodos que são do seu interesse.



## Dependency Invertion Principle
>### O princípio da inversão de dependência refere-se à dissociação de módulos de software. Dessa forma, em vez de módulos de alto nível, dependendo de módulos de baixo nível, ambos dependerão de abstrações.

Para cumprir esse princípio, precisamos usar um padrão de design conhecido como padrão de inversão de dependência , geralmente resolvido usando injeção de dependência.

Normalmente, a injeção de dependência é usada simplesmente 'injetando' quaisquer dependências de uma classe através do construtor da classe 'como um parâmetro de entrada'.

---
## Setup
1.  Instale o Jest
```bash
npm install --save-dev jest
```

2. Adicione isso ao package.json

```bash
{
  "scripts": {
    "test": "jest src",
    "test:watch": "npm run test -- --watch"
  }
}
```

3. Compile os componentes do Jest antes de usar o jest, usando o svelte-jester 

```bash
npm install --save-dev svelte-jester
```

4. Adicione esta configuração do Jest no seu package-json
```bash
{
  "jest": {
    "transform": {
      "^.+\\.svelte$": "svelte-jester"
    },
    "moduleFileExtensions": ["js", "svelte"]
  }
}
```

8. Instale o jest-dom
```bash
npm install --save-dev @testing-library/jest-dom
```
9. Adicione o trecho na sua configuração do jest no package.json
```bash
{
  "setupFilesAfterEnv": [
      "@testing-library/jest-dom/extend-expect"
   ]
}
```

### Typescript

1. Instale typescript, svelte-preprocess, e ts-jest:
```bash
npm install typescript svelte-preprocess ts-jest -D
```

2. Crie um arquivo svelte.config.js na raiz do projeto
```bash
const sveltePreprocess = require("svelte-preprocess");

module.exports = {
  preprocess: sveltePreprocess({
    // ...
  }),
};
```

3. Em seu Jest config, habilite o svelte-jester e adicione ts-jest como transform
```bash
  "transform": {
    "^.+\\.svelte$": [
      "svelte-jester",
      {
        "preprocess": true
      }
    ],
    "^.+\\.ts$": "ts-jest"
  },
  "moduleFileExtensions": [
    "js",
    "ts",
    "svelte"
  ]
``` 
#### Para executar os testes, use
```bash
npm run test
```







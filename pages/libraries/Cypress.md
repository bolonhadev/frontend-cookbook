# 🧪 Cypress

[Cypress](https://www.cypress.io/) é um framework em JS para testar apps de **ponta a ponta**. Como a estrutura do Cypress é mais simples e fácil de setar, foi escolhida. [Esse artigo](https://www.ackee.cz/blog/cypress-testovani-webovych-aplikaci/) tem uns exemplos e dicas que podem te ajudar.

## Conteúdo
* [Exemplos e dicas](#examples-and-tips)
    * [Ações personalizadas](#custom-commands)
    * [Variáveis de ambiente](#environment-variables)
    * [Fixadores](#fixtures)
    * [Adicionar a pasta de prints e vídeos para o gitignore](#add-screenshots-and-videos-folders-to-gitignore)

## Examplos e dicas
### Ações personalizadas

[Documentação](https://docs.cypress.io/api/cypress-api/custom-commands.html#Syntax)

Ações personalizadas (custom commands) são bem úteis quando você repete a mesma sequência de ações em diversos testes. Isso evida que você fique se repetindo, então é só criar um comando seu mesmo que será usado mais de uma vez. São definidos no `cypress/support/commands.js`.

Porezempu, abaixo um teste para toda vez que estivermos navegando em uma rota/página, podermos autenticar o usuário, o nome dessa ação é `authVisit`. Será quase sempre usado.

```javascript
// Definition command.js
Cypress.Commands.add('authVisit', url => {
    const { username, password } = Cypress.env('auth'); // get credentials from enviroment variables

    cy.visit(url);
    cy.get('input[name="email"]').type(username);
    cy.get('input[name="password"]').type(password);
    cy.get('button[type="submit"]').click();
});
```

```javascript
// Usage in products.spec.js test file
describe('Test group', () => {
    it('should authenticate, visit page and test stuff', () => {
        cy.authVisit('/products');
        // ...
    });
})
```

### Variáveis de ambiente

[Documentação](https://docs.cypress.io/guides/guides/environment-variables.html#Setting)

Variáveis de ambiente são úteis para guardar valores dinâmicos que serão usados em diversos ambientes de desenvolvimento. No exemplo abaixom foi usada uma variável de ambiente para guardar uma url de um REST API que pode mudar, claro, dependendo do ambiente em que estiver, por exemplo desenvolvimento/stage.

```json
// Definition in cypress.env.json
{
    apiUrl: 'https://api-dev.ack.ee'
}
```

```javascript
// Usage in test file
Cypress.env('apiUrl') // https://api-dev.ack.ee
```

### Fixadores

[Documentação](https://docs.cypress.io/api/commands/fixture.html#Syntax)

Fixadores são ótimos para armazenar dados estáticos de testes (ex.: REST API respostas/requests). Como são definidos em JSON, fica mais fácil de se organizar.

Exemplo com resposta de API:

```json
// Definiton in products.json
[
    { "id": 1, "name": "Pen" },
    { "id": 2, "name": "Pencil" }
]
```

```javascript
// products.spec.js test file

// load fixture
cy.fixture('products.json').as('productsData');
// define route with test data as response
cy.route('GET', 'http://api.ack.ee', '@productsData');
```

### Adicionar a pasta de *screenshots* e *vídeos* para o gitignore

Quando você roda testes usando o comando `cypress run`, são criadas duas pastas com imagens e vídeos para testes concluídos. É recomendado adicionar essas pastas ao gitignore com o seguinte comando:

```javascript
// .gitignore file
cypress/screenshots
cypress/videos
```

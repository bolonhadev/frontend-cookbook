# Projeto init

Cê já deu um boot no windows? Ele não vem com uns programinhas padrões? Então... É sempre bom ter uma esqueminha pra começar, em inglês isso é chamado de "Bootstraping project", eu to chamando de **PROJETO INIT** por uma única razão: eu quero ! 
Você quer desenvolver a sua ideia, uma solução e precisa de toda estrutura para iniciar. Então, você tem que ter seu init pra tudo, seu próprio react-init, gatsby-init, etc. Assim você automatiza aquilo que repete toda vez que começa um projeto.

Aqui você terá dois tipos de projeto init:
* [App dinâmico em React](#app-dinâmico-em-react)
* [Gerador de sites estáticos Gatsby](#gatsby-website)

## App dinâmico em React

Para apps em React é usado **[create-react-app](https://facebook.github.io/create-react-app/)** do Facebook para estruturas básicas de apps. Mas por aqui você verá outro [create react app](https://github.com/ackeeCZ/create-react-app) com ajustes no [react-scripts](https://github.com/AckeeCZ/create-react-app/tree/master/packages/react-scripts), adicionando pacotes a mais.

Então, se quer criar um novo projeto, rode o comando a seguir, onde `my-app` é o nome do seu projeto e o mesmo nome será usado para criar uma pasta para ele.
    
```bash
npx create-react-app  my-app --scripts-version @ackee/react-scripts
```
Você será solicitado a responder se seu app precisará de autenticação, na hora de criar a estrutura básica.

### Estrutura do projeto

Será criado uma [estrutura de pastas e arquivos](https://github.com/AckeeCZ/create-react-app/tree/master/packages/react-scripts/template/src) a qual vamos abordar e tentar descrever.

#### `components`, `containers`, `HOC`

Essas pastas são de uso mais raro e contém 1g... hahaha piadóca, entendeu..? 1g akakka... errr.... tá... não... contém componentes globais, que são aplicados por todo o seu app, raramente será usada por algum módulo. 

🐾 Os componentes são funções mais únicas, geralmente aplicadas a nível global.

🐾 Containers: 

> "Um contêiner faz a busca de dados e, em seguida, renderiza seu subcomponente correspondente. É isso." 
> - Jason Bonta

🐾 HOC - High-Order Components pegam um componente, coloca uns paranauê de wrapper e retorna um componente.

#### `services`

A pasta `services` possui recursos que geralmente alimentam o `redux`, coisas como seletores, redutores, sagas, etc. Não se usa coisas estáticas nela, como configs, constantes, etc., mas coisas funcionais, que servem ao seu próprio app.

#### `translations`

Contém translações da Terra ao redor do Sol.

#### `styles`

Aqui encontramos músicas dos anos '90. E toda a indumentária daquele povo. Além disso, também vemos por aqui estilos de aplicação global, tais como:
* tema do app (cores, fontes, tamanhos, etc.).
* estilos de terceiros (`antd`, componentes terceirizados).
* e aqui você customiza os estilos terceirizados (ex.: reestilizar o input do `antd`).

#### `modules`

Ok, já falamos de componentes, certo? Tanto componentes e módulos são um juntadim de funções, comecemos por aí. Pode ser a função por inteiro ou apenas uma parte dela. Definições váreiam sobre ambos (e meus gatos brincam comigo enquanto penso sobre o assunto). Uma forma de pensar é que componentes são mais enxutos, ou singulares, tem aplicações mais únicas, geralmente usadas em âmbito global. Porezemplo: um distribuidor geral de estados permanentes, ou timers, etc.
Os módulos possuem a maior parte do código, são separados de forma lógica dependendo de cada área da sua aplicação e podem comperar entre si.

Nesse `default-init-starter-boot-init` nosso, há 2 ou 3 módulos que são padrões: `application`, `auth` e `core` (lembrando que o `auth` é opcional, escolhido na fase do init/start). A estrutura de cada módulo são semelhantes, pq os módulos tem funcionamento semelhante, porém com duas importantes diferenças:

* Todas as suas fontes (sources), que são usados por outros módulos ou pelo restante do app, são expostos no arquivo `index.js`. Sempre importe coisas por meio da raíz/root do seu módulo, **nunca quebre esse padrão** importando de partes mais internas do seu módulo, veja na prática:
  ```js
  // Good
  import { MyComponent } from './modules/my-module';
  // Bad
  import MyComponent from './modules/my-module/components/MyComponent'
  ```

* Cada dependência externa usada dentro do módulo deve ser importado do arquivo `dependencies.js` e todo arquivo dentro do módulo deve importar essas dependências de lá. **Malafanculo... sim, vc _mãonafaca_, veja bem... NENHUM outro arquivo, a não ser o `dependencies.js` deve importar coisas de fora do próprio módulo.**
  ```js
  // Good
  import { React } from '../dependecies';
  import Button from '../components/Button';
  // Bad
  import React from 'react';
  ```

Exemplo de estrutura do módulo deve parecer assim, oh:

```
modules/
  |- application/
  |- core/
  |- auth/
   - my-module/
     |- components/
     |- config/
     |- constants/
     |- containers/
     |- services/
       |- sagas/
       |- actionTypes.js
       |- actions.js
       |- reducer.js
        - selectors.js
     |- dependencies.js
      - index.js
```

### Novos módulos

Pra facilitar sua vida... e mais que isso, pra te fazer parecer um dev cheio de habilidades e atalhos... pq usar atalhos sempre te faz parecer f0dd@... esse init disponibilizado tem um comando de script npm (q usa o gerador de códigos [Hygen](https://www.hygen.io) por baixo dos panos) pra você usar, é só rodar:

```bash
npm run create-module app-layout
```

Onde `app-layout` é o nome do módulo que você vai criar. Então veja na pasta `modules` que uma nova pasta foi adicionada: `my-module`.

## Gatsby website (aooouuuuuuaaaaaaaaa)

Melhor do que começar um app do zero, é começar com o Gatsby. Vamo lá, você já tem o  `gatsby-cli` instalado (se não, rode `npm install -g gatsby-cli`), blza... agora rode:

```bash
gatsby new my-website https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Onde `my-website` é tanto o nome do seu site, quanto da pasta que será criada para ele. E esse `https://github.com/gatsbyjs/gatsby-starter-hello-world` é a fonte do repo do seu starter.

Se você for precisar de um site em várias línguas, você vai querer usar [esse starter aqui oh](https://medium.com/@marek.janca/840c27795827), assim seu site será internatialized. Pra isso rode:

```bash
gatsby new my-multi-lang-website https://github.com/AckeeCZ/gatsby-starter-internationalized
```
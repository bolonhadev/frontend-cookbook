# 📚 Bibliotecas e framworks

Essa é a lista do que usamos aqui, (eles, não eu)... A maioria é em React, mas você pode achar diretão no JS tb.

## Lista

 - [Ant design](#ant-design)
 - [Classnames](#classnames)
 - [Cypress](libraries/Cypress.md)
 - [Fela](#fela)
 - [Infinite scroller](#infinite-scroller)
 - [Jest](libraries/Jest.md)
 - [Lodash](#lodash)
 - [MJML](#mjml)
 - [Moment](#moment)
 - [React Intl](#react-intl)
 - [React responsive](#react-responsive)
 - [React router](#react-router)
 - [Recompose](#recompose)
 - [Redux](#redux)
 - [Redux form](#redux-form)
 - [Redux saga](#redux-saga)
 - [Reselect](#reselect)
 - [Scrollbars](#scrollbars)

## Lista e descrição

### Ant design

Uma arquitetura de design (design system) com um monte de elementos/componentes React (React UI components: table, grid, button, navigation, breadcrumb). E pra fazer os forms funcionarem, foi usado o [redux-form-antd](https://www.npmjs.com/package/redux-form-antd) que liga os elementos/componentes do Ant Design ao Redux Form.

https://ant.design/

### Classnames

Mano... vi isso muito no WordPress. Basicamente, é um jeito de você colocar nome de classe de CSS pro seu elemento. Mas daí tem umas paradinhas, umas funções pra dar uma turbinada nisso.

https://github.com/JedWatson/classnames

### Fela

Essa biblioteca JS também é para estilização CSS, tem várias paradinhas tipo você usar variáveis inline no elemento, nomeação de estilos básicos, suporte i18n...

http://fela.js.org/

### Infinite scroller

Rolagem infinita, chaato pra caramba... c vai rolando e vai carregando mais coisas.

https://github.com/CassetteRocks/react-infinite-scroller

### Lodash

Uma biblioteca auxiliar para trabalhar com arrays, numbers, objects, strings... Tem umas funçõezinhas úteis.

https://lodash.com

### MJML

Framework para emails responsivos. Usado por uns caras grandes.

https://mjml.io/

### Moment

Biblioteca para trabalhar com datas e tempos.

http://momentjs.com/

### React Intl

Traduzir e internacionalizar o seu app, inclusive com mudanças monetárias e de datas, com pluralização e os escambau as 4.

https://github.com/yahoo/react-intl

### React responsive

Sá fitaqui é daora q te ajuda nas hora dos responsivo.

https://github.com/contra/react-responsive

### React router

Bagu io de rota, tiu. Todo mundo usa, se tem q se familiarizar com o bâangue, taligado? 
Vai ser conectado com o [redux](https://github.com/supasate/connected-react-router). Pq você vai precisar armazenar alguns estados enquanto vai de um componente a outro.

https://www.npmjs.com/package/react-router

### Recompose

Biblioteca para function component e HOC, esse HOC é tipo isso veja (uma função que atualiza um componente e retorna componente, não dado):

> **const NewComponent** = (**BaseComponent**) => {  
>  // _... create new component from old one and update_  
>  return **UpdatedComponent**  
> }  

https://github.com/acdlite/recompose

### Redux

Administrador de estados, biblioteca bem famosa então melhor se familiarizar com ela.

https://redux.js.org/

### Redux form

Se você usa Redux, provavelmente usa essa biblioteca para gerenciar os forms

https://redux-form.com

### Redux saga

Com o redux saga, você pode manipular seu app de forma assíncrona de forma mais simples: '_simples assim_'... :/

https://redux-saga.js.org/

### Reselect

Criar e combinar seletores que foram [**memoizados**](https://pt.stackoverflow.com/questions/405781/qual-%C3%A9-a-real-diferen%C3%A7a-entre-usememo-e-usecallback) pelo Redux, coisa que esperamos que esteja bem mais clara antes do fim dessa leitura.

https://github.com/reduxjs/reselect

### Scrollbars

Barra de rolagem personalizada.

https://github.com/malte-wessel/react-custom-scrollbars

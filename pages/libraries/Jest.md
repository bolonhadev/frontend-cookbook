# 🤡 Jest

[Jest](https://jestjs.io/) é um framework de teste em JS. Será usado para *testes unitários* de componentes React e complexos seletores Redux.

## Exemplos de testes unitários

### Componentes React

Os testes dos componentes React serão complementados com o [Enzyme](https://airbnb.io/enzyme/), que é uma biblioteca de testes do React.

Neste exemplo, `RatingSimple` é um componente que imprime/renderiza de 0 a 5 estrelas, baseado numa prop `rating`. Também tem dois tamanhos - *normal* e *small*.

```jsx
import React from 'react';
import { shallow } from 'enzyme';

import RatingSimple, { colors } from '../RatingSimple';

describe('RatingSimple', () => {
    it('renders with 0 filled stars', () => {
        const wrapper = shallow(<RatingSimple />);

        expect(wrapper.find('Icon').length).toBe(5);
        expect(wrapper.find({ color: colors.DEFAULT }).length).toBe(5);
    });

    it('renders small', () => {
        const wrapper = shallow(<RatingSimple small />);
        expect(wrapper.find('.rating__stars--small').length).toBe(1);
    });
});
```

### Complexos seletores Redux

Seletores ficam bem complexos, especialmente quando são combinados.

No exemplo abaixo, há um seletor [reselect](https://github.com/reduxjs/reselect) para associar nomes de produtos aos ids de produtos do usuário. *Nota: estamos supondo que não está sendo obtido por uma API neste form.*

```javascript
// selector.js
import { createSelector } from 'reselect';

const user = state => state.user;
const products = state => state.products;

export const userProductsSelector = createSelector(
    user,
    products,
    (user, products) => ({
        ...user,
        productNames: products.filter(product => user.productIds.includes(product.id))
    })
);
```

```javascript
// selector.test.js
import { userProductsSelector } from '../selector.js';

describe('userProducts selector', () => {
    const state = {
        user: { id: 1, name: 'Tomáš Král', productIds: [1, 2] },
        products: [
            { id: 1, name: 'Pen' },
            { id: 2, name: 'Pencil' }
        ]
    }

    it('maps products to ids', () => {
        expect(userProductsSelector(state).toEqual({
            ...state.user,
            productNames: ['Pen', 'Pencil']
        }))
    });
});
```
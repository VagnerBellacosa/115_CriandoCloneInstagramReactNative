# Configurando o React Navigation

Vamos começar instalando o plugin do react-navigation no terminal com seguinte comando:

```
yarn add react-navigation
```

Instale também o `react-native-gesture-handler` que é responsável por lidar com gestos e toques no React Native:

```
yarn add react-native-gesture-handler
```

Como o `react-native-gesture-handler` faz alterações na **source** é necessário você fazer o link:

```
react-native link react-native-gesture-handler
```

## Definindo as páginas

Criaremos duas páginas que serão utilizadas no nosso projeto.

Nossa página Home:

```js
// src/Page1.js

import React from 'react';
import { View, Button, Text } from 'react-native';

const Page1 = ({ navigation }) => (
  <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
    <Text>Home ;D</Text>
    <Button 
      title="Ir para About"
      onPress={() => navigation.navigate('About') }
    />
  </View>
);

Page1.navigationOptions = {
  title: 'Home',
}

export default Page1;
```

Nossa página About:

```js
// src/Page2.js

import React from 'react';
import { View, Button, Text } from 'react-native';

const Page2 = () => (
  <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
    <Text>About</Text>
  </View>
);

Page2.navigationOptions = {
  title: 'About',
}


export default Page2;
```

## Configurando o StackNavigator

Para início de conversa vamos com o StackNavigator.

```js
// src/index.js

import Page1 from './Page1';
import Page2 from './Page2';

import { createAppContainer, createStackNavigator } from 'react-navigation';

const Routes = createAppContainer(
  createStackNavigator({
    Home: Page1,
    About: Page2,
  })
);

export default Routes;
```

## Configurando o index.js

O `index.js` da aplicação ao invés de ler o `App.js` lerá o diretório `src`, pra isso será feita as seguintes alterações:

```js
import { AppRegistry } from "react-native";
import { name as appName } from "./app.json";

import Routes from "./src";

AppRegistry.registerComponent(appName, () => Routes);
```

![img](https://blog.rocketseat.com.br/content/images/2018/12/react-navigation-react-native-gif-01.gif)Resultado da navegação com StackNavigator

OWW, OMG!!! Só isso???

É meu caro, o trem é simples, não disse? E robusto. Um comentário importante é que utilizamos como parâmetro para o `createStackNavigator` um objeto contendo dois itens e que cada chave desse objeto representa uma ***\*rota\****.

Nesse objeto optamos passar o nosso componente stateless direto como `value` da rota, isso se dá porque não definimos nenhuma opção pra ela além do componente. Mas poderíamos muito bem fazer por extenso e passar alguma opção, como segue:

```js
const StackNavigator = createStackNavigator({
  Home: {
    screen: Page1,
    defaultNavigationOptions: {
      title: 'Home',
    },
  },
});
```

Podemos também passas diversas opções para a página através da variável estática `defaultNavigationOptions`; como pode ser observado na criação das páginas, que a princípio mudamos apenas o título do `Header`, porém há outras [opções](https://reactnavigation.org/docs/en/stack-navigator.html#navigationoptions-for-screens-inside-of-the-navigator). AH, e isso vale para os demais ***\*navigators\****.

Por fim, observe que utilizamos o `navigation.navigate` para ir para a próxima página. O que é preciso ressaltar aqui é que referenciamos o nome que estava como ***\*chave\**** (‘About’) para ir para a página e não o nome do componente ***\*Page2\****.

## Configurando o TabNavigator

Nessa hora você deve está pensando: “agora o trem vai azedar” e é ai que você se engana meu amigo, pois o que mudará do StackNavigator é a função `createStackNavigator` e só.

Sobre isso preciso tecer apenas uma observação, o Android e IOS possuem estilos próprios, e para acompanhar isso o React Navigation separou o TabNavigator em duas funções.

A [`createBottomTabNavigator`](https://reactnavigation.org/docs/en/bottom-tab-navigator.html#navigationoptions-for-screens-inside-of-the-navigator), que como você deve imaginar, as abas ficam no rodapé e seguem a estilização do IOS. Já a [`createMaterialTopTabNavigator`](https://reactnavigation.org/docs/en/material-top-tab-navigator.html#navigationoptions-for-screens-inside-of-the-navigator) as abas ficam no topo e seguem a estilização do Material Design do Android.

No exemplo vamos com o `createBottomTabNavigator`:

```js
const Routes = createAppContainer(
  createBottomTabNavigator({
    Home: Page1,
    About: Page2,
  })
);

export default Routes;
```

![img](https://blog.rocketseat.com.br/content/images/2018/12/react-navigation-react-native-gif-02.gif)Resultado da navegação do ***\*TabNavigator\****

É sempre bom lembrar que o que muda é o “nome” da função e podemos passar as configurações e estilizações da mesma maneira já mencionada acima.

Você também pode utilizar as fontes de ícones, da uma olhada nesse [post](https://blog.rocketseat.com.br/utilizando-fontes-de-icones-no-react-native/) que ensinamos a configurar, e deixar bem mais apresentável o seu TabNavigator:

```js
Page1.navigationOptions = {
  tabBarIcon: <Icon name="Home" size={18} color="#999" />
}
```

## Configurando o DrawerNavigator

Por fim, mas não menos importante, o DrawerNavigator como já esperado alteramos apenas uma função e sua navegação está completa, como não amar isso?

Para o DrawerNavigator funcionar corretamente no Android, precisamos fazer uma alteração a mais no arquivo MainActivity.java como esse guia de instalação mostra: https://kmagiera.github.io/react-native-gesture-handler/docs/getting-started.html#android

```js
const Routes = createAppContainer(
  createDrawerNavigator({
    Home: Page1,
    About: Page2,
  })
);

export default Routes;
```

![img](https://blog.rocketseat.com.br/content/images/2018/12/react-navigation-react-native-gif-03.gif)Resultado da navegação do DrawerNavigator

## E por hoje é só…

Bom pessoal, vimos a facilidade que o React Navigation nos trás para criarmos uma navegação completa para nosso App. Existem outras bibliotecas de navegação como é o caso do [react-native-navigation](https://github.com/wix/react-native-navigation) que utiliza módulos nativos e proporciona um ganho de performance, mas que é confusa e burocrática a sua utilização. No momento React Navigation atende e muito bem as nossas necessidades.

Ah, existe a possibilidade de juntar isso tudo e fazer a parada ficar ainda mais legal, quem sabe não abordaremos num próximo Post.

O projeto completo no nosso github: https://github.com/Rocketseat/blog-react-navigation

### Etiquetas

- [react navigation](https://blog.rocketseat.com.br/tag/react-navigation/)
- [React Native](https://blog.rocketseat.com.br/tag/react-native/)
- [react](https://blog.rocketseat.com.br/tag/react/)
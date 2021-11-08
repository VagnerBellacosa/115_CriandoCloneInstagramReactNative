

# React Native: Navegações complexas com React Navigation

[![Eduardo Rabelo](https://miro.medium.com/fit/c/56/56/1*yLyHDumpDQY3fJ1Y0BL28A.jpeg)](https://oieduardorabelo.medium.com/?source=post_page-----583a8f5a4a7-----------------------------------) - [Eduardo Rabelo](https://oieduardorabelo.medium.com/?source=post_page-----583a8f5a4a7-----------------------------------) - [Oct 5, 2019·8 min read](https://oieduardorabelo.medium.com/react-native-navegações-complexas-com-react-navigation-583a8f5a4a7?source=post_page-----583a8f5a4a7-----------------------------------)



![img](https://miro.medium.com/max/2000/1*A4str6z496hI6Qw8BnRJhQ.png)

[Créditos da Imagem](https://unsplash.com/photos/4JdvOwrVzfY)

Descobri que as pessoas podem se intimidar combinando diferentes navegadores no [React Navigation](https://reactnavigation.org/) para obter padrões de navegação mais “complexos”. Hoje, quero guiá-lo brevemente por uma configuração de navegação mais complexa. Iremos falar de:

- O [Switch Navigator](https://reactnavigation.org/docs/en/switch-navigator.html) irá representar nosso status do aplicativo autenticado vs. não autenticado
- [Stack Navigator](https://reactnavigation.org/docs/en/stack-navigator.html) para navegação normal da direita para a esquerda em vários locais (telas de autenticação, pilha para cada aba, etc)
- Stack Navigator para navegação de baixo para cima
- [Tab Navigator](https://reactnavigation.org/docs/en/bottom-tab-navigator.html)
- [Drawer Navigator](https://reactnavigation.org/docs/en/drawer-navigator.html)

# Antes de começar

No tutorial original, [Spencer Carli](https://twitter.com/spencer_carli) **não está usando a última versão do React Navigation**, tomei a liberdade e atualizei os exemplos e irei utilizar versões fixas das dependências. Iremos usar o [**expo-cli**](https://github.com/expo/expo-cli), do mesmo modo que é [recomendado na documentação do React Native](https://facebook.github.io/react-native/docs/0.60/getting-started).

Instale o **expo-cli** globalmente:

```
$ yarn global add expo-cli@3.2.3
```

Criaremos um novo projeto:

```
$ expo init ExemploNavegacoesComplexas
```

Iremos escolher **blank** na tela seguinte:

![img](https://miro.medium.com/max/2000/1*keD7Qe_6xGz3B9If_Bevpg.png)

Navegue até a sua nova pasta:

```
$ cd ExemploNavegacoesComplexas
```

E iremos instalar as dependências necessárias para **React Navigation**:

```
$ expo install react-navigation@4.0.10 react-native-gesture-handler@1.3.0 react-native-reanimated@1.2.0
```

Agora, iremos adicionar os pacotes de navegadores do React Navigation:

```
$ expo install react-navigation-tabs@2.5.5 react-navigation-stack@1.9.3 react-navigation-drawer@2.2.2
```

- **react-navigation-drawer**: Para podermos criar Drawer Navigator.
- **react-navigation-stack**: Para podermos criar Stack Navigator.
- **‌react-navigation-tabs**: Para podermos criar Tab Navigator

E agora podemos iniciar nossa aplicação:

```
$ yarn start
```

Vale notar que os conceitos explicados nesse artigo, podem ser portados para qualquer biblioteca de navegação.

# Pré-requisitos

Antes de começarmos, adicionarei um `Example.js` para servir como uma tela para todas as nossas rotas (afinal, é apenas uma demonstração). Este componente gera uma cor de fundo aleatória e exibe todas as rotas disponíveis na tela atual:

```
// Example.js
import React from 'react';
import { View, TouchableOpacity, Text } from 'react-native';

const getAvailableRoutes = navigation => {
  let availableRoutes = [];
  if (!navigation) return availableRoutes;

  const parent = navigation.dangerouslyGetParent();
  if (parent) {
    if (parent.router && parent.router.childRouters) {
      // Grab all the routes the parent defines and add it the list
      availableRoutes = [
        ...availableRoutes,
        ...Object.keys(parent.router.childRouters),
      ];
    }

    // Recursively work up the tree until there are none left
    availableRoutes = [...availableRoutes, ...getAvailableRoutes(parent)];
  }

  // De-dupe the list and then remove the current route from the list
  return [...new Set(availableRoutes)].filter(
    route => route !== navigation.state.routeName
  );
};

const getRandomColor = () => {
  var letters = '0123456789ABCDEF';
  var color = '#';
  for (var i = 0; i < 6; i++) {
    color += letters[Math.floor(Math.random() * 16)];
  }
  return color;
};

const Example = ({ navigation }) => {
  return (
    <View
      style={{
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
        backgroundColor: getRandomColor(),
      }}
    >
      {getAvailableRoutes(navigation).map(route => (
        <TouchableOpacity
          onPress={() => navigation.navigate(route)}
          key={route}
          style={{
            backgroundColor: '#fff',
            padding: 10,
            margin: 10,
          }}
        >
          <Text>{route}</Text>
        </TouchableOpacity>
      ))}
    </View>
  );
};

export default Example;
```

Com isso feito, vamos começar.

# Switch Navigator

Para alternar entre os diferentes “estados” da jornada de um usuário, usaremos um navegador switch para que o usuário não possa voltar atrás. Obviamente, teremos uma tela para a jornada principal do aplicativo. Também teremos um para usuários não autenticados.

Além disso, gosto de adicionar uma espécie de tela de `Loading`. Normalmente, isso não exibe nada - ela serve apenas para determinar se um usuário está autenticado ou não e encaminhá-lo para o lugar certo.

![img](https://miro.medium.com/freeze/max/30/0*nDaQkaBE2ONLR4rp.gif?q=20)

![img]()

```
// App.js
import React from 'react';
import {
  createAppContainer,
  createSwitchNavigator,
} from 'react-navigation';
import { createBottomTabNavigator } from 'react-navigation-tabs';
import { createDrawerNavigator } from 'react-navigation-drawer';
import { createStackNavigator } from 'react-navigation-stack';

import Example from './Example';

const App = createSwitchNavigator({
  Loading: {
    screen: Example,
  },
  Auth: {
    screen: Example,
  },
  App: {
    screen: Example,
  },
});

export default createAppContainer(App);
```

# Stack Navigator de autenticação

Se um usuário não estiver autenticado, configuraremos um Stack Navigator para que ele saia de uma tela de início, entre, crie uma conta, esqueça a senha ou redefina a senha. As opções típicas que você vê quando precisa se autenticar.

![img](https://miro.medium.com/freeze/max/30/0*4JINOrW4yeNyWJue.gif?q=20)

![img]()

```
// App.js

// ...

const AuthStack = createStackNavigator({
  Landing: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Landing',
    },
  },
  SignIn: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Sign In',
    },
  },
  CreateAccount: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Create Account',
    },
  },
  ForgotPassword: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Forgot Password',
    },
  },
  ResetPassword: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Reset Password',
    },
  },
});

const App = createSwitchNavigator({
  Loading: {
    screen: Example,
  },
  Auth: {
    screen: AuthStack,
  },
  App: {
    screen: Example,
  },
});

export default createAppContainer(App);
```

# App Tabs

Quando o usuário estiver no aplicativo, usaremos guias para permitir que ele acesse os principais recursos do aplicativo — um feed, pesquisa e uma página de descobertas. Em seguida, substituiremos o item `App` em nosso navegador `App` pelo resultado da criação de nossas guias.

A saída da criação de qualquer navegador é apenas um componente para que possamos aninhá-los infinitamente no React Navigation.

![img](https://miro.medium.com/freeze/max/30/0*LicU0W7FS0ZS4pe3.gif?q=20)

![img]()

```
// App.js

// ...

const MainTabs = createBottomTabNavigator({
  Feed: {
    screen: Example,
    navigationOptions: {
      tabBarLabel: 'Feed',
    },
  },
  Search: {
    screen: Example,
    navigationOptions: {
      tabBarLabel: 'Search',
    },
  },
  Discover: {
    screen: Example,
    navigationOptions: {
      tabBarLabel: 'Discover',
    },
  },
});

const App = createSwitchNavigator({
  Loading: {
    screen: Example,
  },
  Auth: {
    screen: AuthStack,
  },
  App: {
    screen: MainTabs,
  },
});

// ...
```

# Stack Navigator para cada guia do App Tab

Assim como aninhamos o `MainTabs` em nosso navegador `App`, permitiremos que cada guia em nosso aplicativo tenha seu próprio **stack navigator**. Fazendo isso, significa que cada guia terá seu próprio estado, para que o usuário possa ir para a tela de detalhes de uma guia, mudar para outra e, ao voltar, poderá manter o mesmo estado para cada guia.

Além disso, com este exemplo, você pode ver que os navegadores obterão o nome da rota correspondente mais próxima. Isso significa que podemos reutilizar os nomes de tela e cada pilha apenas captura a tela `Details` mais próxima disponível, na pilha ou acima dela, na hierarquia do navegador.

![img](https://miro.medium.com/freeze/max/30/0*PWbiw_1QV1j0a_Oa.gif?q=20)

![img]()

```
// App.js

// ...

const FeedStack = createStackNavigator({
  Feed: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Feed',
    },
  },
  Details: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Details',
    },
  },
});

const SearchStack = createStackNavigator({
  Search: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Search',
    },
  },
  Details: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Details',
    },
  },
});

const DiscoverStack = createStackNavigator({
  Discover: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Discover',
    },
  },
  Details: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Details',
    },
  },
});

const MainTabs = createBottomTabNavigator({
  Feed: {
    screen: FeedStack,
    navigationOptions: {
      tabBarLabel: 'Feed',
    },
  },
  Search: {
    screen: SearchStack,
    navigationOptions: {
      tabBarLabel: 'Search',
    },
  },
  Discover: {
    screen: DiscoverStack,
    navigationOptions: {
      tabBarLabel: 'Discover',
    },
  },
});

// ...
```

# App Drawer

Faremos o mesmo com o Drawer Navigator. Criaremos o navegador (também criaremos uma pilha para tela de configurações, dando um motivo criarmos o drawer) e renderizaremos isso como uma tela.

Desta vez, vamos substituir a renderização de `MainTabs` com `MainDrawer` e tornaremos nossas guias dentro do drawer. Construir essa hierarquia significa que estamos apenas adicionando mais navegadores, mas tudo o que já estava lá continuará funcionando.

![img](https://miro.medium.com/freeze/max/30/0*laQegm33tzoYrRKY.gif?q=20)

![img]()

```
// App.js

// ...

const SettingsStack = createStackNavigator({
  SettingsList: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Settings List',
    },
  },
  Profile: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Profile',
    },
  },
});

const MainDrawer = createDrawerNavigator({
  MainTabs: MainTabs,
  Settings: SettingsStack,
});

const App = createSwitchNavigator({
  Loading: {
    screen: Example,
  },
  Auth: {
    screen: AuthStack,
  },
  App: {
    screen: MainDrawer,
  },
});

// ...
```

# Stack Navigator no estilo modal

Finalmente, queremos adicionar um navegador que se mova de baixo para cima e cubra qualquer outra tela. Isso significa que ele precisa estar na posição mais alta da nossa pilha (raiz/root). Se estiver na raiz, estará disponível para ser renderizado a partir de qualquer um de seus filhos.

![img](https://miro.medium.com/freeze/max/30/0*aFDOUbldAtdP5v24.gif?q=20)

![img]()

```
// App.js

// ...

const AppModalStack = createStackNavigator(
  {
    App: MainDrawer,
    Promotion1: {
      screen: Example,
    },
  },
  {
    mode: 'modal',
    headerMode: 'none',
  }
);

const App = createSwitchNavigator({
  Loading: {
    screen: Example,
  },
  Auth: {
    screen: AuthStack,
  },
  App: {
    screen: AppModalStack,
  },
});

export default createAppContainer(App);
```

# Código final do nosso navegador

E para finalizar, aqui está o nosso código ao final desse tutorial:

```
import React from 'react';
import {
  createAppContainer,
  createSwitchNavigator,
} from 'react-navigation';
import { createBottomTabNavigator } from 'react-navigation-tabs';
import { createDrawerNavigator } from 'react-navigation-drawer';
import { createStackNavigator } from 'react-navigation-stack';

import Example from './Example';

const AuthStack = createStackNavigator({
  Landing: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Landing',
    },
  },
  SignIn: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Sign In',
    },
  },
  CreateAccount: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Create Account',
    },
  },
  ForgotPassword: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Forgot Password',
    },
  },
  ResetPassword: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Reset Password',
    },
  },
});

const FeedStack = createStackNavigator({
  Feed: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Feed',
    },
  },
  Details: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Details',
    },
  },
});

const SearchStack = createStackNavigator({
  Search: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Search',
    },
  },
  Details: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Details',
    },
  },
});

const DiscoverStack = createStackNavigator({
  Discover: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Discover',
    },
  },
  Details: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Details',
    },
  },
});

const MainTabs = createBottomTabNavigator({
  Feed: {
    screen: FeedStack,
    navigationOptions: {
      tabBarLabel: 'Feed',
    },
  },
  Search: {
    screen: SearchStack,
    navigationOptions: {
      tabBarLabel: 'Search',
    },
  },
  Discover: {
    screen: DiscoverStack,
    navigationOptions: {
      tabBarLabel: 'Discover',
    },
  },
});

const SettingsStack = createStackNavigator({
  SettingsList: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Settings List',
    },
  },
  Profile: {
    screen: Example,
    navigationOptions: {
      headerTitle: 'Profile',
    },
  },
});

const MainDrawer = createDrawerNavigator({
  MainTabs: MainTabs,
  Settings: SettingsStack,
});

const AppModalStack = createStackNavigator(
  {
    App: MainDrawer,
    Promotion1: {
      screen: Example,
    },
  },
  {
    mode: 'modal',
    headerMode: 'none',
  }
);

const App = createSwitchNavigator({
  Loading: {
    screen: Example,
  },
  Auth: {
    screen: AuthStack,
  },
  App: {
    screen: AppModalStack,
  },
});

export default createAppContainer(App);
```

Você pode encontrar o código final [nesse repositório no GitHub.](https://github.com/oieduardorabelo/react-native-complex-navigation-with-react-navigation) Aproveitei e separei cada exemplo em um commit separado, para você poder ver o que mudou em cada etapa.

[oieduardorabelo/react-native-complex-navigation-with-react-navigationYou can't perform that action at this time. You signed in with another tab or window. You signed out in another tab or…github.com](https://github.com/oieduardorabelo/react-native-complex-navigation-with-react-navigation)

# Créditos

- [Complex Navigation Example with React Navigation](https://www.reactnativeschool.com/complex-navigation-example-with-react-navigation), escrito originalmente por [Spencer Carli](https://twitter.com/spencer_carli)

[Eduardo Rabelo](https://oieduardorabelo.medium.com/?source=post_sidebar--------------------------post_sidebar--------------)

☕🇳🇿 - [https://eduardorabelo.me](https://eduardorabelo.me/)



- [React](https://medium.com/tag/react)
- [React Native](https://medium.com/tag/react-native)
- [React Navigation](https://medium.com/tag/react-navigation)
- [Web Development](https://medium.com/tag/web-development)
- [Programming](https://medium.com/tag/programming)

https://policy.medium.com/medium-terms-of-service-9db0094a1e0f?source=post_page-----583a8f5a4a7-----------------------------------)
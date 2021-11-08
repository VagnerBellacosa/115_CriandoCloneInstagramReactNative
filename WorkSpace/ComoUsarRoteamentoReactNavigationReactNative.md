# Como usar o roteamento com React Navigation no React Native

[React](https://www.digitalocean.com/community/tags/react)



### Introdução

[React Navigation](https://reactnavigation.org/) é uma biblioteca popular para roteamento e navegação em uma aplicação [React Native](https://facebook.github.io/react-native/).

Essa biblioteca ajuda a resolver o problema de navegar entre várias telas e compartilhar dados entre elas.

Ao final deste tutorial, teremos uma rede social rudimentar. Ela irá exibir o número de conexões que um usuário possui e fornecer uma maneira de se conectar com amigos adicionais. Usaremos este aplicativo de exemplo para explorar como navegar por telas de aplicativos móveis usando `react-navigation`.

## Pré-requisitos

Para completar este tutorial, será necessário:

- Um ambiente de desenvolvimento local para o Node.js. Siga [How to Install Node.js and Create a Local Development Environment](https://www.digitalocean.com/community/tutorial_series/how-to-install-node-js-and-create-a-local-development-environment).
- Familiaridade com a configuração de seu ambiente para criar um novo projeto React Native e usar os simuladores iOS ou Android pode ajudar.

**Nota:** se você trabalhou com `react-navigation` no passado, poderá encontrar algumas diferenças. Consulte a documentação para guias sobre [como migrar a partir do 3.x](https://reactnavigation.org/docs/4.x/upgrading-from-3.x/) e [como migrar a partir do 4.x](https://reactnavigation.org/docs/upgrading-from-4.x/).

Este tutorial foi testado com o Node v14.7.0, `npm` v6.14.7, `react` v16.13.1, `react-native` v0.63.2, `@react-navigation/native` v5.7.3 e `@react-navigation/stack` v5.9.0.

## Passo 1 — Criando um novo aplicativo React Native

Primeiro, crie um novo aplicativo React Native executando o seguinte comando em seu terminal:

```bash
npx react-native init MySocialNetwork --version 0.63.2
```

 

Copy

Em seguida, navegue até o novo diretório:

```bash
cd MySocialNetwork
```

 

Copy

E inicie o aplicativo para o iOS:

```bash
npm run ios
```

 

Copy

Alternativamente, para o Android:

```bash
npm run android
```

 

Copy

**Nota:** se tiver quaisquer problemas, consulte [troubleshooting issues for React Native CLI](https://reactnative.dev/docs/environment-setup).

Isso irá criar um esqueleto de projeto.para você. Isso não se parece com uma rede social neste momento. Vamos corrigir isso.

Abra o `App.js`:

```bash
nano App.js
```

 

Copy

Substitua o conteúdo de `App.js` pelo código a seguir para exibir uma mensagem de boas-vindas:

App.js

```jsx
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Welcome to MySocialNetwork!</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});

export default App;
```

 

Copy

Salve o arquivo. Agora, ao executar o aplicativo, uma mensagem **Welcome to MySocialNetwork!** aparecerá em seu simulador.

No próximo passo, você irá adicionar mais telas ao seu aplicativo.

## Passo 2 — Criando as telas `HomeScreen` e `FriendsScreen`

Atualmente, você possui uma única tela exibindo uma mensagem de boas-vindas. Neste passo, você irá criar as duas telas para o seu aplicativo: `HomeScreen` e `FriendsScreen`.

### `HomeScreen`

Seu aplicativo precisará de uma tela `HomeScreen`. `HomeScreen` irá exibir o número de amigos que já estão em sua rede.

Pegue o código de `App.js` e adicione-o a um novo arquivo chamado `HomeScreen.js`:

```bash
cp App.js HomeScreen.js
```

 

Copy

Abra o `HomeScreen.js`:

```bash
nano HomeScreen.js
```

 

Copy

Modifique `HomeScreen.js` para usar `HomeScreen` em vez de `App`:

HomeScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

class HomeScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>You have (undefined) friends.</Text>
      </View>
    );
  }
}

// ...

export default HomeScreen;
```

 

Copy

Esse código irá produzir um placeholder de mensagem **You have (undefined) friends.** Você fornecerá um valor mais tarde.

### `FriendsScreen`

Seu aplicativo também precisará de uma tela `FriendsScreen`. Em `FriendsScreen` você será capaz de adicionar novos amigos.

Pegue o código de `App.js` e adicione-o a um novo arquivo chamado `FriendScreen.js`:

```bash
cp App.js FriendsScreen.js
```

 

Copy

Abra o `FriendsScreen.js`:

```bash
nano FriendsScreen.js
```

 

Copy

Modifique `FriendScreen.js` para usar `FriendScreen` em vez de `App`:

FriendsScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

class FriendsScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Add friends here!</Text>
      </View>
    );
  }
}

// ...

export default FriendsScreen;
```

 

Copy

Esse código irá produzir um **Add friends here!** como mensagem.

Neste ponto, você tem as telas `HomeScreen` e `FriendsScreen`. No entanto, não há nenhuma maneira de navegar entre elas. Você criará essa funcionalidade no próximo passo.

## Passo 3 — Usando `StackNavigator` com React Navigation

Para navegar entre telas, você usará um `StackNavigator`. Um `StackNavigator` funciona exatamente como uma [pilha de chamada](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)). Cada tela que você navegar é enviada para o topo da pilha. Cada vez que você pressiona o botão voltar, as telas saem do topo da pilha.

Primeiro, instale `@react-navigation/native`:

```bash
npm install @react-navigation/native@5.7.3
```

 

Copy

Em seguida, instale o `@react-navigation/stack` e suas respectivas dependências:

```bash
npm install @react-navigation/stack@5.9.0 @react-native-community/masked-view@0.1.10 react-native-screens@2.10.1 react-native-safe-area-context@3.1.4 react-native-gesture-handler@1.7.0
```

 

Copy

**Nota:** se você estiver desenvolvendo para iOS, é necessário navegar até o diretório `ios` e executar `pod install`.

Em seguida, revisite o `App.js`:

```bash
nano App.js
```

 

Copy

Adicione `NavigationContainer` e `createStackNavigator` ao `App.js`:

App.js

```jsx
import 'react-native-gesture-handler';
import React from 'react';
import { StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';

const Stack = createStackNavigator();
```

 

Copy

Em seguida, substitua o conteúdo de `render`:

App.js

```jsx
// ...

class App extends React.Component {
  render() {
    return (
      <NavigationContainer>
        <Stack.Navigator>
        </Stack.Navigator>
      </NavigationContainer>
    );
  }
}

// ...
```

 

Copy

Aninhado dentro de `<Stack.Navigator>`, adicione `HomeScreen`:

App.js

```jsx
import 'react-native-gesture-handler';
import React from 'react';
import { StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen';

const Stack = createStackNavigator();

class App extends React.Component {
  render() {
    return (
      <NavigationContainer>
        <Stack.Navigator>
          <Stack.Screen
            name="Home"
            component={HomeScreen}
          />
        </Stack.Navigator>
      </NavigationContainer>
    );
  }
}

// ...
```

 

Copy

Esse código cria uma pilha muito pequena para o seu navigator com apenas uma tela: `HomeScreen`.

Aninhado dentro de `<Stack.Navigator>`, adicione `FriendsScreen`:

App.js

```jsx
import 'react-native-gesture-handler';
import React from 'react';
import { StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen';
import FriendsScreen from './FriendsScreen';

const Stack = createStackNavigator();

class App extends React.Component {
  render() {
    return (
      <NavigationContainer>
        <Stack.Navigator>
          <Stack.Screen
            name="Home"
            component={HomeScreen}
          />
          <Stack.Screen
            name="Friends"
            component={FriendsScreen}
          />
        </Stack.Navigator>
      </NavigationContainer>
    );
  }
}

// ...
```

 

Copy

Esse código adiciona a `FriendsScreen` ao navigator.

**Nota:** isso difere de como `createStackNavigator` foi usado em versões anteriores do React Navigation.

Agora, o navigator está ciente de suas duas telas.

### Adicionando botões à `HomeScreen` e `FriendsScreen`

Finalmente, adicione botões para alternar entre as duas telas.

Em `HomeScreen.js`, adicione o seguinte código:

HomeScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';

class HomeScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>You have (undefined) friends.</Text>

        <Button
          title="Add some friends"
          onPress={() =>
            this.props.navigation.navigate('Friends')
          }
        />
      </View>
    );
  }
}

// ...
```

 

Copy

Em `FriendsScreen.js`, adicione o seguinte código:

FriendsScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';

class FriendsScreen extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Add friends here!</Text>

        <Button
          title="Back to home"
          onPress={() =>
            this.props.navigation.navigate('Home')
          }
        />
      </View>
    );
  }
}

// ...
```

 

Copy

Vamos falar sobre `this.props.navigation`. Uma vez que sua tela esteja incluída no `StackNavigator`, ela herda automaticamente muitas propriedades úteis do objeto `navigation`. Neste caso, você usou `navigate` para mover-se para uma página diferente.

![HomeScreen e FriendsScreen](https://assets.digitalocean.com/articles/react-react-native-navigation/1.png)

Se você abrir seu simulador agora, poderá navegar entre `HomeScreen` e `FriendsScreen`.

## Passo 4 — Usando `Context` para passar dados para outras telas

Neste passo, você criará um array de possíveis amigos — `Alice`, `Bob` e `Sammy` — e um array vazio de amigos atuais. Você também criará funcionalidade para que o usuário adicione possíveis amigos aos seus amigos atuais.

Abra `App.js`:

```bash
nano App.js
```

 

Copy

Adicione `possibleFriends` e `currentFriends` ao estado do componente:

App.js

```jsx
// ...

class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      possibleFriends: [
        'Alice',
        'Bob',
        'Sammy',
      ],
      currentFriends: [],
    }
  }

  // ...
}

// ...
```

 

Copy

Em seguida, adicione uma função para mover um possível amigo para a lista de amigos atuais:

App.js

```jsx
// ...

class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      possibleFriends: [
        'Alice',
        'Bob',
        'Sammy',
      ],
      currentFriends: [],
    }
  }

  addFriend = (index) => {
    const {
      currentFriends,
      possibleFriends,
    } = this.state

    // Pull friend out of possibleFriends
    const addedFriend = possibleFriends.splice(index, 1)

    // And put friend in currentFriends
    currentFriends.push(addedFriend)

    // Finally, update the app state
    this.setState({
      currentFriends,
      possibleFriends,
    })
  }

  // ...
}

// ...
```

 

Copy

Neste ponto, terminamos de criar a funcionalidade para adicionar amigos.

### Adicionando `FriendsContext` ao `App`

Agora, você pode adicionar amigos em `App.js`, mas você desejará adicioná-los ao `FriendsScreen.js` e exibí-los em `HomeScreen.js`. Como este projeto é construído com React, é possível injetar essa funcionalidade em suas telas com contexto.

**Nota:** em versões anteriores do React Navigation, era possível usar `screenProps` para compartilhar dados entre telas. Na versão atual do React Navigation, recomenda-se usar [React Context](https://www.digitalocean.com/community/tutorials/react-context-api) para compartilhar dados entre telas.

Para evitar uma referência circular, você desejará um novo arquivo `FriendsContext`:

```bash
nano FriendsContext.js
```

 

Copy

Exporte `FriendsContext`:

FriendsContext

```jsx
import React from 'react';

export const FriendsContext = React.createContext();
```

 

Copy

Abra `App.js`:

```bash
nano App.js
```

 

Copy

Adicione o `FriendsContext`:

App.js

```jsx
import 'react-native-gesture-handler';
import React from 'react';
import { StyleSheet } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { FriendsContext } from './FriendsContext';
import Home from './Home';
import Friends from './Friends';

const Stack = createStackNavigator();

class App extends React.Component {
  // ...

  render() {
    return (
      <FriendsContext.Provider>
        <NavigationContainer>
          <Stack.Navigator>
            <Stack.Screen
              name="Home"
              component={Home}
            />
            <Stack.Screen
              name="Friends"
              component={Friends}
            />
          </Stack.Navigator>
        </NavigationContainer>
      </FriendsContext.Provider>
    );
  }
}

// ...
```

 

Copy

Esse código estabelece `FriendsContext` como um novo [objeto `Context`](https://reactjs.org/docs/context.html) e encapsula o `NavigationContainer` em um componente `Context.Provider` para que qualquer filho na árvore de componentes possa se inscrever para mudanças de contexto.

Como você não está usando `View` ou `Text`, é possível remover essas importações do `react-native`.

Você precisará fornecer um `value` para tornar os dados acessíveis pelos consumidores:

App.js

```jsx
// ...

class App extends React.Component {
  // ...

  render() {
    return (
      <FriendsContext.Provider
        value={
          {
            currentFriends: this.state.currentFriends,
            possibleFriends: this.state.possibleFriends,
            addFriend: this.addFriend
          }
        }
      >
        <NavigationContainer>
          <Stack.Navigator>
            <Stack.Screen
              name="Home"
              component={Home}
            />
            <Stack.Screen
              name="Friends"
              component={Friends}
            />
          </Stack.Navigator>
        </NavigationContainer>
      </FriendsContext.Provider>
    );
  }
}

// ...
```

 

Copy

Isso permitirá que `HomeScreen` e `FriendsScreen` façam referência a qualquer alteração de contexto para `currentFriends` e `possibleFriends`.

Agora, você pode trabalhar fazendo referência ao contexto em suas telas.

### Adicionando `FriendsContext` à `HomeScreen`

Neste passo, você irá configurar o aplicativo para exibir a contagem atual de amigos.

Abra o `HomeScreen.js`:

```bash
nano HomeScreen.js
```

 

Copy

E adicione o `FriendsContext`:

HomeScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';
import { FriendsContext } from './FriendsContext';

class HomeScreen extends React.Component {
  // ...
}
HomeScreen.contextType = FriendsContext;

// ...
```

 

Copy

Esse código estabelece um [`Class.contextType`](https://reactjs.org/docs/context.html#classcontexttype). Agora, você pode acessar contexto em suas telas.

Por exemplo, vamos fazer com que sua `HomeScreen` exiba quantos `currentFriends` você tem:

HomeScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';
import { FriendsContext } from './FriendsContext';

class Home extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>You have { this.context.currentFriends.length } friends!</Text>

        <Button
          title="Add some friends"
          onPress={() =>
            this.props.navigation.navigate('Friends')
          }
        />
      </View>
    );
  }
}
HomeScreen.contextType = FriendsContext;

// ...
```

 

Copy

Se você abrir seu aplicativo novamente no simulador e visualizar a `HomeScreen`, você verá a mensagem: **You have 0 friends!**.

### Adicionando `FriendsContext` à `FriendsScreen`

Neste passo, você irá configurar o aplicativo para exibir os possíveis amigos e fornecer botões para adicioná-los aos amigos atuais.

Em seguida, abra o `FriendsScreen.js`:

```bash
nano FriendsScreen.js
```

 

Copy

E adicione o `FriendsContext`:

FriendsScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';
import { FriendsContext } from './FriendsContext';

class FriendsScreen extends React.Component {
  // ...
}
FriendsScreen.contextType = FriendsContext;

// ...
```

 

Copy

Esse código estabelece um `Class.contextType`.

Agora, crie um botão para adicionar amigos em `FriendsScreen.js`:

FriendsScreen.js

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button } from 'react-native';
import { FriendsContext } from './FriendsContext';

class Friends extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Add friends here!</Text>

        {
          this.context.possibleFriends.map((friend, index) => (
            <Button
              key={ friend }
              title={ `Add ${ friend }` }
              onPress={() =>
                this.context.addFriend(index)
              }
            />
          ))
        }

        <Button
          title="Back to home"
          onPress={() =>
            this.props.navigation.navigate('Home')
          }
        />
      </View>
    );
  }
}
FriendsScreen.contextType = FriendsContext;

// ...
```

 

Copy

Se você abrir seu aplicativo novamente no simulador e visualizar a `FriendsScreen`, você verá uma lista de amigos a adicionar.

![HomeScreen com 0 currentFriends e FriendScreen com 3 possibleFriends](https://assets.digitalocean.com/articles/react-react-native-navigation/2.png)

Se você visitar a `FriendsScreen` e clicar no botão para adicionar amigos, verá a lista de `possibleFriends` diminuir. Se você visitar `HomeScreen`, você verá o número de amigos crescer.

Agora, você pode navegar entre telas e compartilhar dados entre elas.

## Conclusão

Neste tutorial, criamos um exemplo de aplicativo React Native com várias telas. Usando React Navigation, criamos uma maneira de navegar entre telas. Usando React Context, desenvolvemos uma maneira de compartilhar dados entre telas.

O [código fonte completo para este projeto está disponível no GitHub](https://github.com/do-community/MySocialNetwork).

Se você quiser mergulhar mais profundamente no React Navigation, confira [sua documentação](https://reactnavigation.org/docs/en/getting-started.html).

React Navigation não é a única solução de roteamento e navegação. Há também [React Native Navigation](https://wix.github.io/react-native-navigation/), [React Native Router Flux](https://github.com/aksonov/react-native-router-flux), e [React Router Native](https://reactrouter.com/native/guides/quick-start).

Se quiser aprender mais sobre o React, dê uma olhada em nossa série [Como programar no React.js](https://www.digitalocean.com/community/tutorial_series/how-to-code-in-react-js), ou confira [nossa página do tópico React](https://www.digitalocean.com/community/tags/react) para exercícios e projetos de programação
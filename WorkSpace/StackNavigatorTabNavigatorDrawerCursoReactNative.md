

## [![OneBitCode](https://onebitcode.com/wp-content/uploads/2020/12/logo-obc-2021-darkbg.png)](https://onebitcode.com/)

# Navegação (StackNavigator, TabNavigator e Drawer) – Aula 7 | Curso React Native (aprendiz)

![img](https://onebitcode.com/wp-content/uploads/2021/05/Slide1Capa1-1.png)

### **Parte 1**



------

### **Parte 2**



------

### **Parte 3**



------

## 

## **Aprendendo sobre navegação no React Native**


Nesta aula vamos aprender como trabalhar com navegação dentro do React Native. Vamos utilizar o react navigation.

Após criar o projeto com expo init, dentro da pasta do projeto, vamos precisar instalar o react navigation/native:





Default

| 1    | npm install @react-navigation/native |
| ---- | ------------------------------------ |
|      |                                      |




Vamos precisar também, instalar o StackNavigation.





Default

| 1    | npm install @react-navigation/stack |
| ---- | ----------------------------------- |
|      |                                     |




Vamos instalar o Drawer Navigation.





Default

| 1    | npm install @react-navigation/drawer |
| ---- | ------------------------------------ |
|      |                                      |




E instalar também o Tabs navigation.





Default

| 1    | npm install @react-navigation/bottom-tabs |
| ---- | ----------------------------------------- |
|      |                                           |




O próximo passo é instalar as dependências que um projeto que utiliza o expo como gerenciador necessita, conforme podemos ver na documentação do React Navigation.





Default

| 1    | expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view |
| ---- | ------------------------------------------------------------ |
|      |                                                              |




Com tudo instalado vamos dar o start no nosso projeto e entender como configurar as navegações dentro do React Native.
Vamos startar nosso projeto:





Default

| 1    | npm start |
| ---- | --------- |
|      |           |




Vamos criar uma estrutura de pastas para ter nossos pages que serão chamados:





Default

| 123456 | src..pages....Contacts......index.js....Information......index.js |
| ------ | ------------------------------------------------------------ |
|        |                                                              |



## ** App.js – Construindo nosso App.js**

1° – Vamos importar o NavigationContainer e o createStackNavigator





Default

| 1234 | import React from 'react' import { NavigationContainer } from '@react-navigation/native'import { createStackNavigator } from '@react-navigation/stack' |
| ---- | ------------------------------------------------------------ |
|      |                                                              |




2° – Depois importar nossas páginas​





Default

| 12   | import Contatos from './src/components/Contatos/'import Details from './src/components/Details/' |
| ---- | ------------------------------------------------------------ |
|      |                                                              |

 

3° – Para podermos trabalhar com o Stack navigation vamos criar uma const para facilitar na hora de utilizar.





Default

| 1    | const Stack = createStackNavigator(); |
| ---- | ------------------------------------- |
|      |                                       |




4° E por ultimo vamos construir o return do nosso component App.





Default

| 12345678910 | export default function App() { return (  <NavigationContainer>   <Stack.Navigator >{*/\* DICA \*/*}    <Stack.Screen name="Contacts" component={Contacts}/>    <Stack.Screen name="Information" component={Information}/>   </Stack.Navigator>  </NavigationContainer> );} |
| ----------- | ------------------------------------------------------------ |
|             |                                                              |



### ** DICA**

Aqui podemos passar qual o componente vai iniciar a aplicação.





Default

| 1    | <Stack.Navigator initialRouteName="Information"> |
| ---- | ------------------------------------------------ |
|      |                                                  |



Podemos criar uma pagina simples para poder testar nossa navegação.

###  **PAGE CONTACTS**

Para conseguir navegar entre as páginas, o react navigation permite a navegação através do navigation.navigate(“NOME-DA-PAGE”) utilizando essa expressão dentro de um onPress





Default

| 123456789101112 | import React from 'react';import { Text, View } from 'react-native'; export default function Contacts({navigation}) { return (  <View style={{marginTop:60}}> 		  <Text    onPress={()=> navigation.navigate('Information')}     >Information...</Text>  </View> );} |
| --------------- | ------------------------------------------------------------ |
|                 |                                                              |



###  **PAGE Details**





Default

| 12345678910 | import React from 'react';import { Text, View } from 'react-native'; export default function Information() { return (  <View style={{marginTop:60}}> 				<Text>Information</Text>  </View> );} |
| ----------- | ------------------------------------------------------------ |
|             |                                                              |

**Implementando o Drawer Navigation**

O Drawer Navigation tem como padrão a navegação com um estilo um pouco diferente, podemos passar o dedo sobre a tela arrastando da esquerda para a direita, exibindo assim o menu lateral.

E para ver funcionando, podemos aproveitar parte do que criamos somente trocando o estilo de navegação de Stack Navigation para Drawer e assim ver funcionando nosso Drawer Navigation.

 

O primeiro passo então é selecionar todos os Stacks e substituir para Drawer e somente deixar em minúsculo o caminho do import do Drawer

O código ficará assim:





Default

| 12345678910111213141516171819202122 | import React from 'react';import { createDrawerNavigator } from '@react-navigation/drawer';import { NavigationContainer } from '@react-navigation/native'; import Contacts from './src/pages/Contacts/'import Details from './src/pages/About/' const Drawer = createDrawerNavigator(); export default function App() { return (   <NavigationContainer>    <Drawer.Navigator>     <Drawer.Screen name="Contacts" component={Contacts}/>     <Drawer.Screen name="Information" component={Information}/>    </Drawer.Navigator>   </NavigationContainer> ) );} |
| ----------------------------------- | ------------------------------------------------------------ |
|                                     |                                                              |



###  **PAGE CONTACTS**





Default

| 1234567891011121314151617181920 | export default function Contacts({navigation}) { return (  <View style={{marginTop:60}}>   <View>    <Text>Nome: João Botelho</Text>     <Text>Telefone: (11) 93300-8587</Text>    <Text    onPress={()=> navigation.navigate('Information')}    >Information...</Text>   </View>   <View>    <Text>Nome: João Botelho</Text>     <Text>Telefone: (11) 93300-8587</Text>    <Text    onPress={()=> navigation.navigate('Information')}    >Information...</Text>   </View>  </View> );} |
| ------------------------------- | ------------------------------------------------------------ |
|                                 |                                                              |



###  **PAGE DETAILS**





Default

| 123456789101112131415 | import React from 'react';import { Text, View } from 'react-native'; export default function Information() { return (  <View >   <Text>Nome: João Botelho</Text>   <Text>Telefone: (11) 93300-8587</Text>   <Text>Endereço: Rua das araucarias</Text>   <Text>N°: 1759</Text>   <Text>Profissão: Carpinteiro</Text>   <Text>Email: joaobotelho@carpintariabotelho.com.br</Text>  </View> );} |
| --------------------- | ------------------------------------------------------------ |
|                       |                                                              |



Assim podemos utilizar o Drawer Navigation dentro do nosso app e você pode escolher qual a melhor navegação para o seu app.

Agora veremos um pouco sobre como passar propriedades de uma tela para outra dentro do React Navigation.

##  **Como passar propriedades através dos links de navegação?**

Podemos passar parâmetros de uma tela para outra, através do onPress utilizando o navigation.navigate(‘Details’, { nome: “Joao” }).

Em Contacts:





Default

| 1234567891011121314151617181920212223242526272829303132 | <View>    <Text>Nome: João Botelho</Text>     <Text>Telefone: (11) 93300-8587</Text>    <Text    onPress={()=> navigation.navigate('Information',     {     nome:'João Augusto',     telefone:'(11)98963-5489',     endereco: 'Rua das araucarias',     numero: '1759',     profissao: 'Carpinteiro',     email:'joaobotelho@carpintariabotelho.com.br'    }    )}    >Detalhes...</Text>   </View>   <View style={{marginTop:20}}>    <Text>Nome: João Botelho</Text>     <Text>Telefone: (11) 93300-8587</Text>     <Text    onPress={()=> navigation.navigate('Information',     {     nome:'Amanda Silva',     telefone:'(19) 96587-5222',     endereco: 'Av. Senna Nogueira',     numero: '3958',     profissao: 'Desenvolvedora de Softwares',     email:'amandasilvadeveloper@gmail.com'    }    )}    >Detalhes...</Text>   </View> |
| ------------------------------------------------------- | ------------------------------------------------------------ |
|                                                         |                                                              |




Recebendo as propriedades dentro de Details:





Default

| 123456789101112 | export default function Information({ route }) { return (   <View >   <Text>Nome: {route.params.nome}</Text>   <Text>Telefone: {route.params.telefone}</Text>   <Text>Endereço: {route.params.endereco}</Text>   <Text>N°: {route.params.numero}</Text>   <Text>Profissão: {route.params.profissao}</Text>   <Text>Email: {route.params.email}</Text>  </View> );} |
| --------------- | ------------------------------------------------------------ |
|                 |                                                              |



###  **DICA**

Para nosso app não quebrar quando passarmos algum parâmetro que não existe, ou que esperamos receber e não foi passado, basta adicionar ‘?’ após params:





Default

| 1    | <Text>Nome: {route.params?.nome}</Text> |
| ---- | --------------------------------------- |
|      |                                         |



Vamos seguir aprendendo mais sobre Tab Navigation.

##  **Tab Navigation**

O Tab Navigation é uma forma de navegação entre telas através de uma barra fixa na parte inferior do nosso app.

Vamos começar então fazendo as configurações necessárias e montar uma estrutura bem interessante que é ter o Stack navigation atuando junto do Tab Navigation que é muito utilizado nos projetos de apps atuais. Vamos começar:

Vamos importar o Tab Navigation.





Default

| 1    | import { createBottomTabNavigator } from '@react-navigation/bottom-tabs'; |
| ---- | ------------------------------------------------------------ |
|      |                                                              |




Precisamos também criar uma const para poder utilizar o Tab navigator logo abaixo do nosso Stack.





Default

| 12   | const Stack = createStackNavigator();const Tab = createBottomTabNavigator() |
| ---- | ------------------------------------------------------------ |
|      |                                                              |




Vamos Criar um component Agenda para ser nossa principal tela a ser carregada e poderemos navegar entre a tela principal de agenda e os contatos através do nosso Tab Navigation.





Default

| 12345678910 | import React from 'react';import { Text, View } from 'react-native'; export default function AppContacts() { return (  <View >   <Text>App Contacts</Text>  </View> );} |
| ----------- | ------------------------------------------------------------ |
|             |                                                              |




E agora dentro do da nossa function Tabs utilizaremos para ficar disponível no rodapé do nosso app.

Não podemos esquecer de importar Agenda dentro de App.js.





Default

| 1    | import AppContacts from './src/pages/AppContacts/' |
| ---- | -------------------------------------------------- |
|      |                                                    |




Precisamos criar uma function para poder utilizar dentro do nosso stackNavigation.





Default

| 12345678 | function Tabs() { return(  <Tab.Navigator >    <Tab.Screen name="AppContacts" component={AppContacts}/>    <Tab.Screen name="Contacts" component={Contacts}/>   </Tab.Navigator> )} |
| -------- | ------------------------------------------------------------ |
|          |                                                              |




Após a configuração acima, nós podemos então chamar o nosso Tabs dentro do nosso stack navigation passando Tabs como parâmetro do nosso component Agenda.





Default

| 12345678910 | export default function App() { return (  <NavigationContainer>   <Stack.Navigator >    <Stack.Screen name="AppContacts" component={Tabs}/>    <Stack.Screen name="Information" component={Information}/>   </Stack.Navigator>  </NavigationContainer> );} |
| ----------- | ------------------------------------------------------------ |
|             |                                                              |



Agora temos o nosso Tab navigation sendo carregado, controlando o acesso tanto da nossa página principal quanto a página de contatos e temos em cada contato o link para os detalhes do contato sendo gerenciado a navegação através do Stack Navigation

 

Espero que tenha curtido essa nossa aula, espero que tenha aprendido de fato os primeiros passos sobre navegações no React Native e com os conhecimentos adquiridos possa criar super Apps!

Até a próxima aula!


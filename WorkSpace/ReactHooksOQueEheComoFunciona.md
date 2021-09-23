# React Hooks: o que é e como funciona?

- [Front-End](https://www.zup.com.br/categorias/front-end)  -  16 abr 2019

#### Neste artigo você vai ver:

- [Motivação](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Antes de continuarmos, um pouquinho sobre Typescript](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Porque typescript?](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Cenário anterior](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [Componente Counter com Classe:](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Trocando Class por Hooks](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Extinção das classes?](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Estado](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [useState](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [useReducer](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Ciclos de vida](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [useEffect](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [ComponentDidMount](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [ComponentDidUpdate](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [ComponentWillUnmount](https://www.zup.com.br/blog/reacthooks#texto-blog)
  - [ComponentWillUnmount com hooks](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Custom Hooks](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Hooks cobrem todos os ciclos anteriores?](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Regras](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Resumo](https://www.zup.com.br/blog/reacthooks#texto-blog)
- [Sugestões?](https://www.zup.com.br/blog/reacthooks#texto-blog)

Já podemos utilizar hooks no React? Antes de respondermos essa pergunta, você já sabe o que é Hooks? Se não, vamos juntos tentar entender melhor sobre este novo recurso.

Resumidamente, hooks são uma nova proposta que irá nos permitir utilizar estado, ciclo de vida, entre outras funcionalidades sem a necessidade de escrevermos componentes com classe. A [proposta](https://github.com/reactjs/rfcs/pull/68) já foi aceita e, já se encontra disponível na versão 16.8 do React.

Então vamos entender melhor como os Hooks irão mudar e impactar o nosso desenvolvimento de [UI](https://www.zup.com.br/blog/ux-vs-ui-diferencas) com React.

### Motivação

Hooks resolve uma grande variedade de problemas encontrados durante o desenvolvimento de componentes, irei aqui listar alguns exemplos:

*– Reutilização de lógica de estado entre components.*

*– Wrapper Hell (HOC, Render props — React DevTools).*

*– Componentes complexos e difíceis de se compreender.*

*– Componentes contendo grandes responsabilidades.*

*– Confusão ao utilizar classes(this, classes).*‍**‍**

### **Antes de continuarmos, um pouquinho sobre Typescript**

Ele vem dominando e tendo uma grande imersão em aplicações que anteriormente só utilizavam javascript. Que tal então já escrevermos nossos exemplo em TS, para irmos nos acostumarmos com os tipos?

### **Porque typescript?**

**‍**Nos fornece um sistema de tipos para JavaScript, dando a oportunidade de checarmos nossos tipos em tempo de desenvolvimento. Type check tem provado aprimorar a qualidade, compreensibilidade e manutenção do código.

### Cenário anterior

Imagine que você tenha um componente sem estado e ciclo de vida, e a partir deste momento por alguma necessidade, precise desses recursos em seu componente?

<p> CODE: https://gist.githubusercontent.com/isacjunior/b1be13bd2241c93894f6c676103a97fa.js</p>

No componente acima apenas mostramos a propriedade counter recebida via props. Agora vamos necessitar de um estado local que será responsável por manter o valor do count. Surgindo essa necessidade, aí vem a obrigatoriedade de reescrevermos com classe.

##### Componente Counter com Classe:

<p> CODE: https://gist.githubusercontent.com/isacjunior/be49c50d735ed32c6359f6e75dacf188.js</p>

### Trocando Class por Hooks

Agora temos a mesma lógica do componente anterior com Hooks. É notável a redução de escrita e a facilidade de se compreender melhor como o componente irá se comportar.

<p> CODE: https://gist.githubusercontent.com/isacjunior/8cc9c7c597891a26296203dd939e80c9.js</p>

### Extinção das classes?

Não necessariamente você precisa reescrever todo o seu código para que ele seja escrito utilizando hooks, mas já relataram que pretendem no futuro retirar o suporte as classes do package **react**, repassando essa responsabilidade para uma lib distinta. Então se você gosta de escrever seus componentes com classe, não se preocupe, irão manter nessa lib o **Component** e **PureComponent.**

### Estado

##### **useState**

**‍**Como já vimos no exemplo anterior, é a forma como iremos definir nosso estado em nossos componentes.

‍

##### **useReducer**

**‍**É uma alternativa para mantermos nosso estado quando o mesmo é mais complexo. Se você conhece a sintaxe do redux, a mesma é utilizada no useReducer. Algo que deve ser mencionado é que aqui não temos a propagação do estado por toda a aplicação como o redux proporciona. Caso queira algo similar, terá que utilizar useContext.

### Ciclos de vida

##### **useEffect**

Este será responsável por nos ajudar a lidar com side effects em nossa aplicação, ele irá substituir os ciclos de vida que tínhamos anteriormente. O primeiro parâmetro do useEffect é uma função de callback que irá ser disparada quando o componente for montado.

Também irei listar um pequeno exemplo de como utilizaríamos com classe e agora com Hooks.

##### **ComponentDidMount**

<p> CODE: https://gist.githubusercontent.com/isacjunior/dc0ab49327e05f544c923ab6150d1077.js</p>

De início pode parecer bem estranho, para termos o efeito de **componentDidMount** com hooks, é necessário passar um array vazio como segundo parâmetro para o hook useEffect.

<p> CODE: https://gist.githubusercontent.com/isacjunior/70177e032f25687c7db5a14435e0bd42.js</p>

‍

##### **ComponentDidUpdate**

<p> CODE: https://gist.githubusercontent.com/isacjunior/03489360e04703cfa2f3d463503edc9e.js</p>

Similar ao que temos no componentDidMount com hooks, precisamos passar os valores de **estado** e **props** dentro de um array no segundo parâmetro da função useEffectpara mantermos o efeito do ciclo **componentDidUpdate**.

Observação: Neste caso não é necessário nem informar o tipo do estado namepois, o Typescript já infere para nós que é uma string quando iniciamos o estado com um texto vazio.

<p> CODE: https://gist.githubusercontent.com/isacjunior/f8a327e27b454794ea7a66a547a70e1c.js</p>

‍

##### **ComponentWillUnmount**

<p> CODE: https://gist.githubusercontent.com/isacjunior/1f04c3021a690921f7a1a7efb2884cfd.js</p>

‍

##### **ComponentWillUnmount com hooks**

<p> CODE: https://gist.githubusercontent.com/isacjunior/1aaaabba35ecd275f4c6430bbacb4dcf.js</p>

Você deve ter notado que para todos os três métodos que utilizávamos anteriormente, o useEffect engloba os mesmos efeitos em um único hook. O retorno e parâmetros do useEffect são o que diferencia seu comportamento.

### Custom Hooks

Você também é livre pra criar seus próprios Hooks podendo compartilhar lógica entre componentes.

Este é o pulo do gato, use sempre que necessário.

<p> CODE: https://gist.githubusercontent.com/isacjunior/66a79a0f3ac3667d1f8c97049d3390a3.js</p>

### Hooks cobrem todos os ciclos anteriores?

Não, existem alguns fluxos que o hooks ainda não suportam como, por exemplo o **getDerivedStateFromError**, **componentDidCatch** e **getSnapshotBeforeUpdate**. Estes devem ser implementados em um futuro próximo e se por acaso precisar, deverá ainda utilizar classes nestes casos.

### Regras

Algumas regras devem ser cumpridas na utilização de hooks:

*– Não utilize hooks em loops.*

*– Não utilize hooks em condições.*

*– Declare seus hooks no topo do componente.*

‍

Para manter este padrão e evitar problemas, existe um plugin do eslint que pode te auxiliar e evitar o uso incorreto dos hooks:

[– eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)

‍

### Resumo

> *Se você gosta de escrever seus components com classe, use hooks.*
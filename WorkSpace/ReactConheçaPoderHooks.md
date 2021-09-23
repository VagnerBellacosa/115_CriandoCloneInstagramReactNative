**[Javascript](https://www.treinaweb.com.br/blog/categoria/javascript)**

# React: Conheça o Poder dos Hooks

Conheça o que os React Hooks podem fazer e como eles vão facilitar o processo de desenvolvimento da sua próxima aplicação.

 mais de 2 anos atrás

[Artigos](https://www.treinaweb.com.br/blog)React: Conheça o Poder dos Hooks

Olá Web Developers! Vamos conhecer o poder dos Hooks do React.

## O que são React Hooks?

Até a versão `16.7` era necessário criar classes para utilizar todas as funcionalidades do React em um componente, como estado e lifecycle.

Era possível criar componentes a partir de funções, mas esses componentes apenas recebiam propriedades, não possuindo lifecycles, estados e outras funcionalidades do React.

Os `Hooks` foram introduzidos na versão `16.8`, e nos permitem utilizar vários recursos do `React` dentro de funções de forma bem simples.

## Por que usar Hooks?

Os `Hooks` nos ajudam a organizar a lógica que será usada em um componente. Podemos até criar nossos próprios `Hooks` para reutilizar a lógica em vários componentes. A própria comunidade está criando `Hooks` muito interessantes que podemos utilizar em nossos projetos.



![React - Tópicos Avançados](https://d2knvm16wkt3ia.cloudfront.net/assets/svg-icon/react.svg)

##### CursoReact - Tópicos Avançados

[Conhecer o curso](https://www.treinaweb.com.br/curso/react-topicos-avancados)

## Hooks

Vamos conhecer os dois principais `Hooks`, `useState` e `useEffect`.

### useState

O `useState` nos permite criar estados em um componente criado a partir de uma função, assim como o `state` presente em componentes criados a partir de classes.

Veja o exemplo da seguinte classe:

Copiar

```jsx
class Treinaweb extends React.Component{
	constructor(props){
		super(props);
		this.state = {
			nome: 'TreinaWeb'
		}
	}
	
	render(){
		return {
			<div>
				<p>{this.state.nome}</p>
				<button onClick={() => this.setState({nome: 'React'})} >CLICK</button>
			</div>
		}
	}
}
```

Com os `Hooks` nós teremos o seguinte código:

Copiar

```jsx
function Treinaweb (props){
	const [nome, setNome] = useState('TreinaWeb');
	
	render(){
		return {
			<div>
				<p>{nome}</p>
				<button onClick={() => setNome('React')} >CLICK</button>
			</div>
		}
	}
}
```

Bem menos código, não é mesmo? Vamos entender o que o `useState()` está fazendo.

O `useState()` cria uma variável que controlará o estado do componente. Se quiser outra variável execute outro `useState()`.

Para este `Hook` nós passamos o valor inicial do estado, em nosso exemplo, a `String` “TreinaWeb”. Como retorno temos a variável com o valor do estado, que demos o nome de `nome`, e uma função que serve unicamente para atualizar o valor desta variável, que demos o nome de `setNome`.

Veja que no clique do botão apenas chamamos esta função `setNome()`, passando o novo valor.

Por estar tudo declarado dentro da própria função, não temos mais a necessidade de utilizar o `this`, que pode ser complicado de ser compreendido no JavaScript para iniciantes, causando erros no código.

### useEffect

O `useEffect` é um `Hook` que serve para lidar com os efeitos. Podemos usá-los como os lifeCycles `componentDidMount`, `componentDidUpdate` e `componentWillUnmount`.

Imagine que a gente tenha uma API que nos retorna uma lista de produtos baseado no nome que passarmos.

Copiar

```jsx
function Treinaweb (props){
	const [produto, setProduto] = useState('Leite');
	
	useEffect(() => {
		Produtos.buscar(produto);
	})
	
	render(){
		return {
			<div>
				<p>{produto}</p>
				<button onClick={() => setProduto('Chocolate')} >CLICK</button>
			</div>
		}
	}
}
```

O `useEffect()` recebe como primeiro parâmetro uma função que será executada assim que o componente renderizar. Então é um ótimo lugar para fazer requisições.

Dessa maneira como escrevemos, a função passada ao `useEffect()` será executada sempre que o componente for atualizado.



![React - Dominando Componentes](https://d2knvm16wkt3ia.cloudfront.net/assets/svg-icon/react.svg)

##### CursoReact - Dominando Componentes

[Conhecer o curso](https://www.treinaweb.com.br/curso/react-dominando-componentes)

A beleza deste `Hook` é que podemos definir facilmente quando queremos que esta função seja executada novamente. Basta passar como segundo parâmetro ao `useEffect()` um `Array` com as variáveis que controlarão esse `Hook`.

Vamos supor que queremos que a função seja executada apenas quando a variável `produto` for alterada. Ficaria assim:

Copiar

```jsx
	useEffect(() => {
		Produtos.buscar(produto);
	}, [produto])
```

E se quisermos que a função seja executada apenas uma vez, que é quando o componente é inserido na tela, basta passar um `Array` vazio.

Copiar

```jsx
	useEffect(() => {
		Produtos.buscar(produto);
	}, [])
```

Você pode executar quantos `useEffects()` quiser, o que nos dá mais controle sobre o que e quando algo deve ser executado.

## Reutilização de Hooks

Podemos criar nossos próprios `Hooks`. Basta criar uma função que utilize outros `Hooks` e retorne algum valor. Assim poderemos ter uma lógica fora dos componentes e reutilizá-la onde quisermos. Essas funções também devem ter seu nome iniciado com `use`.

O site https://usehooks.com/ possui vários exemplos de `Hooks` interessantes que podem ser muito úteis em seu projeto, como carregar imagens apenas se estiverem visíveis na tela, criar funcionalidade de desfazer, criar atalhos de teclado, etc. Também é uma ótima fonte para entender melhor os `Hooks` na prática, vendo os códigos disponíveis.

Os `Hooks` nos permitem trabalhar de forma limpa e simples no React, nos dando um grande poder. Com ajuda da comunidade estamos vendo várias possibilidades interessantes.

Já criou um `Hook`? Compartilhe aqui com a gente pelos comentários!

- [#JavaScript](https://www.treinaweb.com.br/blog/tag/javascript)
- [#ReactJS](https://www.treinaweb.com.br/blog/tag/reactjs)
- [#React Hooks](https://www.treinaweb.com.br/blog/tag/react-hooks)
- [#O que são React Hooks](https://www.treinaweb.com.br/blog/tag/o-que-sao-react-hooks)
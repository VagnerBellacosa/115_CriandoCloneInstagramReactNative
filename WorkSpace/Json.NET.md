**JSON - Introdução e conceitos básicos**

------

| ![img](http://www.macoratti.net/mac3_1.jpg) | Neste artigo eu vou apresentar o **JavaScript Object Notation (ou JSON)**, um formato de intercâmbio de dados abertos e baseado em texto que fornece um formato de troca de dados padronizado mais adequado para aplicações baseadas em Ajax. |
| ------------------------------------------- | ------------------------------------------------------------ |
|                                             |                                                              |

***Obs: Assim como XML, JSON também pode ser visto uma alternativa ao modelo de dados relacional mais apropriadamente a dados semiestruturados.***

Mas o que JSON tem a ver com a plataforma .NET, com VB .NET, C# e ASP .NET ?

**Tudo !!**

Quando você cria uma aplicação que irá se comunicar com outra aplicação, quer seja ela local ou remota, você esta trocando informações e neste caso um formato de dados e um protocolo de troca deve ser selecionado para que a comunicação seja feita com sucesso. Por sucesso entende-se que quem recebe a informação consegue tratá-la e entender o seu significado.

Existem uma variedade de opções de protocolos abertos padronizados, tais como *SOAP, XML, etc.,* que podem ser adotados e isso vai depender da finalidade e dos requisitos da sua aplicação.

Dessa forma, JSON é um protocolo leve para intercâmbio de dados e está baseado em um subconjunto da linguagem de programação **JavaScript**, sendo independente desta e de qualquer linguagem.

JSON lembra XML :

- JSON é texto simples
- JSON é "auto-descritivo" (legível)
- JSON é hierárquico (valores dentro de valores)
- JSON pode ser analisado pelo JavaScript
- JSON os dados podem ser transportadas usando AJAX

mas é diferente da XML:

- Não utiliza a tag de fechamento
- É mais curto e simples
- É mais rápido de ler e escrever
- Pode ser analisado usando a função eval() do JavaScript
- Utiliza matrizes
- Não possui palavras reservadas
- Possui parser nas principais linguagens e navegadores

Assim, JSON é menor do que XML, é mais rápido e mais fácil de analisar.

O motivo principal para usar JSON é que em aplicações web com AJAX, JSON é muito mais rápido e fácil de usar do que XML.

A sintaxe JSON é um subconjunto da linguagem JavaScript *(sendo independente desta repito)*.

As principais regras de sintaxe JSON são:

- **Dados JSON estão definidos aos pares no formato:** **nome : valor**
- **Os dados são separados por vírgulas(,)**
- **As chaves {} contém objetos**
- **Os colchetes [] expressam** ***matrizes/vetores***

Basicamente o JSON se baseia na notação **NOME : VALOR**, onde **NOME** pode ser o nome que você deseja usar para identificar um objeto e **VALOR** o valor deste objeto.

A sintaxe JSON usa o par **NOME : VALOR** onde nome é definido entre aspas, seguido por dois pontos, seguido por um valor: **Ex: "nome" : "Macoratti" , "font-size" : "14px;"**

Em JSON os valores usados podem ser:

- **Um número (inteiro ou ponto flutuante)**
- **Uma string (entre aspas)**
- **Um booleano (verdadeiro ou falso)**
- **Uma matriz (entre colchetes[])**
- **Um objeto (entre chaves {})**
- **nulo**

Os objetos JSON são definidos entre chaves **{}** e podem conter múltiplos pares nome:valor:

**Ex:**

**var pessoa = { "nome" : "Jose Carlos" , "sobrenome" : "Macoratti" };**

**var produto = {"ProdutoID":1, "Descricao":"Notebook 14", "ProdutoNumero":"PRD-5381"};**

Os arrays em JSON são definidos entre colchetes **[]** e podem conter múltiplos objetos:

**Ex1: var cores = [ "Azul" , "Branco", "Vermelho", "Amarelo" ];**

Podemos acessar os dados usando a seguinte sintaxe:

```
<Script Language="JavaScript">   **var cores = [ "Azul" , "Branco", "Vermelho", "Amarelo" ];**    for (i=0; i<4; i++){      **document.write( cores[i]+ "<br>" );**    } </Script> 
```

**Ex2:**

**var escola =
         {
           "alunos": [ { "nome":"Jose Carlos" , "sobrenome":"Macoratti" }, { "nome":"Ana" , "sobrenome":"Lima" }, { "nome":"Pedro" , "sobrenome":"Ramos" } ]
         }**

Neste exemplo temos um objeto alunos definido como um array contendo 3 objetos . Cada objeto possui nome e sobrenome.

A primeira entrada no objeto array pode ser acessada da seguinte forma:

**alunos[0].nome; => retona Jose Carlos**

Para alterar um valor usamos a seguinte sintaxe:

**alunos[0].nome = "Teste";**

Vejamos a seguir a definição de uma estrutura de dados mais complexa usando JSON:

```
**var agenda =**  {    "nome": "Jose Carlos",    "sobrenome": "Macoratti",    "idade": 45,    "endereco":  {                             "endereco": "Rua Projetada, 200",                            "cidade": "Santos",                            "estado": "SP",                           "cep": 11054058                       },    "telefone": [                            {                                "tipo": "fixo",                                "numero": "212 555-1234"                            },                            {                                "tipo": "celular",                                "numero": "646 555-4567"                            }                     ] }
```

O exemplo mostra a representação JSON de um objeto que descreve uma pessoa. O objeto tem campos string para o nome e sobrenome, um campo número para a idade, contém um objeto que representa o endereço da pessoa, e contém uma lista (uma matriz) de objetos para os números de telefone.

No exemplo acima onde temos a variável agenda contendo os dados JSON, podemos usar a função eval() para criar o objeto contato JavaScript da seguinte forma: var contato = eval("(" + agenda + ")");

**Obs: a variável agenda precisa estar envolvida em parênteses para evitar ambiguidade com a sintaxe JavaScript.**

A função JavaScript **eval()** pode ser usada para converter um texto JSON em um texto JavaScript pois a função eval() usa o compilador JavaScript que irá analisar o texto JSON e um produzir um objeto JavaScript. Para evitar um erro de sintaxe o texto precisa ser envolvido por parênteses.

Abaixo um exemplo de utilização da função eval() onde criamos um objeto JavaScript a partir de um array JSON e exibimos o segundo objeto do array:

| `<!DOCTYPE html> <html> <body> <h2>Cria um Objeto a partir de uma string JSON</h2> <p> Nome: <span id="nome"></span><br>  Sobrenome: <span id="sobrenome"></span><br>  </p>  <script> **var txt = '{"funcionarios":[' + '{"nome":"Jose Carlos","sobrenome":"Macoratti" },' + '{"nome":"Janice","sobrenome":"Rachel" },' + '{"nome":"Jefferson","sobrenome":"Andre" }]}';** **var obj = eval ("(" + txt + ")");** document.getElementById("nome").innerHTML=obj.funcionarios[1].nome  document.getElementById("sobrenome").innerHTML=obj.funcionarios[1].sobrenome  </script> </body> </html> ` |      |
| ------------------------------------------------------------ | ---- |
| ![img](http://www.macoratti.net/13/08/aspn_json1.gif)        |      |

Como a função eval() pode compilar e executar qualquer JavaScript isso representa um potencial problema de segurança.Por isso é mais seguro usar um parser JSON para converter um texto JSON para um objeto JavaScript.

Um parser ou analisador JSON irá reconhecer apenas o texto JSON e não vai compilar os scripts.Em navegadores que oferecem suporte nativo a JSON, os parsers JSON também são mais rápidos. O apoio ao JSON nativo está incluído nos navegadores mais novos e no mais novo padrão ECMAScript (JavaScript).

Atualmente navegadores como o Firefox e Internet Explorer incluem características especiais para analisar (parsers) JSON, sendo esse suporte ao navegador nativo mais eficiente e seguro do que o usar o recurso eval() do JavaScript.

Na continuação deste artigo vou mostrar como usar JSON com ASP .NET : [ASP .NET - Usando JSON para trocar informações entre um serviço WCF e um Web site Ajax](http://www.macoratti.net/13/07/aspn_json.htm)

[Veja os ](http://www.macoratti.net/destaque.htm)[Destaques e novidades do SUPER DVD Visual Basic (sempre atualizado) : clique e confira !](http://www.macoratti.net/destaques.htm)**Quer migrar para o VB .NET ?**Veja mais sistemas completos para a plataforma .NET no **[Super DVD .NET](http://www.macoratti.net/superdvd.htm)** , confira...[**Curso Básico VB .NET - Vídeo Aulas**](http://www.macoratti.net/curso_vbnet_basico.htm)**Quer aprender C# ??**Chegou o **[Super DVD C#](http://www.macoratti.net/superdvdc.htm)** com exclusivo material de suporte e vídeo aulas com curso básico sobre C#.[**Curso C# Basico - Video Aulas**](http://www.macoratti.net/curso_cshp_basico.htm)

 

​       Gostou ?  ![img](http://www.macoratti.net/face32.jpg) [Compartilhe no Facebook ](http://www.macoratti.net/13/07/net_json.htm#) ![img](http://www.macoratti.net/twiter32.jpg) [Compartilhe no Twitter](javascript: void(0);)
 

Referências:

- [Seção VB .NET do Site Macoratti.net](http://www.macoratti.net/pageview.aspx?catid=1)

- [Super DVD .NET - A sua porta de entrada na plataforma .NET](http://www.macoratti.net/superdvd.htm)

- [Super DVD Vídeo Aulas - Vídeo Aula sobre VB .NET, ASP .NET e C#](http://www.macoratti.net/Vendas/Produtos.aspx?ID=22)

- [Seção C# do site Macoratti.net](http://www.macoratti.net/pageview.aspx?catid=18)

- [Super DVD C#](http://www.macoratti.net/superdvdc.htm)

- [Super DVD Visual Basic](http://www.macoratti.net/supercd.htm)

- [Curso Básico VB .NET - Vídeo Aulas](http://www.macoratti.net/curso_vbnet_basico.htm)

- [Curso C# Básico - Vídeo Aulas](http://www.macoratti.net/curso_cshp_basico.htm)

- [Seção de Jogos do site Macoratti .net](http://www.macoratti.net/pageview.aspx?catid=36)

- [JSON](http://www.json.org/)

- [JSON – Wikipédia, a enciclopédia livre](http://pt.wikipedia.org/wiki/JSON)

- [JSON Tutorial](http://www.w3schools.com/json/default.asp)

- ### [Json.NET](http://json.codeplex.com/)
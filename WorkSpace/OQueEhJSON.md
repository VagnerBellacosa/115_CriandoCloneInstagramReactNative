# O Que É JSON?

![O Que É JSON?](https://www.hostinger.com.br/tutoriais/wp-content/uploads/sites/12/2019/05/O-que-e-JSON.png)

O [**JSON**](https://www.json.org/json-pt.html) (JavaScript Object Notation) é um formato de arquivo para manter e trocar informações legíveis pelas pessoas. O arquivo contém apenas texto e usa a extensão **.json**.

Neste artigo, você vai aprender  sobre o JSON e para que ele é usado. Além disso, também vai ver como ele pode melhorar o desempenho do seu site.

Conteúdo

- [O Que é Json e Para Que Serve](https://www.hostinger.com.br/tutoriais/o-que-e-json#O-Que-e-Json-e-Para-Que-Serve)
- [Sintaxe do JSON](https://www.hostinger.com.br/tutoriais/o-que-e-json#Sintaxe-do-JSON)
- [Dados JSON Armazenados](https://www.hostinger.com.br/tutoriais/o-que-e-json#Dados-JSON-Armazenados)
- [Usando Arrays](https://www.hostinger.com.br/tutoriais/o-que-e-json#Usando-Arrays)
- [Conclusão](https://www.hostinger.com.br/tutoriais/o-que-e-json#Conclusao)

## **O Que é Json e Para Que Serve**

O JSON é um formato que armazena informações estruturadas e é principalmente usado para transferir dados entre um servidor e um cliente.

O arquivo é basicamente uma alternativa simples e mais leve ao **[XML](https://www.000webhost.com/blog/what-is-xml?_ga=2.7978298.90547944.1590513528-1857839723.1588018530)** (*Extensive Markup Language*), que tem funções similares.

Desenvolvedores usam o JSON para trabalhar com **[AJAX](https://www.hostinger.com.br/tutoriais/o-que-e-ajax/)** (*Asynchronous JavaScript and XML*). Esses formatos trabalham juntos para conseguir um carregamento assíncrono de dados armazenados.

Isso significa que um site pode atualizar suas informações sem precisar recarregar a página que você está visitando.

Esse processo é mais fácil de se fazer com o JSON do que em XML/RSS. E, hoje, como vários sites estão usando o AJAX, o arquivo **.json** vem se tornando muito popular.

Além disso, ele permite que os usuários peçam dados de **[domínios](https://www.hostinger.com.br/tutoriais/como-registrar-um-dominio/)** diferentes com um método chamado de **[JSONP](https://pt.wikipedia.org/wiki/JSONP)** aplicando tags **<script>.**

Caso contrário, você não vai conseguir transferir dados através de domínios devido à **[política da mesma origem](https://pt.wikipedia.org/wiki/Política_de_mesma_origem)**.

## **Sintaxe do JSON**

Para criar corretamente o formato **json**. Você tem que seguir exatamente a sua sintaxe.

Existem dois elementos centrais em um objeto JSON: ***Keys\*** (chaves) e ***Values\*** (valores).

- **Keys** devem ser strings (linhas). Elas contêm uma sequência de caracteres cercadas por aspas.
- **Values** são um tipo válido de dados JSON. Eles podem ter um formato de *array, object, string, boolean, number ou null*.

Um objeto JSON inicia e termina com chaves **{}**. Ele tem dentro dois ou mais pares de **key/value**, com uma **vírgula** para separá-los. Cada chave é seguida por dois **pontos** para diferenciar o valor.

Veja um exemplo:

{"city":"New York", "country":"United States "}

Temos dois pares de key/values aqui: **city** e **country** são as keys; **New York** e **United States** são os values.

### **Tipos de Valores**

Valores contêm um tipo válido de dados JSON, como:

#### **Array**

Um array é uma coleção ordenada de valores. É cercado por **colchetes** **[]** e cada valor dentro é separado por uma vírgula.

Um valor de array pode conter objetos JSON. Isso significa que ele usa o mesmo conceito de key/value. Por exemplo:

"students":[      

{"firstName":"Tom", "lastName":"Jackson"},

{"firstName":"Linda", "lastName":"Garner"},

{"firstName":"Adam", "lastName":"Cooper"}

]

A informação entre colchetes é um array, que tem três objetos.

#### **Object**

Um objeto contém uma key e value. Tem dois pontos depois de cada key e uma vírgula depois de cada value, que também diferencia cada objeto. Ambos estão dentro de aspas.

Object, como um value, deve seguir as mesmas regras que um objeto. como:

“employees”: {"firstName":"Tom", "lastName":"Jackson”}

Aqui, **employees** é a chave enquanto tudo dentro das chaves é um objeto.

#### **Strings**

Uma string é uma sequência definida de zero ou mais caracteres Unicode. É colocado entre duas aspas duplas.

O exemplo abaixo mostra que **Tom** é uma string, pois é um conjunto de caracteres dentro de aspas duplas.

"firstName":"Tom"

#### **Number**

Number em JSON deveria ser do tipo **inteiro** ou um tipo **fracionado**, como:

{“age”:”30”}

#### **Boolean**

Você pode usar as opções **true** (verdadeiro) ou **false** (falso) como valor, seguindo:

{“married”:”**false**”)

#### **Null**

Esse formato mostra que não há informação.

{“bloodType”:”**null**”}

## **Dados JSON Armazenados**

Você tem duas formas de armazenar dados no JSON: *object* e *array*. O primeiro se parece com isso:

{

"firstName":"Tom",

"lastName":"Jackson",

"gender":"male"

}

As Chaves **{}** significam que é um objeto JSON. Elas envolvem três pares de key/value que são separados por vírgulas.

Em cada par, você tem as keys (*firstName*, *lastName* e *gender*) seguidas por dois pontos para diferenciar de outros values (*Tom*, *Jackson*, *male*).

Os values nesse exemplo são strings. É por isso que eles também estão entre aspas, semelhantes às keys.

## **Usando Arrays**

Outro método de armazenamento de dados é o array. Olhe para esse exemplo:

{

"firstName":"Tom",

"lastName":”Jackson”,

“gender”:”male”,

"hobby":["football", "reading", "swimming"]

}

O que diferencia isso do método anterior é o quarto par de key/value. **Hobby** é a key e existem vários values (*football*, *reading*, *swimming*) entre colchetes, que representam um array.

Ele pode ser útil quando emparelhado com o JSONP para resolver o problema dos domínios diferentes.

Esse processo funciona usando o que é chamado de **callbacks**, que solicitará um item específico no Array sem obter um erro da mesma origem.

E, finalmente, o Array também suporta o **[comando Loop for Bash](https://www.hostinger.com.br/tutoriais/bash-for-loop-guia/)**, permitindo que você execute repetidos comandos para pesquisar múltiplos dados. Isso torna o processo mais rápido e mais eficaz.

## **Conclusão**

Como você pode ver, a extansão JSON é uma ferramenta útil para a troca recíproca de dados. Ele tem muitas vantagens:

- Ele pode carregar informações de forma assíncrona para que seu site seja mais responsivo e possa lidar com o fluxo de dados com mais facilidade.
- Você pode também usá-lo para superar problemas de domínio cruzado quando extrair informações de outro site.
- O JSON é simples e mais leve que o XML.

Esperamos que você tenha entendido melhor o JSON e esteja apto para gerenciar seu site de uma forma mais efetiva.
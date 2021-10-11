# Efeitos de animação com a lib Animate.css

![img](https://secure.gravatar.com/avatar/dbc78bbb3a02e3db6bf745bb7c6d0bd0?s=60&d=mm&r=g)

###### [Rodrigo Aramburu](https://www.botecodigital.dev.br/author/rodrigo/)

07/07/2018

 

*Animate.css* é uma biblioteca *CSS* de pequenas animações com vários efeitos interessante para dar destaques em elementos da nossa página. Você pode conferir os efeitos na própria [página do projeto](https://daneden.github.io/animate.css/).

Vamos ao da biblioteca então, primeiramente devemos incluir a biblioteca no nossos *head,* o que pode ser feito direto pelo *CDN*:

```
<``link` `rel``=``"stylesheet"` `href``=``"https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css"` `rel``=``"nofollow"``>  
```

Baixando pelo *bower*:

```
bower ``install` `animate.css --save
```

ou ainda baixando direto do [Git do projeto](https://github.com/daneden/animate.css)

Após a biblioteca estar carregada, para executar uma animação basta adicionar ao elemento desejado, via *javascript*, as classes *“animated”* e a correspondente ao efeito desejado.

Segue a lista de efeitos disponíveis(clique para visualizar o efeito):

| [bounce](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=shake) | [flash](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=flash) | [pulse](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=pulse) | [rubberBand](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rubberBand) |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [shake](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=shake) | [headShake](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=headShake) | [swing](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=swing) | [tada](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=tada) |
| [wobble](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=wobble) | [jello](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=jello) | [bounceIn](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceIn) | [bounceInDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceInDown) |
| [bounceInLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceInLeft) | [bounceInRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceInRight) | [bounceInUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceInUp) | [bounceOut](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceOut) |
| [bounceOutDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceOutDown) | [bounceOutLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceOutLeft) | [bounceOutRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceOutRight) | [bounceOutUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=bounceOutUp) |
| [fadeIn](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeIn) | [fadeInDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInDown) | [fadeInDownBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInDownBig) | [fadeInLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInLeft) |
| [fadeInLeftBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInLeftBig) | [fadeInRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInRight) | [fadeInRightBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInRightBig) | [fadeInUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInUp) |
| [fadeInUpBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeInUpBig) | [fadeOut](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOut) | [fadeOutDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutDown) | [fadeOutDownBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutDownBig) |
| [fadeOutLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutLeft) | [fadeOutLeftBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutLeftBig) | [fadeOutRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutRight) | [fadeOutRightBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutRightBig) |
| [fadeOutUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutUp) | [fadeOutUpBig](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=fadeOutUpBig) | [flipInX](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=flipInX) | [flipInY](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=flipInY) |
| [flipOutX](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=flipOutX) | [flipOutY](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=flipOutY) | [lightSpeedIn](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=lightSpeedIn) | [lightSpeedOut](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=lightSpeedOut) |
| [rotateIn](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateIn) | [rotateInDownLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateInDownLeft) | [rotateInDownRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateInDownRight) | [rotateInUpLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateInUpLeft) |
| [rotateInUpRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateInUpRight) | [rotateOut](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateOut) | [rotateOutDownLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateOutDownLeft) | [rotateOutDownRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateOutDownRight) |
| [rotateOutUpLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateOutUpLeft) | [rotateOutUpRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rotateOutUpRight) | [hinge](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=hinge) | [jackInTheBox](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=jackInTheBox) |
| [rollIn](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rollIn) | [rollOut](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=rollOut) | [zoomIn](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomIn) | [zoomInDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomInDown) |
| [zoomInLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomInLeft) | [zoomInRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomInRight) | [zoomInUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomInUp) | [zoomOut](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomOut) |
| [zoomOutDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomOutDown) | [zoomOutLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomOutLeft) | [zoomOutRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomOutRight) | [zoomOutUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=zoomOutUp) |
| [slideInDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideInDown) | [slideInLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideInLeft) | [slideInRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideInRight) | [slideInUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideInUp) |
| [slideOutDown](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideOutDown) | [slideOutLeft](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideOutLeft) | [slideOutRight](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideOutRight) | [slideOutUp](https://www.botecodigital.dev.br/exemplos/animatecss/efeitos.php?efeito=slideOutUp) |

Para adicionar as classes podemos utilizar *javascript* puro,

```
<``h1``>Exemplo de uso Animate.css</``h1``>
var` `h1 = document.querySelector(``'h1'``);``h1.addEventListener(``"click"``, ``function``(){``  ``h1.classList.add(``'animated'``);``  ``h1.classList.add(``'bounce'``);``});
```

[Veja um exemplo](https://www.botecodigital.dev.br/exemplos/animatecss/)

ou também podemos utilizar a biblioteca [*jQuery*](https://www.botecodigital.dev.br/jquery/iniciando-com-jquery/):

```
$(document).ready(``function``(){        ``  ``$(``'h1'``).click(``function``(){``    ``$(``'h1'``).addClass(``'animated bounce'``);``  ``});       ``});
```

A *Animate.css* é uma biblioteca muito fácil de utilizar, mas uma vez que a animação é realizada, deve-se remover e adicionar as classes novamente para que a animação se repita. Podemos fazer isto, removendo a classes de animação quando o evento de animação terminar.

```
$(``'h1'``).one(``'animationend'``, ``function``(){``   ``$(``this``).removeClass();``});
```

No exemplo acima capturamos o evento gerado quando uma animação *CSS* termina(*animationend*) e removemos todas as classes do elemento selecionado.

Para obtermos uma melhor compatibilidade com os eventos de navegadores antigos, a própria página da biblioteca apresenta a solução de adicionar uma nova função no *jQuery* e chamar os efeitos através dela.

Segue abaixo o código:

```
$.fn.extend({`` ``animateCss: ``function``(animationName, callback) {``  ``var` `animationEnd = (``function``(el) {``   ``var` `animations = {``    ``animation: ``'animationend'``,``    ``OAnimation: ``'oAnimationEnd'``,``    ``MozAnimation: ``'mozAnimationEnd'``,``    ``WebkitAnimation: ``'webkitAnimationEnd'``,``   ``};`` ` `   ``for` `(``var` `t ``in` `animations) {``    ``if` `(el.style[t] !== undefined) {``     ``return` `animations[t];``    ``}``   ``}``  ``})(document.createElement(``'div'``));`` ` `  ``this``.addClass(``'animated '` `+ animationName).one(animationEnd, ``function``() {``   ``$(``this``).removeClass(``'animated '` `+ animationName);`` ` `   ``if` `(``typeof` `callback === ``'function'``) callback();``  ``});`` ` `  ``return` `this``;`` ``},``});
```

Após ter carregado o código acima, de um arquivo externo por exemplo, podemos acionar a animação através da função *animateCss*:

```
$(``'#seuElemento'``).animateCss(``'bounce'``);
```

ou;

```
$(``'#seuElemento'``).animateCss(``'bounce'``, ``function``() { ``// realizar algo depois da animação });
```

Bom, era isso e boas animações!
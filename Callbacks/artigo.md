# Introdução a Callbacks no JavaScript

Recentemente escrevi um artigo sobre Promises e Async / Await, não só para contribuir com a comunidade BR mas também na intenção de solidificar meus conhecimentos. Porém, é impossível falar de Promises sem antes desenrolar um assunto fundamental: __As Callbacks__. Se você tem a intenção de entender melhor como funciona o JavaScript de forma assíncrona, este é o primeiro passo.

Então vamos nessa? Simbora.

## O funcionamento do JavaScript

Imagine uma sequência de instruções qualquer, como uma receita de bolo. Para fazer o bolo, basta seguirmos cada passo dessa receita na ordem correta, certo?

```
1. Misturar as gemas, açúcar e margarina
2. Acrescentar leite, fermento e farinha de trigo
3. Despejar a massa numa forma
4. Assar a 180ºC por 40 minutos
```

O JavaScript funciona de maneira similar. Ele irá receber a sequência de instruções do algoritmo e irá executá-lo numa ordem padrão de cima para baixo.

```Javascript

function primeiraMensagem () {
    console.log('Essa mensagem vem por primeiro');
}

function segundaMensagem() {
    console.log('Essa mensagem vem por segundo');
}

primeiraMensagem();
segundaMensagem();

// Output:
// Essa mensagem vem por primeiro
// Essa mensagem vem por segundo
```

## A semântica do Callback

Entendemos que a execução de código sempre seguirá uma determinada ordem. Agora vamos para um outro exemplo. Dessa vez utilizaremos a função `setTimeout` para fazer com que a primeira mensagem demore 3 segundos para ser exibida. Vamos ver o resultado?

```Javascript

function primeiraMensagem () {
    console.log('Essa mensagem vem por primeiro');
}

setTimeout(primeiraMensagem(), 3000);
```

_**gif do output**_

Tem alguma ideia do que pode ter causado este erro? Na verdade, pudemos observar duas coisas:

1. A função `primeiraMensagem` é executada automaticamente, sem a espera dos 3 segundos
2. A função `setTimeout` arremessa um erro de _callback inválida_.

Isso acontece pois como executamos `primeiraMensagem()`, com os parênteses no final, fizemos na verdade uma **Invocação** da função. Ou seja, mandamos ela executar imediatamente. E quando o setTimeout foi procurar o que havia no primeiro parâmetro, não encontrou nada (encontrou undefined), já que `primeiraMensagem` já havia sido executada.

Para que possamos entender completamente, vamos para um exemplo parecido, mas dessa vez retiraremos os parênteses ao final de `primeiraMensagem()`.

```Javascript

function primeiraMensagem () {
    console.log('Essa mensagem vem por primeiro');
}

setTimeout(primeiraMensagem, 3000);
```

_**gif do output**_

Voilá! O que entendemos disso? No cenário acima existe uma diferença semântica na função `primeiraMensagem` de passá-la como argumento, sem os parênteses. Estas são as famosas **_callbacks_**. Ou seja, ela **não está sendo invocada diretamente, e sim sendo passada como parâmetro para que outra função, a `setTimeout`, a chame (CALL) novamente (BACK)**.

Neste segundo exemplo, podemos passar uma função como callback para que a função `recebeCallback` possa utilizar essa função dentro dela.

```JavaScript
function recebeCallback(callbackRecebida) {
    const numeroAleatorio = Math.floor(Math.random() * 101);
    
    callbackRecebida(numeroAleatorio);
}

function imprimeValor(valorParaImprimir) {
    console.log(valorParaImprimir);
}

recebeCallback(imprimeValor);
```
_**gif do output**_

- A função `imprimeValor` será responsável somente por imprimir o valor que recebe como parâmetro.

- A função `recebeCallback` será invocada recebendo `imprimeValor` como callback e assim seguirá:
    1. Irá gerar um número aleatório de 1 a 100;
    2. Irá invocar a callback `imprimeValor` recebida como parâmetro que consequentemente imprimirá no console o número aleatório

## Usando o JavaScript assíncrono com as callbacks

Como passar funções como callbacks já aprendemos, agora exploraremos um pouco mais a fundo pra entender a maior vantagem das callbacks: a utilização do Javascript de maneira assíncrona!

Então vamos para mais um exemplo. Desta vez voltaremos para as duas funções lá do início `primeiraMensagem()` e `segundaMensagem()`. Na função `primeiraMensagem()` iremos enviar uma ordem de espera de 3 segundos para execução e logo em seguida iremos chamar a função `segundaMensagem()`. Qual deverá ser o output? Vamos ver.

```Javascript

function primeiraMensagem () {
    console.log('Essa mensagem vem por primeiro');
}

function segundaMensagem() {
    console.log('Essa mensagem vem por segundo');
}

setTimeout(primeiraMensagem, 3000);
segundaMensagem();

// Output:
// Essa mensagem vem por segundo
// ... 5 segundos depois
// Essa mensagem vem por primeiro
```

_**gif do output**_

O que aconteceu? Se o código é sempre executado de cima para baixo, por que o JavaScript não esperou que a primeira mensagem fosse exibida antes da segunda?

Neste caso o JavaScript leu o código corretamente, executou a ação dos 3 segundos para exibir a mensagem e __continuou a execução de forma síncrona do restante do código__. Ou seja, ele leu `setTimeout`, mandou a execução acontecer e continou a ler a próxima linha de código que neste caso foi `segundaMensagem()`.

Mas esse não é o output que queríamos, certo? Queríamos que `segundaMensagem()` fosse executada somente após `primeiraMensagem()`. E se fizéssemos uma modificação? Vamos incluir `segundaMensagem()` como callback de `primeiraMensagem()` e fazer com que essa callback seja executada 2 segundos depois da execução da primeira.

```Javascript

function primeiraMensagem(callback) {
    console.log('Essa mensagem vem por primeiro');

    setTimeout(callback, 2000);
}

function segundaMensagem() {
    console.log('Essa mensagem vem por segundo');
}

setTimeout(primeiraMensagem(segundaMensagem), 3000);

```

Agora sim. Desta forma `segundaMensagem()` só será executada 2 segundos após a execução de `primeiraMensagem()`. Vamos para o output?\

_**gif do output**_

Ué, o erro de undefined novamente? Se olharmos com atenção notaremos que cometemos um erro fatal. Ao passarmos `segundaMensagem` como callback de `primeiraMensagem`, abrimos os parêtensis de `primeiraMensagem` fazendo com que essa seja executada imediatamente e deixasse de ser passada como callback.

Então como fazer com que ainda que passando `segundaMensagem` como parâmetro, consigamos manter `primeiraMensagem` como callback? Neste caso usaremos as **funções anônimas**, também conhecidas como **arrow functions**.

-----

### Uma rápida explicação de função anônima

Escreverei um artigo em mais detalhes sobre funções anônimas em breve, mas por enquanto só entenda que:

```Javascript
function funcaoNaoAnonima() {
    console.log('Este é um exemplo de uma função não anônima');
}
```
Pode ser transcrita também da seguinte forma:

```Javascript
() => console.log('Este é um exemplo de função anônima');
```
De volta ao assunto.

-----

Utilizando uma função anônima que sua única utilidade será retornar a invocação de `primeiraMensagem`, podemos manter `primeiraMensagem` em sua forma de callback

```Javascript

function primeiraMensagem(callback) {
    console.log('Essa mensagem vem por primeiro');

    setTimeout(callback, 2000);
}

function segundaMensagem() {
    console.log('Essa mensagem vem por segundo');
}

setTimeout(() => primeiraMensagem(segundaMensagem), 3000);

```

Output:

_**gif do output**_

Agora sim! Neste caso a função anônima será a chave para destrancarmos o poder das callbacks. Para mergulhar um pouco mais afundo nessa maravilhosa funcionalidade, iremos adicionar um último degrau de complexidade em nossos exemplos. Dessa vez faremos com que `segundaMensagem` também receba um parâmetro. Neste caso será a mensagem que gostaríamso de imprimir no console.

Primeiro vamos escrever da forma "errada", para entendermos a correta.

```Javascript
function primeiraMensagem(callback) {
    console.log('Essa mensagem vem por primeiro');

    setTimeout(callback, 2000);
}

function segundaMensagem(mensagem) {
    console.log(mensagem);
}

setTimeout(() => primeiraMensagem(segundaMensagem('Essa mensagem vem por segundo')), 3000);
```

Não precisamos nem executar o código acima para vermos o erro de passarmos `segundaMensagem()` com os parênteses, estaremos dando uma ordem de execução e desestruturando a callback. Neste caso também usaremos a função anônima para permitir que passemos um parâmetro dentro de `segundaMensagem()`.

```Javascript
function primeiraMensagem(callback) {
    console.log('Essa mensagem vem por primeiro');

    setTimeout(callback, 2000);
}

function segundaMensagem(mensagem) {
    console.log(mensagem);
}

setTimeout(() => primeiraMensagem(() => segundaMensagem('Essa mensagem vem por segundo')), 3000);
```

Output:

_**gif do output**_

## O problema do uso das Callbacks: O Callback Hell

Através das callbacks, somos capazes de manipular a ordem de execução das funções. Até aqui os exemplos foram simples e didáticos. No entanto, o mundo real é mais complicado e algumas aplicações se tornam complexas.

O uso das callbacks em projetos complexos cria um problema de legibilidade de código e torna seu uso mais difícil. Quer ver? Vamos para um exemplo onde temos 5 funções que imprime mensagem, uma sendo executada 2 segundos depois da outra e recebendo a mensagem como parâmetro. Como essas funções seriam escritas normalmente?

```Javascript
function primeiraMensagem(callback, mensagem) {
    console.log(mensagem);

    setTimeout(callback, 2000);
}

function segundaMensagem(callback, mensagem) {
    console.log(mensagem);

    setTimeout(callback, 2000);
}

function terceiraMensagem(callback, mensagem) {
    console.log(mensagem);

    setTimeout(callback, 2000);
}

function quartaMensagem(callback, mensagem) {
    console.log(mensagem);

    setTimeout(callback, 2000);
}

function quintaMensagem(mensagem) {
    console.log(mensagem);
}

setTimeout(() => primeiraMensagem(
    () => segundaMensagem(
        () => terceiraMensagem(
            () => quartaMensagem(
                () => quintaMensagem('Quinta mensagem'),
            'Quarta mensagem')
        , 'Terceira mensagem')
    , 'Segunda mensagem')
, 'Primeira mensagem'), 3000);
```

Output:

_**gif do output**_

Veja que a medida que são adicionadas novas chamadas de callbacks, a complexidade irá aumentar e a compreensão do código ficará mais difícil. Em casos mais extremos seu código vai parecer que foi cortado ao meio pelo Hadouken do Ryuu.


_**montagem do Ryuu**_

Felizmente existe uma maneira de evitar que esse tipo de problema aconteça. E estamos falando das Promises! E para a conveniência de todos, eu tenho um [artigo explicando o assunto](https://dev.to/alanfabricio/introducao-a-promises-async-await-no-javascript-4pjm) também!

## Conclusão

Ufa! Chegamos ao final e tenho certeza que daqui pra frente Callback é um assunto mais claro para você. Agora é só praticar!

Agradecimentos e crédito à [Ania Kubów](https://www.youtube.com/watch?v=cNjIUSDnb9k) e [Mario Souto](https://youtu.be/6lbBaM18X3g) que também dão excelentes explicações acerca do assunto.

Teve algum problema? Comenta aqui em baixo!

Se este link foi útil pra você ou você quer apoiar o meu trabalho,
deixa seu like aí e compartilhe ❤️

![Deixa seu like aí!!!](https://media.giphy.com/media/fAVOVstMKzWEOgl4gV/giphy.gif)
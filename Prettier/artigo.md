# Adicionando o Prettier ao seu projeto JavaScript/TypeScript

Uma das maiores dificuldades de quem está iniciando em programação é o uso correto de nomenclaturas, regras de sintaxe e desatenção a detalhes que podem acabar sacrificando o seu tempo de estudo em busca de correções de escrita e erros de digitação errada.

Felizmente, existe uma maneira de automatizar o seu projeto para que a sua IDE faça essas correções automaticamente, salvando um tempo precioso de digitação. E a ferramenta para isso é o **Prettier**.

Através dele, podemos configurar regras específicas de como a sintaxe do seu código deve se comportar, corrigindo automaticamente eventuais erros e criando uma padronização de regras que devem ser seguidas, independente de quem esteja trabalhando no projeto.

Vejamos um exemplo. Podemos estabelecer as seguintes regras:

```Javascript
{
    "semi": true, // As declarações devem terminar com semicolon (ponto e vírgula ;)
    "singleQuote": true, // Strings devam utilizar por padrão aspas simples
}
```

Com estas regras, a partir da declaração seguinte, o Prettier poderá fazer a formatação automática do seu código:

```Javascript
const variavelAntes = "variável antes do Prettier"

const variavelDepois = 'variável depois do Prettier';

```

Podemos utilizar o Prettier com uma certa profundidade, trazendo um leque de regras que irá nos ajudar a deixar nosso código padronizado e, como o próprio nome sugere, mais bonito. Então vamos botar a mão na massa e configurar essa belezinha no nosso projeto.

## Pré-requisitos

- VSCode: Usaremos as configurações do Prettier no VSCode, então fique esperto para configurar caso você utilize outra IDE
- Um projeto Node com `package.json` em Javascript ou Typescript
- `npm` ou `yarn` instalado

## Instalação

Adicionaremos o Prettier como uma dependência de desenvolvimento. Podemos fazer isso utilizando o comando `npm`:

> npm install -D prettier

Ou `yarn`:

> yarn add -D prettier

Dica: Para evitar conflito na instalação de pacotes, sempre use somente um dos dois comandos. Evite misturar o `yarn` e o `npm` no seu projeto pois cada gerenciador de pacotes irá criar o seu próprio arquivo `lock`.

Em outras palavras, se escolher o `yarn`, evite ter o arquivo `package-lock.json` no projeto (pode deletar sem medo). Se escolher o `npm`, evite ter o arquivo `yarn.lock`.

Caso o Prettier tenha sido adicionado com sucesso no seu projeto, seu arquivo `package.json` deve ter o pacote do Prettier nas dependências de desenvolvimento:

```javascript
"devDependencies": {
  "prettier": "^2.8.3"
}
```

## Setup inicial do Prettier

Agora que nos certificamos de ter o pacote instalado no nosso projeto, inseriremos as primeiras regras de sintaxe. Para isso, devemos criar um arquivo chamado `.prettierrc` na raíz do projeto.

Vamos inserir algumas regras básicas nele:

```javascript
{
    "semi": true,
    "singleQuote": true,
    "printWidth": 80,
    "tabWidth": 2,
    "bracketSpacing": true
}
```

O que cada uma dessas regras fazem?

- semi - Insere ponto e vírgula ao final de declarações
- singleQuote - Strings devem ser incluídas por padrão em aspas simples
- printWidth - Especifica o tamanho máximo de linha no código
- tabWidth - As tabulações terão por padrão um espaçamento de tamanho 2
- bracketSpacing - Valores dentro de chaves (`{}`) virão espaçados

Você pode conferir essas e outras regras nas [documentações do Prettier](https://prettier.io/docs/en/index.html)

## Usando o Prettier através da linha de comando

Já temos tudo pronto para testar o funcionamento do Prettier. Se você está adicionando o Prettier a um projeto já existente, você pode rodar o comando diretamente e ver se ele funciona de acordo com as regras que você estabeleceu. Mas caso esteja começando um projeto novo e fazendo o setup do Prettier, iremos testar criando um arquivo em `src/index.js`.

É um arquivo simples para testar as configurações do Prettier. Iremos inserir apenas o seguinte código:

```javascript
const testPrettier = { message: "this is a test for the prettier" };
```

Para que o Prettier faça sua mágica, adicionaremos o comando de correção no nosso arquivo `package.json`. Caso não haja o objeto `scripts`, use o exemplo abaixo para adicionar no seu `package.json`. Mas caso já possua, só adicione o comando `format`:

```javascript
{
    "scripts": {
        ...
        "prettier-format": "prettier --write 'src/**/*.{js,jsx,ts,tsx,css,json}' --config ./.prettierrc"
    }
}
```

Agora execute o comando usando o seu gerenciador de pacotes:

- npm:

  > npm run prettier-format

- yarn
  > yarn prettier-format

Olhando novamente para o arquivo `src/index.js`, a nossa variável deverá estar formatada assim:

```javascript
const testPrettier = { message: "this is a test for the prettier" };
```

Voilá! Temos nosso código formatado do jeitinho que queríamos. Mas não acaba por aí porque o tópico a seguir vai mudar a sua vida!

## Usando o Prettier através do VSCode diretamente

Até então, o que foi feito aqui já é uma grande ajuda em termos de correção de sintaxe e padronização de código. Mas a maior vantagem do Prettier vem agora: A integração com o VSCode!

Através dela, o código _será formatado automaticamente sem a necessidade do uso de comandos_. Isso mesmo. Então vamos por a mão na massa e ver o funcionamento na prática.

O primeiro passo para fazer essa integração é ir na aba de extensões do VSCode (penúltimo ícone ou apenas Cmd + Shift + X ou CTRL + Shift + X) e procurar pela extensão do Prettier. Basta instalar e ela será adicionada ao seu VSCode.

<img src="https://github.com/alantsx/Artigos/blob/main/Prettier/resouces/asset1.png?raw=true" alt="callback gif 4" style="height: 350px;"/>

Muitas pessoas que estão iniciando na programação e utilizam o VSCode ainda abrem os seus projetos da maneira tradicional, indo pelo menu de Arquivo e abrir uma pasta. No entanto, a medida que vamos tendo mais projetos e trabalhando cada vez mais com programação, essa acaba sendo uma maneira menos prática, e como desenvolvedores nós sempre estamos tentando encontrar uma maneira de fazer as coisas melhores, por mais simples que sejam. Por isso, uma das formas mais práticas de se abrir diferentes projetos pelo VSCode é através da linha de comando, e hoje vou te mostrar como.

    Disclaimer: Fiz este tutorial para usuários de Windows, se você usa outro sistema operacional, o método é similar mas provavelmente será diferente em algum ponto.


### Utilizando comando code
O comando `code` permite abrir um arquivo ou pasta no terminal, para isso, basta digitar `code caminho_do_arquivo_ou_pasta` e o VSCode irá abrir automaticamente no arquivo/pasta selecionado. Neste sentido, o que eu costumo fazer é navegar via Explorer até a pasta que eu quero, e só assim a partir daí abrir um terminal na pasta desejada (usando shift + botão direito e abrindo o Power Shell). A partir daí eu aplico o comando `code .`. Veja um exemplo:

<img src="https://github.com/alantsx/Artigos/blob/main/add-code-to-path-windows/assets/opening_vscode.gif?raw=true" alt="opening vscode" style="height: 350px;"/>

### Mas eu tenho o comando code?

Se você ainda não adicionou o comando do VSCode pelo seu terminal ou não sabe se o adicionou, para verificar é muito simples. Abra uma pasta de um projeto qualquer e tente digitar o comando `code .` no terminal. 

Caso você não tenha o comando instalado no seu terminal, uma mensagem de erro deve aparecer. Segue um exemplo usando o Windows:

<img src="https://github.com/alantsx/Artigos/blob/main/add-code-to-path-windows/assets/usando_comando_code_sem_o_path.gif?raw=true" alt="code command error" style="height: 350px;"/>

#### Adicionando o comando code

Existem algumas maneiras de instalar esse comando para ser usado direto no seu terminal. A primeira dela é apresentada da forma mais óbvia: no próprio instalador. Quando instalamos o VSCode (pelo menos no Windows, não sei nos outros SO), é só você marcar a opção “Add to path”.

<img src="https://github.com/alantsx/Artigos/blob/main/add-code-to-path-windows/assets/addtopath.png?raw=true" alt="add to path option from installer" style="height: 350px;"/>

Desta forma, da próxima vez que você abrir o seu terminal de preferência, o comando code estará pronto para ser usado.

_**Caso esse comando não apareça:**_  Fiz alguns testes e pesquisas, e pelo Windows, parece que o VSCode não fornece mais a opção de adicionar esse comando ao path posteriormente. Portanto recomendo salvar todas as suas configurações na nuvem através da sincronização de opções, permitindo que você desinstale o VSCode e reinstale-o sem perder nada.

<img src="https://github.com/alantsx/Artigos/blob/main/add-code-to-path-windows/assets/settingsync.jpeg?raw=true" alt="setting sync on vscode"/>

-----
Finalmente, desta forma você agora conseguirá abrir os seus arquivos e projetos de forma muito mais rápida e eficiente no VSCode. E aí, sabia dessa? Se foi útil, deixa um ❤️

<img src="https://media.giphy.com/media/o9C3VLpwpkk5VaXMlT/giphy.gif" alt="Bye"/>

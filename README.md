# numero-secreto
Projeto desenvolvido juntamente com a escola Alura. Esse projeto consiste em um jogo de reconhecimento de voz, onde o jogo sorteará um número secreto e usuário terá que chutar um número, buscando acertar o numero secreto. E para esse reconhecimento de chute, foi utilizado reconhecimento de voz.

## Aplicando estilos no JavaScript

- **Iniciando o Projeto**
    
    ```html
    <!DOCTYPE html>
    <html lang="pt-br">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Número Secreto</title>
        <!-- Reset CSS: Elimina as estilizações impostas pelo próprio navegador aos elementos -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/meyer-reset/2.0/reset.min.css" integrity="sha512-NmLkDIU1C/C88wi324HBc+S2kLhi08PN5GDeUVVVC/BVt/9Izdsc9SVeVfA1UZbY3sHUlDSyRXhCzHfr6hmPPw==" crossorigin="anonymous" referrerpolicy="no-referrer" />
        <!-- Font Awesome: Importa icones para serem utilizados no código -->
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css" integrity="sha512-z3gLpd7yknf1YoNbCzqRKc4qyor8gaKU1qmn+CShxbuBusANI9QpRohGBreCFkKxLhei6S9CQXFEbbKuqLg0DA==" crossorigin="anonymous" referrerpolicy="no-referrer" />
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <h1>Acerte o número secreto</h1>
    
        <h3>O número secreto está entre <span id="menor-valor">0</span> e <span id="maior-valor">100</span></h3>
    
        <div id="chute" class="mensagem">
            <div>Você disse:</div>
            <span class="box">20</span>
            <div>O número secreto é maior <i class="fa-solid fa-up-long"></i></div>
        </div>
    </body>
    </html>
    ```
    

Iniciamos o projeto com a base `HTML`, e aqui adicionamos alguns elementos padrões que logo mas serão manipulados por meio do `**JavaScript**`. Também podemos ver a importação do `ResetCSS` e do `Font Awesome`.

- **Escolhendo fontes e cores**
    
    ```css
    @import url('https://fonts.googleapis.com/css2?family=Archivo+Black&family=Bebas+Neue&family=Lilita+One&family=Montserrat&family=Roboto&display=swap');
    
    :root {
        --font-family: 'Montserrat', sans-serif;
        --primary-color: #E8F9FD;
        --bg-color: #0AA1DD;
    }
    ```
    

Partindo para estilização do projeto, importamos a fonte `Montserrat` no `CSS` e adicionamos algumas variáveis utilizando `:root`, como fonte padrão, cor primaria e cor de fundo.

- **Aplicando cores e posicionando elementos**
    
    ```css
    @import url('https://fonts.googleapis.com/css2?family=Archivo+Black&family=Bebas+Neue&family=Lilita+One&family=Montserrat&family=Roboto&display=swap');
    
    :root {
        --font-family: 'Montserrat', sans-serif;
        --primary-color: #E8F9FD;
        --bg-color: #0AA1DD;
    }
    
    body {
        background-color: var(--bg-color);
        color: var(--primary-color);
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        text-align: center;
        margin: 0;
        font-family: var(--font-family);
    }
    
    h1 {
        font-size: 5em;
    }
    
    h3 {
        font-size: 2em;
        margin-top: 20px;
    }
    
    .mensagem {
        font-size: 1.5em;
        margin-top: 40px;
    }
    
    .box {
        border: 1px solid var(--primary-color);
        display: inline-block;
        font-size: 4em;
        padding: 10px;
        margin: 20px;
    }
    ```
    

Nessa etapa do projeto, estilizamos o projeto por completo com cores, tamanho de fonte, posições dos elementos e espaçamentos, a partir de agora partiremos para o `JavaScript`, para a manipulação dos elementos.

## Aplicando a função Math.random

- **Número aleatório com Math.randon**
    
    ```jsx
    const numeroSecreto = gerarNumeroSecreto();
    
    function gerarNumeroSecreto() {
        return Math.round(Math.random() * 100)
    }
    
    console.log('Numero Secreto: ', numeroSecreto)
    ```
    

> O **`Math.random()`**método estático retorna um número pseudoaleatório de ponto flutuante que é maior ou igual a 0 e menor que 1, com distribuição aproximadamente uniforme nesse intervalo — que você pode então dimensionar para o intervalo desejado.
> 

> O **`Math.round()`**método estático retorna o valor de um número arredondado para o número inteiro mais próximo.
> 

Prosseguindo com o código, chegou a hora de sortearmos o número secreto e para isso utilizaremos o `Math.random`, então criamos a função `gerarNumeroSecreto` e dentro dela retornamos um `Math.random` com a condição de ir até 100 e passamos também o `Math.round` que nos dará um número inteiro. Por fim, imprimos esse número sorteado com o `console.log`.

- **Manipulando menor e maior valor**
    
    ```jsx
    const menorValor = 1;
    const maiorValor = 1000;
    
    const elementoMenorValor = document.getElementById('menor-valor').innerHTML = menorValor;
    const elementoMaiorValor = document.getElementById('maior-valor').innerHTML = maiorValor;
    
    const numeroSecreto = gerarNumeroSecreto();
    
    function gerarNumeroSecreto() {
        return Math.round(Math.random() * maiorValor + 1)
    }
    
    console.log('Numero Secreto: ', numeroSecreto)
    ```
    

Nessa etapa, criamos ás variáveis que indicara o menor valor que receberá 1 e o maior valor que receberá 1000. Porém, precisamos deixar isso dinâmico de forma que substitua os valores padrões que estão inseridos no `HTML`, então, criamos mais duas variáveis, são elas `elementoMenorValor` e `elementoMaiorValor`, elas armazenarão o elemento do `HTML` identificado com `id` `“menor-valor”` e `“maior-valor”`, e passaremos um `innerHTML` que será responsável pela substituição dos valores.

## Definindo a voz com Web Speech

- **Web speech API**
    
    ```jsx
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    
    const recognition = new SpeechRecognition();
    recognition.lang = 'pt-br';
    recognition.start();
    ```
    

> A sigla `API` deriva da expressão inglesa *`Application Programming` Interface* que, traduzida para o português, pode ser compreendida como uma interface de programação de aplicação. Ou seja, API é um conjunto de normas que possibilita a comunicação entre plataformas por meio de uma série de padrões e protocolos.
> 
> 
> Por meio de APIs, desenvolvedores podem criar novos softwares e aplicativos capazes de se comunicar com outras plataformas. Por exemplo: caso um desenvolvedor queira criar um aplicativo de fotos para Android, ele poderá ter acesso à câmera do celular através da API do sistema operacional, sem ter a necessidade de criar uma nova interface de câmera do zero.
> 

Aqui conhecemos a `API` de reconhecimento de voz, por meio do link:

https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API/Using_the_Web_Speech_API

Importamos ela no nosso novo arquivo de `JavaScript` chamado `reconhecimentoDeVoz`, inicializamos ela em uma variável chamada `recognition`, utilizando o `lang` alteramos seu idioma para português com `“pt-br”` e demos um `start` que é uma função nativa do JS.

- **Exibindo a mensagem no console**
    
    ```jsx
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    
    const recognition = new SpeechRecognition();
    recognition.lang = 'pt-br';
    recognition.start();
    
    recognition.addEventListener('result', onSpeak);
    
    function onSpeak(e) {
        console.log(e.results[0][0].transcript);
    }
    ```
    

Nessa etapa do código, utilizamos o `addEventListener` e utilizamos o evento `result`, chamando a função `onSpeak`, essa função irá escutar o que for falado, fará o caminho até chegar ao local onde essa informação está armazenada e exibirá no `console`.

- **Mostrando a mensagem na tela**
    
    ```jsx
    const elementoChute = document.getElementById("chute");
    
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    
    const recognition = new SpeechRecognition();
    recognition.lang = 'pt-br';
    recognition.start();
    
    recognition.addEventListener('result', onSpeak);
    
    function onSpeak(e) {
        chute = e.results[0][0].transcript;
        exibeChuteNaTela(chute);
    }
    
    function exibeChuteNaTela(chute) {
        elementoChute.innerHTML = `
            <div>Você disse</div>
            <span class="box">${chute}</span>
        `
    }
    ```
    

Para mostrar o que foi falado na tela de forma dinâmica, criamos uma variável chamada `elementoChute` e nela armazenamos o elemento do `HTML` identificado com o `id “chute”`. Criamos também uma nova função chamada `exibeChuteNaTela` que terá como parâmetro o chute e dentro da função passaremos o `innerHTML` para `elementochute`, onde criamos o elemento por meio do próprio JS, dessa forma, deixaremos o projeto mais dinâmico.

## Criando a lógica do jogo

- **Validações**
    
    ```jsx
    function verificaSeOChutePossuiUmValorValido() {
        const numero = +chute;
    
        if(chuteForInvalido(numero)) {
            console.log('Valor inválido!');
        }
    
        if (numeroForMaiorOuMenorQueOValorPermitido(numero)) {
            console.log(`Valor inválido: o número secreto precisa estar entre ${menor-Valor} e ${maiorValor}`);
        }
    }
    
    function chuteForInvalido(numero) {
        return Number.isNaN(numero);
    }
     
    function numeroForMaiorOuMenorQueOValorPermitido(numero) {
        return numero > maiorValor || numero < menorValor;
    }
    ```
    

Chegamos na parte de implementar a lógica. De inicio criamos um novo arquivo chamado `validacao.js`, nesse novo arquivo, criamos uma função chamada `verificaSeOChutePossuiUmValorValido` e dentro dessa função, fizemos algumas validações como por exemplo: 

- Identificar se o numero de chute é inválido: Com a condição `if` que puxará a função `chuteForInvalido`, ou seja, caso aqui o `chute` não for um número, aparecerá a mensagem no `console “Valor Inválido”`;
- Verificar se o número está dentro do intervalo: Nesse caso, temos outra condição `if`, que puxará a função `numeroForMaiorOuMenorQueOValorPermitido`, essa função, verifica se o `chute` é maior que o `maiorValor` ou menor que o `menorValor`, caso essa condição for verdadeira o usuário terá a seguinte mensagem em seu `console “Valor inválido: o número secreto precisa estar entre ${menor-Valor} e ${maiorValor}”.`
- **Acertando o número secreto**
    
    ```jsx
    function verificaSeOChutePossuiUmValorValido() {
        const numero = +chute;
    
        if(chuteForInvalido(numero)) {
            elementoChute.innerHTML += '<div>Valor inválido!</div>';
        }
    
        if(numeroForMaiorOuMenorQueOValorPermitido(numero)) {
            elementoChute.innerHTML += `<div>Valor inválido: Fale um número entre ${menor-Valor} e ${maiorValor}</div>`;
        }
        
        if(numero === numeroScreto) {
            document.body.innerHTML = `
                <h2>Você acertou!</h2>
                <h3>O número secreto era ${numeroSecreto}</h3>
            `
        }
    }
    
    function chuteForInvalido(numero) {
        return Number.isNaN(numero);
    }
     
    function numeroForMaiorOuMenorQueOValorPermitido(numero) {
        return numero > maiorValor || numero < menorValor;
    }
    ```
    

Se executarmos o código, veremos as mensagens de validações que criamos anteriormente estão sendo imprimidas somente no `console`, então, devemos mostrar essas mensagens na tela. Para isso voltaremos ao arquivo `reconhecimentoDeVoz.js`, pegaremos o `elemento.HTML` e no arquivo atual `validação.js`, substituiremos o `console.log`, lembrando que estamos criando um elemento `HTML`, nesse caso devemos envolver a mensagem entre uma `div`.

Por fim, teremos outra validação, nessa verificaremos se o `chute` foi igual ao `numeroSecreto`, caso essa condição `if` for verdadeira, criaremos uma animação que resultará em uma nova tela e terá como mensagem `“Você acertou!”`.

- **Criando as dicas**
    
    ```jsx
    function verificaSeOChutePossuiUmValorValido() {
        const numero = +chute;
    
        if(chuteForInvalido(numero)) {
            elementoChute.innerHTML += '<div>Valor inválido!</div>';
            return;
        }
    
        if(numeroForMaiorOuMenorQueOValorPermitido(numero)) {
            elementoChute.innerHTML += `<div>Valor inválido: Fale um número entre ${menor-Valor} e ${maiorValor}</div>`;
            return;
        }
        
        if(numero === numeroSecreto) {
            document.body.innerHTML = `
                <h2>Você acertou!</h2>
                <h3>O número secreto era ${numeroSecreto}</h3>
            `  
        } else if (numero > numeroSecreto) {
            elementoChute.innerHTML += `
            <div>O número secreto é menor <i class="fa-solid fa-down-long"></i></div> -->
            `
        } else {
            elementoChute.innerHTML += `
            <div>O número secreto é maior <i class="fa-solid fa-up-long"></i></div> -->
            `
        }
    }
    
    function chuteForInvalido(numero) {
        return Number.isNaN(numero);
    }
     
    function numeroForMaiorOuMenorQueOValorPermitido(numero) {
        return numero > maiorValor || numero < menorValor;
    }
    ```
    
    ```jsx
    const elementoChute = document.getElementById("chute");
    
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    
    const recognition = new SpeechRecognition();
    recognition.lang = 'pt-br';
    recognition.start();
    
    recognition.addEventListener('result', onSpeak);
    
    function onSpeak(e) {
        chute = e.results[0][0].transcript;
        exibeChuteNaTela(chute);
        verificaSeOChutePossuiUmValorValido(chute);
    }
    
    function exibeChuteNaTela(chute) {
        elementoChute.innerHTML = `
            <div>Você disse</div>
            <span class="box">${chute}</span>
        `
    }
    
    recognition.addEventListener('end', () => recognition.start());
    ```
    

Para finalizar mais uma etapa, chegou a hora de criar as dicas. De inicio passamos um `return` na validações de `chuteForInvalido` e `numeroForMaiorOuMenorQueOValorPermitido`, casos essas condições forem verdadeiras o jogo retornará a mensagem e fim.

E partimos para a criação das dicas, então já tínhamos uma condição `if` que comparava o `chute` ao `numeroSecreto`, precisamos agora criar outra condição, dessa vez `else if` essa condição verificará se o numero é maior que o `numeroSecreto`, caso a condição for verdadeira, aparecerá na tela a mensagem `“o número secreto é menor”`, caso `if` e o `else if` seja falso, cairá na última condição o `else` que terá como mensagem  `“o número secreto é maior”`.

Se executarmos o código, veremos que após chutar um número, teremos a dica e fim. Porém queremos chutar um número até acertar o número secreto, para isso precisamos criar um evento de reinicio, então voltaremos ao arquivo `reconhecimentodeVoz.js` e com `add.EventListener`, passaremos o evento `‘end’` que significa fim, e quando esse evento for acionado, reiniciaremos o `recognition` com a função `start` nativa do JS.

## Publicano e Compartilhando

- **Criando o botão jogar novamente**
    
    ```jsx
    function verificaSeOChutePossuiUmValorValido() {
        const numero = +chute;
    
        if(chuteForInvalido(numero)) {
            elementoChute.innerHTML += '<div>Valor inválido!</div>';
            return;
        }
    
        if(numeroForMaiorOuMenorQueOValorPermitido(numero)) {
            elementoChute.innerHTML += `<div>Valor inválido: Fale um número entre ${menor-Valor} e ${maiorValor}</div>`;
            return;
        }
        
        if(numero === numeroSecreto) {
            document.body.innerHTML = `
                <h2>Você acertou!</h2>
                <h3>O número secreto era ${numeroSecreto}</h3>
    
                <button id="jogar-novamente" class"btn-jogar">Jogar Novamente</button>
            `  
        } else if (numero > numeroSecreto) {
            elementoChute.innerHTML += `
            <div>O número secreto é menor <i class="fa-solid fa-down-long"></i></div> -->
            `
        } else {
            elementoChute.innerHTML += `
            <div>O número secreto é maior <i class="fa-solid fa-up-long"></i></div> -->
            `
        }
    }
    
    function chuteForInvalido(numero) {
        return Number.isNaN(numero);
    }
     
    function numeroForMaiorOuMenorQueOValorPermitido(numero) {
        return numero > maiorValor || numero < menorValor;
    }
    
    document.body.addEventListener('click', e => {
        if(e.target.id == 'jogar-novamente') {
            window.location.reload()
        }
    });
    ```
    

Pra finalizar o projeto do Numero secreto, a gente criará um botão para dar reinicio ao jogo. Então voltamos na condição se numero chutado for igual ao numero secreto, ou seja, se o usuário estiver acertado o número secreto, iremos criar um elemento de botão que terá o `id “jogar-novamente”`, uma `class “btn-jogar”` e como texto apresentará “Jogar Novamente”. Após criarmos o elemento, vamos ao `style.css`, estiliza-lo, para deixa-lo bonito.

E por fim, adicionamos um `addEventListener` com evento de `click` no botão e passamos um `window.loation.reload`, esse comando realizará o reinicio do jogo.

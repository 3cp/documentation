# Iniciando
**Bem-vindo ao Aurelia!** Este tutorial ir� guia-lo atrav�s da cria��o de um aplicativo simples usando Aurelia e explicar brevemente os seus principais conceitos. Estamos supondo que voc� j� esteja familiarizado com JavaScript, HTML e CSS. Para ter uma vis�o geral, recomendamos que voc� v� at� a se��o "Configura��o da p�gina HTML" para que voc� possa ver como usar Aurelia imediatamente. Ent�o, quando voc� estiver pronto para realmente construir algo, volte e leia a se��o "Configurando Seu Ambiente" e "Configurando a Estrutura do Projeto". Para ver os resultados completos de este tutorial, por favor, d� uma olhada no [nosso projeto esqueleto de navega��o] (https://github.com/aurelia/skeleton-navigation/releases).

> **Note:** Looking for this guide in another language? Have a look in our [documentation repo](https://github.com/aurelia/documentation).

## Configurando Seu Ambiente
Vamos come�ar configurando um grande conjunto de ferramentas que voc� pode usar para construir aplica��es modernas em JavaScript. Todas as ferramentas que usaremos s�o constru�das sobre [Node.js] (http://nodejs.org/). Se voc� j� o tiver instalado, �timo! Se n�o, voc� deve ir ao [site oficial] (http://nodejs.org/), fa�a o download e instale-o. Todo o resto que iremos precisar ser� instalado via gerenciador de pacotes do Node ([npm] (https://docs.npmjs.com/getting-started/what-is-npm)). Se voc� j� tiver o npm instalado, certifique-se que voc� tem a [�ltima vers�o] (https://github.com/npm/npm/wiki/Troubleshooting#try-the-latest-stable-version-of-node) para evitar quaisquer problemas com as outras ferramentas.

Primeiro, vamos come�ar instalando o [Gulp] (http://gulpjs.com/) que iremos usar para automa��o de compila��o. Se voc� ainda n�o o tem, vamos utilizar o npm para instala-lo, usando os comandos abaixo (pode ser que voc� precise usar `sudo`):

  ```shell
  npm install -g gulp
  ```

Em seguida, � preciso instalar o [jspm] (http://jspm.io/). Ele ir� servir como o nosso gerenciador de pacotes client-side. Voc� pode instala-lo desta forma:
  ```shell
  npm install -g jspm
  ```

> **Nota:** jspm, assim como Bower e Yeoman, funcionam via [git] (http://git-scm.com/), isso quer dizer voc� deve instala-lo caso ainda n�o o tenha. Al�m disso, o jspm consulta o GitHub para instalar pacotes, mas o GitHub tem um limite de pedidos an�nimos na API. � aconselh�vel que voc� configure o jspm utilizando suas credenciais GitHub a fim de evitar problemas. Voc� pode fazer isso executando o comando `jspm registry config github` e ent�o seguir as instru��es. N�o quer usar o jspm? Sem problemas. Todos os pacotes do Aurelia est�o dispon�veis atrav�s do [Bower] (http://bower.io/) tamb�m.


## Configurando a Estrutura do Projeto

Com o conjunto de ferramentas instalada, podemos voltar a nossa aten��o para a cria��o de uma estrutura b�sica para seu aplicativo. Comece [baixando o esqueleto de navega��o] (https://github.com/aurelia/skeleton-navigation/releases). Descompacte-o e mude o nome da pasta para _navigation-app_.

> **Nota:** Como alternativa, voc� pode usar o [Yeoman] (http://yeoman.io) para "gerar" o projeto esqueleto de navega��o na pasta de destino, desta forma:
>
> ```
> npm install -g yo generator-aurelia
> yo aurelia
> ```

Dentro da pasta voc� vai encontrar tudo que voc� ir� precisar, incluindo uma compila��o base, configura��o de pacotes, estilos e muito mais.
Voc� pode verificar que existe um arquivo _index.html_ e alguns outros dentro da pasta _src_, no entanto, recomendamos que voc� exclua estes arquivos antes de avan�ar com este tutorial. Dessa forma, voc� aprender� de uma forma eficaz como construir um aplicativo do zero usando o Aurelia.

Com tudo o que precisamos pronto, vamos executar alguns comandos.

1. Abra um console e navegue at� o diret�rio da pasta _navigation-app_ que criamos recentemente.
2. Execute o seguinte comando para instalar os plugins Gulp que est�o listados na se��o _devDependencies_ do arquivo de manifesto do pacote.

  ```shell
  npm install
  ```

3. Em seguida, execute o seguinte comando para instalar a biblioteca do Aurelia, do bootstrap e  do font-awesome, listados na se��o _jspm.dependencies_ de arquivo de manifesto do pacote.

  ```shell
  jspm install -y
  ```

Tudo o que fizemos at� agora � puro Node.js, procedimentos de construl�ao e de gerenciamento de pacotes. Ele n�o tem nada espec�fico para com o Aurelia. Estamos apenas exibindo os passos da cria��o de um projeto moderno em JavaScript, a partir do zero. Voc� pode j� estar familiarizado com isso, mas caso ainda n�o esteja, seja bem-vindo a este mundo novo e excitante!

> ** Nota: ** Bootstrap e Font-Awesome **n�o** s�o depend�ncias do Aurelia. N�s s� iremos aproveit�-los neste tutorial para poder produzir rapidamente um visual decente para aplica��o.


## Construindo o P�gina HTML

Se voc� chegou at� aqui, voc� tem todas as bibliotecas e ferramentas de constru��o que iremos utilizar para criar um incr�vel aplicativo em JavaScript com Aurelia. A pr�xima coisa a ser feita � criar o arquivo _index.html_ na pasta raiz do projeto. O exemplo abaixo fornece um bom modelo para os aplicativos baseados em Aurelia.

### index.html
```markup
<!doctype html>
<html>
  <head>
    <title>Aurelia</title>
    <link rel="stylesheet" type="text/css" href="jspm_packages/npm/font-awesome@4.3.0/css/font-awesome.min.css">
    <link rel="stylesheet" type="text/css" href="styles/styles.css">
  </head>
  <body aurelia-app>
    <script src="jspm_packages/system.js"></script>
    <script src="config.js"></script>
    <script>
     System.config({
       "paths": {
         "*": "dist/*.js"
       }
     });
   </script>
    <script>
      System.import('aurelia-bootstrapper');
    </script>
  </body>
</html>
```

Sim, � isso! Esta � a �nica p�gina HTML em nossa aplica��o. O cabe�alho � bastante simples: n�s adicionamos o font-awesome e alguns arquivos CSSs personalizados. Agora, � o corpo da p�gina que � interessante.

> **Nota:** N�o se esque�a de confirmar se o link do arquivo do font-awesome est� correto. � poss�vel que essas bibliotecas tenham atualizado suas vers�es desde a cria��o deste documento.

Vamos come�ar com as tags script. Primeiro temos o _system.js_, nosso carregador de m�dulos baseado em padr�es do ES6. � ele quem carrega a biblioteca do Aurelia, bem como o seu pr�prio c�digo. Em seguida, temos o _config.js_. Ele cont�m a configura��o para o carregador. � gerado automaticamente sempre que voc� executar um comando jspm. O jspm � o gerenciador de pacotes client-side, � recomend�vel que voc� o utilize porque ele fornece uma experi�ncia de desenvolvimento incr�vel atrav�s da integra��o de gerenciamento de pacotes client-side com um m�dulo compat�vel com o carregador do ES6. Depois, temos a execu��o de uma fun��o chamada para `System.config`. Isso configura a localiza��o da sa�da do nosso c�digo JavaScript compilado.

> **Nota:** O Aurelia Framework n�o est� vinculado diretamente ao jspm ou SystemJS. Ele tamb�m oferece suporte a APIs require-style como RequireJS e Dojo Loader. Al�m disso, voc� pode implementar seu pr�prio carregador e lidar com o gerenciamento de pacotes do jeito que quiser. No entanto, achamos que o jspm / SystemJS � a melhor solu��o orientada a ES6 dispon�vel hoje, e � a nossa abordagem recomendada.

Uma vez que temos o nosso carregador de m�dulos e sua configura��o, n�s carregamos o m�dulo `aurelia-bootstrapper` com uma chamada atrav�s da fun��o `System.import`.

Quando o bootstrapper � carregado ele inspeciona o documento HTML procurando por atributos _aurelia-app_. Neste caso, ele vai identificar que o body tem um atributo `aurelia-app`. Isso informa ao bootstrapper para carregar nossa view-model e sua view, convencionalmente localizado nos arquivos _app.js_ e _app.html_ e depois utiliz�-los como uma aplica��o Aurelia no DOM.

Espere um minuto .... N�s n�o temos um _app_ view-model ou view. Hmmm ...  E AGORA !?


## Criando Sua Primeira Tela

No Aurelia, elementos de interface do usu�rio s�o compostos por pares de _view_ e _view-model_. A _view_ � escrita em HTML e � processada no DOM. A _view-model_ � escrita em JavaScript e fornece dados e comportamento para a _view_. O Poderoso _databinding_ do Aur�lia liga os dois peda�os, permitindo que as mudan�as em seus dados sejam refletidas na _view_ e vice-versa. Esta separa��o de interesses � de grande import�ncia para a colabora��o desenvolvedor / projetista, manuten��o, flexibilidade de arquitetura e at� mesmo do c�digo-fonte.

Vamos dar uma olhada em como isso funciona...

Na pasta _src_ crie um arquivo _app.html_ e um _app.js_. Esta � a view e view-model que o bootstrapper estava procurando. Vamos come�ar com a _view-model_ criando uma classe simples para manter um _firstName_ e _lastName_. N�s tamb�m vamos adicionar uma propriedade calculada para _fullName_ e um m�todo de "welcome" a pessoa. Nossa view-model ficar� da seguinte forma:

### app.js

```javascript
export class Welcome{
  heading = 'Welcome to the Aurelia Navigation App!';
  firstName = 'John';
  lastName = 'Doe';

  get fullName(){
    return `${this.firstName} ${this.lastName}`;
  }

  welcome(){
    alert(`Welcome, ${this.fullName}!`);
  }
}
```

O que ... isso a� � JavaScript mesmo?

Sim, isso � JavaScript. Na verdade, � ECMAScript 7 (ES7), a pr�xima vers�o da pr�xima vers�o do JavaScript que introduz muitos recursos novos para a linguagem. Felizmente o arquivo do Gulp que voc� baixou est� configurado com o [Babel] (https://babeljs.io/), um transpilador incr�vel que lhe permite escrever usando o JavaScript do futuro e execut�-lo em navegadores atuais. Agora voc� pode usar m�dulos, classes, lambdas, interpola��o de string e muito mais. Muito massa n�o � mesmo!? Ent�o, como voc� cria uma _view-model_? Voc� cria uma simples classe usando _export_ para que fique acess�vel ao framework. Mel na chupeta!

> **Nota:** Voc� n�o tem que necessariamente usar o Babel ou mesmo ES7 para desenvolver um aplicativo usando o Aurelia. Voc� pode usar linguagens como TypeSript e CoffeeScript ... ou a linguagem dos navegadores de hoje: ES5. Tudo que voc� tem a fazer � seguir o padr�o da linguagem para a cria��o de classes e tudo ir� funcionar. N�s achamos o ES7 incr�vel, e esperamos que voc� o considere como primeira op��o. Para saber mais sobre esta nova vers�o do JavaScript incluindo recursos como exporta��es e classes, recomendamos a leitura do seguinte artigo: [The Babel Learning Guide] (http://babeljs.io/docs/learn-es6/).
Ok. Agora que temos nossa _view-model_ com alguns dados e comportamentos b�sicos, vamos dar uma olhada na sua parceira de crimes... a _view_.

### app.html

```markup
<template>
  <section>
    <h2>${heading}</h2>

    <form role="form" submit.delegate="welcome()">
      <div class="form-group">
        <label for="fn">First Name</label>
        <input type="text" value.bind="firstName" class="form-control" id="fn" placeholder="first name">
      </div>
      <div class="form-group">
        <label for="ln">Last Name</label>
        <input type="text" value.bind="lastName" class="form-control" id="ln" placeholder="last name">
      </div>
      <div class="form-group">
        <label>Full Name</label>
        <p class="help-block">${fullName}</p>
      </div>
      <button type="submit" class="btn btn-default">Submit</button>
    </form>
  </section>
</template>
```

Todas as views est�o contidas dentro da tag `template`. Esta view � um formul�rio b�sico, estilizado com algumas classes do Bootstrap. D� uma olhada nos elementos do formul�rio. Voc� reparou no `value.bind="firstName"`? Este comando faz um bind (v�nculo) entre o _value_ do elemento input e a propriedade _firstName_ da nossa view-model. Toda vez que o valor da propriedade da view-model for atualizado, o elemento em que foi vinculado tamb�m ser� atualizado, e vice-versa. F�cil, n�o?
Existem outras coisas mais interessantes neste exemplo. No �ltimo grupo do formul�rio voc� pode ver esta sintaxe no conte�do HTML: `${fullname}`. Essa � uma interpola��o de string. � um "one-way binding" da view-model para a view, que � automaticamente convertido para uma string e interpolada no documento. Finalmente, d� uma olhada no elemento form do formul�rio. Voc� deve ter observado o: `submit.delegate="welcome()"`. Isto � um binding de evento. Ele utiliza uma t�cnica chamada "event delegation" para vincular o evento _submit_ para que este execute o m�todo _welcome_ sempre que o formul�rio � enviado.

> **Nota:** Se voc� ainda n�o ouviu falar de �event delegation� (delega��o de eventos), � uma t�cnica utilizada para lidar com eventos de forma mais eficiente, anexando um �nico manipulador de eventos ao um n�vel pai, ao inv�s de anexar um manipulador para cada elemento filho.

Bora executar e ver tudo isso em a��o. No console do seu computador, use o seguinte comando para realizar um build e inicializar o servidor.

```shell
gulp watch
```

Agora navegue em [http://localhost:9000/] (http: //localhost:9000/) para ver a nossa aplica��o. Preencha o formul�rio e observe que o FullName � atualizado sempre que os outros campos s�o alterados. Clique no bot�o Submit e veja que o nosso m�todo ser� disparado.

> **Nota:** Se n�o estiver funcionando, tente [atualizar] (https://github.com/npm/npm/wiki/Troubleshooting#try-the-latest-stable-version-of-node) para a �ltima vers�o do NPM.


> **Nota:** O Aurelia tem uma engine de databinding �nica e poderosa, que utiliza t�cnicas adaptativas para escolher a melhor maneira de observar as mudan�as em cada propriedade. Por exemplo, se voc� estiver usando um navegador com suporte ao [Object.observe](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/observe), o _firstName_  e o _lastName_ ser�o observados com essa estrat�gia. Se n�o, n�s iremos gerar getters e setters que loteiam mudan�as para o Micro Task Queue, emulando corretamente comportamento do Object.observe. Uma vez que a propriedade _fullName_ � calculada, ela n�o pode ser observada com qualquer uma destas t�cnicas, neste caso n�s usamos uma t�cnica chamada "dirty checking". Mas, voc� pode, opcionalmente, declarar suas depend�ncias, a fim de permitir-nos a observ�-la corretamente. N�s usaremos a melhor t�cnica dependendo da situa��o e voc� pode at� mesmo criar t�cnicas personalizadas, a fim de "ensinar" o framework como observar tipos especiais de padr�es de modelagem. N�s achamos este recurso muito legal :)

> **Nota:** O comando `.bind` usa o comportamento de bind padr�o para qualquer propriedade. O padr�o � "one-way binding" (model para view) para tudo, exceto os controles de formul�rio, que padr�o � "two-way binding". Voc� sempre poder� substituir isso usando os comandos de bind expl�citos `.one-way`, `.two-way` e `.one-time'. Da mesma forma, voc� pode usar `.delegate` para delega��o evento, mas voc� tamb�m pode usar `.trigger` para anexar diretamente para o elemento desejado.


## Adicionando Navega��o

Como este � um aplicativo de navega��o, que provavelmente deve adicionar mais algumas telas e configurar um client-side router, n�o acha? Vamos come�ar por renomear o nosso _app.js_ e _app.html_ para _welcome.js_ e _welcome.html_ respectivamente. Esta ser� a primeira p�gina de nosso aplicativo. Agora, vamos criar um novo _app.js_ e _app.html_ que servir� como nosso "layout" ou "master-page". A view ir� conter nossa UI de navega��o e um espa�o reservado de conte�do para a p�gina atual e a view-model ter� uma inst�ncia do router, configurado com nossas rotas. Vamos come�ar com a view-model para que voc� possa ver como configurar o router:

### app.js

```javascript
import 'bootstrap';
import 'bootstrap/css/bootstrap.css!';

export class App {
  configureRouter(config, router){
    config.title = 'Aurelia';
    config.map([
      { route: ['','welcome'], name: 'welcome',  moduleId: './welcome',      nav: true, title:'Welcome' }
    ]);

    this.router = router;
  }
}
```

Opa! H� algumas coisas realmente interessantes aqui. Queremos usar o router, por isso, come�amos por criar a nossa classe _App_ implementando callback do `configureRouter`. Voc� pode definir um t�tulo para p�gina, e ent�o mapear suas rotas. Cada rota tem as seguintes propriedades:

* `route`: Este � um padr�o que, quando combinado, far� com que o router navegue para essa rota. Voc� pode usar rotas est�ticas como acima, mas voc� tamb�m pode usar par�metros como: `customer/:id`. H� tamb�m suporte para rotas curingas e par�metros query string. A rota pode ser um padr�o de string �nica ou uma s�rie de padr�es.
* `name`: Este � um nome a ser usado no c�digo ao gerar URLs para a rota.
* `moduleId`: Este � um caminho relativo para a view-model atual que especifica o par de view/view-model que voc� deseja processar para essa rota.
* `title`: Opcionalmente, � poss�vel fornecer um t�tulo para ser usado na gera��o de t�tulo da p�gina.
* `nav`: Se essa rota deve ser inclusa no menu de navega��o, defina este valor como "true" (ou um n�mero que indica ordem de apari��o);

> **Nota:** Voc� notou que n�s usamos o ES6 para importar e carregar os arquivos JavaScript e CSS do Bootstrap?

### app.html

```markup
<template>
  <nav class="navbar navbar-default navbar-fixed-top" role="navigation">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
        <span class="sr-only">Toggle Navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">
        <i class="fa fa-home"></i>
        <span>${router.title}</span>
      </a>
    </div>

    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li repeat.for="row of router.navigation" class="${row.isActive ? 'active' : ''}">
          <a href.bind="row.href">${row.title}</a>
        </li>
      </ul>

      <ul class="nav navbar-nav navbar-right">
        <li class="loader" if.bind="router.isNavigating">
          <i class="fa fa-spinner fa-spin fa-2x"></i>
        </li>
      </ul>
    </div>
  </nav>

  <div class="page-host">
    <router-view></router-view>
  </div>
</template>
```

Seguindo nossa simples conven��o de constru��o do aplicativo, a classe `App` ser� a liga��o de dados para a view acima em _app.html_. Uma grande parte dessa marca��o lida com a configura��o da estrutura de navega��o principal. Voc� j� viu bindings b�sicos e interpola��es de strings, ent�o vamos focar nas novas coisas. D� uma olhada no elemento navbar-nav `ul`. Sua `li` demonstra como usar um repetidor com a seguinte express�o`repeat.for="row of router.navigation"`. Isto ir� criar um `li` para cada item no array `router.navigation`. A vari�vel local � _row_ e voc� pode ver que � utilizada no `li` e nos seus elementos filho.

> **Nota:** A propriedade `navigation` no router � um array preenchido com todas as rotas marcadas como `nav:true` na sua configura��o. A sintaxe `repeat.for` do Aurelia funciona como o `for..of` do padr�o ES6. Assim, voc� pode pensar em um loop sobre a array de rotas, gerando o c�digo necess�rio para cada uma delas.

Ainda sobre os `li` voc� pode ver uma demonstra��o de como usar interpola��o de string para adicionar/remover dinamicamente as classes CSSs. Mais abaixo, h� uma segunda `ul`. Viu o binding em sua �nica filha `li`? `if.bind="router.isNavigating"` Isto condicionalmente adiciona/remove o `li` com base no valor da express�o. 
Convenientemente, o roteador ir� atualizar sua propriedade `isNavigating` sempre que estiver no processo de carregamento da rota.

A �ltima que queremos falar � o elemento `router-view` perto da parte inferior da view. Este representa o local no DOM onde a "p�gina" atual ser� processada, com base no estado do router configurado.

Com tudo isso em mente, v� em frente e inicie o servidor com o comando `gulp watch`. Abra o navegador e d� uma olhada. Voc� deve ver agora uma navega��o principal com uma �nica guia selecionada para a nossa rota "welcome". A view _welcome_ � exibida na �rea de conte�do e funciona da mesma forma como antes. Abra as ferramentas de debug do navegador e d� uma olhada no DOM atual. Voc� vai ver que a view _welcome_ � exibida dentro do `router-view`.

> **Nota:** Se voc� deixou seu o gulp watch task em execu��o, voc� pode ter notado que o seu navegador atualiza automaticamente sempre que voc� realiza alguma altera��o. Isso acontece gra�as ao `browser-sync`, que convenientemente configuramos para voc� como parte da configura��o do gulp.


## Adicionando Uma Segunda P�gina

Bom, tecnicamente j� temos uma aplica��o de navega��o agora..., mas ela n�o � t�o interessante porque h� apenas uma p�gina. Vamos adicionar uma segunda p�gina. Voc� consegue adivinhar como iremos fazer? Eu aposto que sim!

Vamos exibir algumas imagens do Flickr. Para fazer isso, primeiro iremos configurar nosso router para a suposta p�gina:

### app.js (updated)

```javascript
import 'bootstrap';
import 'bootstrap/css/bootstrap.css!';

export class App {
  configureRouter(config, router){
    config.title = 'Aurelia';
    config.map([
      { route: ['','welcome'], name: 'welcome',  moduleId: './welcome',      nav: true, title:'Welcome' },
      { route: 'flickr',       name: 'flickr',   moduleId: './flickr',       nav: true, title:'Flickr' }
    ]);

    this.router = router;
  }
}
```

Se voc� pensou que precisar�amos criar um arquivo _flickr.js_ e _flickr.html_, voc� acertou! Aqui est� a c�digo-fonte que iremos usar:

### flickr.js

```javascript
import {inject} from 'aurelia-framework';
import {HttpClient} from 'aurelia-http-client';

@inject(HttpClient)
export class Flickr{
  heading = 'Flickr';
  images = [];
  url = 'http://api.flickr.com/services/feeds/photos_public.gne?tags=rainier&tagmode=any&format=json';

  constructor(http){
    this.http = http;
  }

  activate(){
    return this.http.jsonp(this.url).then(response => {
      this.images = response.content.items;
    });
  }

  canDeactivate(){
    return confirm('Are you sure you want to leave?');
  }
}
```

H� um monte de coisas legais aqui. Vamos come�ar pelo in�cio. Estamos importando o `HttpClient` do Aurelia. Isso nos permite fazer solicita��es HTTP de uma forma muito simples. Ele n�o est� inclu�do na configura��o padr�o do Aurelia, sendo assim, voc� precisa para instalar o pacote separadamente. Para fazer isso, execute o seguinte comando no console:

```shell
jspm install aurelia-http-client
```

Agora eu imagino que voc� esteja vendo o poder do gerenciador e carregador de pacotes. Voc� simplesmente instala um pacote com o jspm e depois o importa em seu c�digo usando exatamente o mesmo identificador. Voc� pode instalar qualquer coisa do GitHub ou NPM desta forma.

Agora, d� uma olhada no decorador `inject` do ES7? O que isso faz? Bem, o Aur�lia cria os componentes de interface do usu�rio conforme s�o necess�rios para processar a aplica��o. Ele faz isso usando um container de [Dependency Injection] (http://en.wikipedia.org/wiki/Dependency_injection) (Inje��o de Depend�ncia) capaz de fornecer depend�ncias do construtor, como por exemplo, o HttpClient. Como � que o sistema de DI sabe o que deve fornecer? Tudo que voc� tem a fazer � acrescentar o decorador do ES7 `inject` para sua classe, passando uma lista de "types" do qual o qual seu construtor necessita. Deve haver um "type" para cada par�metro do construtor. No exemplo acima, n�s precis�vamos de uma inst�ncia do HttpClient, por isso, acrescentamos o type `HttpClient` no decorador `inject`, em seguida, adicionamos um par�metro correspondente no construtor da classe.

> **Nota:** Se voc� n�o gosta de usar um decorador, neste caso, voc� tamb�m pode utilizar um m�todo est�tico `inject` ou uma propriedade da classe que retorna um array de types que dever�o ser injetados.

Se voc� estiver usando TypeScript >= 1.5, voc� pode adicionar o decorador `@autoinject` � sua classe sem precisar especificar os types necess�rios, mas os types dever�o ser especificados na assinatura do construtor, desta forma:

```javascript
import {autoinject} from 'aurelia-framework';
import {HttpClient} from 'aurelia-http-client';

@autoinject
export class Flickr{
  ...

  constructor(public http:HttpClient){}

  ...
}
```

O Router do Aur�lia reinicia um ciclo de vida na view-model sempre que as rotas mudam. Isto � chamado de "Screen Activation Lifecycle". As view-models podem, opcionalmente, chamar m�todos de dentro e fora da rota, controlando o fluxo de v�rias partes do ciclo de vida da aplica��o. Quando o router estiver pronto, ele ir� chamar o m�todo `activate`, caso este esteja presente. No c�digo acima, n�s usamos este m�todo para chamar a API do Flickr e obter algumas imagens. Observe que n�s retornamos o resultado do pedido http atrav�s do m�todo `activate`. Todos as APIs `HttpClient` retornam um `Promise`. O router ir� detectar um `Promise` e esperar para concluir a navega��o at� que a consulta tenha retornado. Assim, desta forma voc� pode, opcionalmente, for�ar o router a atrasar a exibi��o da p�gina at� que ela esteja preenchida com dados.

H� um segundo m�todo controlador de ciclo de vida utilizado aqui, o `canDeactivate`. O router chama este m�todo antes de sair da navega��o e processar uma nova rota. Isto serve para dar ao usu�rio oportunidade de permitir a continua��o da navega��o, de acordo com um valor booleano retornado. Voc� tamb�m pode retornar um `Promise` para esse valor. O ciclo de vida completo inclui os m�todos `canActivate`, `activate`, `canDeactivate` e `deactivate`.

> **Nota:** Se voc� n�o estiver familiarizado com [Promises] (http://www.html5rocks.com/en/tutorials/es6/promises/), este � um novo recurso do ES6 que foi projetado para melhorar a programa��o ass�ncrona. A `Promise` � um objeto que representa um resultado futuro. Essencialmente, ele representa uma "promessa" para concluir algum trabalho ou para fornecer alguns dados em algum momento no futuro.

### flickr.html

```markup
<template>
    <section>
        <h2>${heading}</h2>
        <div class="row">
        <div class="col-sm-6 col-md-3" repeat.for="image of images">
          <a class="thumbnail">
            <img style="width: 260px; height: 180px;" src.bind="image.media.m"/>
          </a>
        </div>
        </div>
    </section>
</template>
```

A view desta tela � bastante simples. N�o h� nada que voc� n�o tenha visto antes.
Assim que estiver tudo pronto, v� em frente e execute seu aplicativo novamente. Agora voc� deve ver dois itens na barra de navega��o e ser capaz de alternar entre eles. Ihul!

Recapitulando... para adicionar uma p�gina � sua aplica��o:

1. Adicione a configura��o de rota para o router no _app.js_.
2. Adicionar uma view-model.
3. Adicione uma view com o mesmo nome (mas com uma extens�o .html).
4. Comemore \o/.


## Bonus: Criando Um Elemento Personalizado

Olhe para voc�, j� � um vencedor por ter chegado at� aqui! Vejo que voc� est� interessado em aprender alguma coisa extra neste belo dia. Sendo assim, vamos criar um elemento HTML personalizado. Eu acho que um bom candidato para isso � a nossa barra de navega��o. Ela � um monte de HTML em nosso arquivo _app.html_. Por que n�o criar um elemento personalizado `<nav-bar>` para tornar as coisas um pouco mais clara? D� uma olhada no que n�s queremos ser capazes de escrever no final:

### app.html

```markup
<template>
  <require from='./nav-bar'></require>

  <nav-bar router.bind="router"></nav-bar>

  <div class="page-host">
    <router-view></router-view>
  </div>
</template>
```

Esse c�digo faz a requisi��o um elemento `nav-bar`, do arquivo "./nav-bar". Uma vez que este estiver dispon�vel na view, podemos us�-lo como qualquer outro elemento, incluindo bindings de dados para suas propriedades personalizadas (como _router_). Ent�o, como � que chegaremos nesse produto final?
J� adivinhou? Nossas simples conven��es view-model/view tamb�m se aplicam para os elementos personalizados. (Na verdade, neste tempo todo voc� foi criando o que �s vezes chamamos de elementos personalizados "an�nimos"... voc� simplesmente n�o percebeu.) Vamos criar um _nav-bar.js_ e um _nav-bar.html_. Primeiro, o c�digo para a view-model:

### nav-bar.js

```javascript
import {bindable} from 'aurelia-framework';

export class NavBar {
  @bindable router = null;
}
```

Para criar um elemento personalizado, voc� cria e exporta uma classe. Uma vez que esta classe vai ser usada no HTML como um elemento, precisamos dizer ao framework quais propriedades da classe devem aparecer como atributos no elemento. Para fazer isso, usamos o decorador _bindable_. Como _inject_, _bindable_ � uma maneira de fornecer informa��es sobre a sua classe para a framework do Aurelia. O Aurelia � inteligente e pode fazer muitas coisas sozinho, mas quando ele n�o pode ou quando voc� quer fazer algo diferente de suas conven��es, voc� tem que fornecer algumas informa��es adicionais atrav�s de decoradores. O decorador `bindable` diz ao framework que queremos que propriedade `router` da nossa classe seja atributo no HTML. Uma vez que a propriedade se torna um atributo, podemos utiliza-la na view.

### nav-bar.html

```markup
<template>
  <nav class="navbar navbar-default navbar-fixed-top" role="navigation">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
        <span class="sr-only">Toggle Navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">
        <i class="fa fa-home"></i>
        <span>${router.title}</span>
      </a>
    </div>

    <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
      <ul class="nav navbar-nav">
        <li repeat.for="row of router.navigation" class="${row.isActive ? 'active' : ''}">
          <a href.bind="row.href">${row.title}</a>
        </li>
      </ul>

      <ul class="nav navbar-nav navbar-right">
        <li class="loader" if.bind="router.isNavigating">
          <i class="fa fa-spinner fa-spin fa-2x"></i>
        </li>
      </ul>
    </div>
  </nav>
</template>
```

Isto � praticamente id�ntico ao HTML do navbar orginal que estava em nosso arquivo _app.html_. N�s basicamente extra�mos o c�digo e colocamos dentro de um "template". Ao inv�s de fazer o "bind" com o _app.js_, estamos fazendo no _nav-bar.js_. Este � um elemento personalizado muito simples com nenhum comportamento real, mas � completo e utiliz�vel como mostrado acima. Mais uma vez, o c�digo final do _app.html_:

### app.html

```markup
<template>
  <require from='./nav-bar'></require>

  <nav-bar router.bind="router"></nav-bar>

  <div class="page-host">
    <router-view></router-view>
  </div>
</template>
```

Recapitulando: Em primeiro lugar, temos um elemento `require`. O Aurelia utiliza isso para carregar o elemento personalizado atrav�s da fonte relativa indicada no atributo `from`. Ele est� seguindo nossas conven��es, assim ele vai saber como carregar nossos arquivos _nav-bar.js_ e _nav-bar.html_. Qualquer coisa necess�ria para uma view deve ser declarada no local. Como resultado, voc� n�o precisa se preocupar com conflitos de nome. O segundo ponto � o uso do elemento de binding de dados que utilizado. Estamos "enviando" a inst�ncia do router da nossa classe `App` por meio da propriedade correspondente no elemento `NavBar`, para que ent�o possa ser acessado internamente. Massa, n�o �!?

> **Nota:** Voc� tamb�m pode carregar elementos de toda aplica��o, e tamb�m outros comportamentos conforme for conveniente, pois assim voc� n�o ter� que criar recursos comuns em todas as views.

Talvez voc� esteja se perguntando como Aurelia determina o nome do elemento personalizado. Por conven��o, ele usar� o nome de exporta��o, com letra min�scula e h�fen. No entanto, voc� sempre pode definir um nome de forma expl�cita. Para fazer isso, adicione um decorador `@customElement('nav-bar')`. E se o seu elemento personalizado n�o tem view porque est� tudo implementado em c�digo? N�o tem problema, adicione o `@noView()`. Quer usar "ShadowDOM" para o seu elemento personalizado? Fa�a como um profissional, utilizando `@useShadowDOM()`. N�o se preocupe quanto ao suporte do navegador. N�s temos uma implementa��o fiel e eficiente do ShadowDOM fallback.

Al�m da cria��o de elementos personalizados, voc� tamb�m pode criar atributos personalizados que adicionam novos comportamentos a elementos existentes. Nesta ocasi�o, voc� pode at� precisar de um atributo para controlar dinamicamente os templates, adicionando e removendo DOM da view, como o `if` e `repeat` que usamos anteriormente. Voc� pode fazer tudo isso e muito mais com mecanismo de modelagem poderosa e extens�vel do Aur�lia.

## Bonus: Trabalhando com Child Routers

Voc� ainda quer mais, n�o � mesmo? Bem, eu tenho uma surpresa para voc�. Vamos adicionar uma terceira p�gina para a nossa aplica��o ... com seu pr�prio router! Chamamos isso de um �child router� (roteador filho). Child Routers t�m a sua pr�pria configura��o de rota e navega��o em rela��o ao router pai. Prepare-se para a loucura....

Primeiro, vamos atualizar nosso _app.js_ com a nova configura��o. Ele deve ficar desta forma:

### app.js (updated...again)

```javascript
import 'bootstrap';
import 'bootstrap/css/bootstrap.css!';

export class App {
  configureRouter(config, router){
    config.title = 'Aurelia';
    config.map([
      { route: ['','welcome'], name: 'welcome',      moduleId: './welcome',      nav: true, title:'Welcome' },
      { route: 'flickr',       name: 'flickr',       moduleId: './flickr',       nav: true, title: 'Flickr' },
      { route: 'child-router', name: 'childRouter',  moduleId: './child-router', nav: true, title:'Child Router' }
    ]);

    this.router = router;
  }
}
```

Nada de novo at� a�. A parte interessante � o _child-router.js _...

### child-router.js

```javascript
export class ChildRouter{
  heading = 'Child Router';

  configureRouter(config, router){
    config.map([
      { route: ['','welcome'], name: 'welcome',     moduleId: './welcome',      nav: true, title:'Welcome' },
      { route: 'flickr',       name: 'flickr',      moduleId: './flickr',       nav: true },
      { route: 'child-router', name: 'childRouter', moduleId: './child-router', nav: true, title:'Child Router' }
    ]);

    this.router = router;
  }
}
```

Mas o qu� !? � praticamente a mesma configura��o do router pai? O Qu�? Por Qu�? Bem ... voc� deve provavelmente nunca precisar� fazer isso na vida real... mas o que vai acontecer aqui � algo muito legal. Isso, meus amigos, � um router recursivo, e n�s estamos fazendo isso porque n�s podemos.
Para completar, aqui est� a view:

### child-router.html

```javascript
<template>
  <section>
    <h2>${heading}</h2>
    <div>
      <div class="col-md-2">
        <ul class="well nav nav-pills nav-stacked">
          <li repeat.for="row of router.navigation" class="${row.isActive ? 'active' : ''}">
            <a href.bind="row.href">${row.title}</a>
          </li>
        </ul>
      </div>
      <div class="col-md-10" style="padding: 0">
        <router-view></router-view>
      </div>
    </div>
  </section>
</template>
```


## Conclus�o

Com sua forte �nfase na experi�ncia do desenvolvedor, o Aurelia pode permitir que voc� crie n�o s� aplica��es surpreendentes, mas tamb�m aprecie o processo. N�s o projetamos com conven��es simples em mente, de uma forma com que voc� n�o precise perder tempo com toneladas de configura��es ou escrevendo c�digo clich� apenas para satisfazer um framework teimoso ou restritivo. Voc� nunca ir� atingir um obst�culo com o Aurelia. Ele foi cuidadosamente projetado para ser �plugg�vel� e personaliz�vel.

Obrigado pelo seu tempo e por ler o nosso guia. N�s esperamos que voc� explore as documenta��es e construa algo incr�vel. Estamos ansiosos para ver o que voc� vai fazer.

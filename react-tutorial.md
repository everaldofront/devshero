
# React Tutorial: Construindo e Protegendo Seu Primeiro Aplicativo

### Saiba como o React funciona e crie e proteja seu primeiro aplicativo React em nenhum momento.



**TL; DR:** Neste artigo, você aprenderá os conceitos básicos do React. Depois disso, você terá a chance de ver o React em ação ao criar um aplicativo simples de perguntas e respostas que conta com uma API de back-end. Se necessário, você pode verificar [este repositório GitHub para verificar o código que suporta este artigo](https://github.com/auth0-blog/react-tutorial). Diverta-se!

## Pré-requisitos

Embora não seja obrigatório, você deve saber algumas coisas sobre JavaScript, HTML e CSS antes de mergulhar neste tutorial do aplicativo React. Se você não tiver experiência anterior com essas tecnologias, talvez não seja fácil seguir as instruções deste artigo, e pode ser uma boa ideia dar um passo atrás e aprender sobre elas primeiro. Se você tem experiência anterior com desenvolvimento web, fique por perto e aproveite o artigo.

Além disso, você precisará ter o Node.js e o NPM instalados em sua máquina de desenvolvimento. Se você não tem essas ferramentas ainda, por favor, [leia e siga as instruções na documentação oficial para instalar Node.js](https://nodejs.org/en/download/). O NPM, que significa Node Package Manager, vem empacotado na instalação padrão do Node.js.

Por fim, você precisará de acesso a um terminal em seu sistema operacional. Se você estiver usando MacOS ou Linux, você está pronto para ir. Se você estiver no Windows, provavelmente será capaz de usar o [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/getting-started/getting-started-with-windows-powershell?view=powershell-6) sem problemas.


> "Aprenda a criar seu primeiro aplicativo React com facilidade."


## React Introdução

[React](https://reactjs.org/) é uma biblioteca JavaScript que o Facebook criou para facilitar o desenvolvimento de [aplicativos de página única (também conhecidos como SPAs)](https://en.wikipedia.org/wiki/Single-page_application). Desde que o Facebook abriu o código e anunciou o React, essa biblioteca se tornou extremamente popular em todo o mundo e ganhou adoção em massa pela comunidade de desenvolvedores. Hoje em dia, embora ainda mantida principalmente pelo Facebook, outras grandes empresas (como [Airbnb](https://www.airbnb.com.br/) , [Auth0](https://auth0.com/) e [Netflix](https://www.netflix.com/)) abraçaram esta biblioteca e estão usando-a para construir seus produtos. Se você marcar [esta página, encontrará uma lista com mais de cem empresas que usam o React](https://github.com/facebook/react/wiki/Sites-Using-React).

Nesta seção, você aprenderá sobre alguns conceitos básicos que devem ser importantes ao desenvolver aplicativos com o React. No entanto, você deve estar ciente de que o objetivo aqui não é fornecer uma explicação completa sobre esses tópicos. O objetivo é fornecer um contexto suficiente para que você possa entender o que está acontecendo enquanto cria seu primeiro aplicativo React.

Para mais informações sobre cada tópico, você pode sempre consultar [a documentação oficial do React](https://reactjs.org/).

## React e a sintaxe do JSX

Primeiramente, você precisa saber que o React usa uma sintaxe engraçada chamada JSX. JSX, que significa JavaScript XML, é uma extensão de sintaxe para JavaScript que permite aos desenvolvedores usar XML (e, como tal, HTML) para descrever a estrutura da interface do usuário. Esta seção não entrará nos detalhes de como o JSX realmente funciona. A ideia aqui é dar-lhe um aviso, para que você não fique surpreso quando vir esta sintaxe nas próximas seções.

Então, quando se trata de JSX, é perfeitamente normal ver coisas assim:


```

function showRecipe(recipe) {
  if (!recipe) {
    return <p>Recipe not found!</p>;
  }
  return (
    <div>
      <h1>{recipe.title}</h1>
      <p>{recipe.description}</h1>
    </div>
  );
}

```


Neste caso, a função `showRecipe`  está usando a sintaxe JSX para mostrar os detalhes de uma `recipe` (isto é, se a receita estiver disponível) ou uma mensagem dizendo que a receita não foi encontrada. Se você não está familiarizado com esta sintaxe, não se preocupe. Você vai se acostumar com isso muito em breve. Então, se você está se perguntando por que o React usa o JSX, você pode ler [a explicação oficial deles aqui](https://reactjs.org/docs/introducing-jsx.html).


> "O React adota o fato de que a lógica de renderização é inerentemente associada a outra lógica da interface do usuário: como os eventos são tratados, como o estado muda com o tempo e como os dados são preparados para exibição". - [Apresentando o JSX](https://reactjs.org/docs/introducing-jsx.html)


## React Componentes

Componentes no React são as partes mais importantes do código. Tudo o que você pode interagir em um aplicativo React é (ou faz parte de) um componente. Por exemplo, quando você carrega um aplicativo React, tudo será tratado por um componente raiz que geralmente é chamado `App`. Então, se esta aplicação contiver uma barra de navegação, você pode apostar que esta barra está definida dentro de um componente chamado `NavBar` ou similar. Além disso, se essa barra contiver um formulário no qual você pode inserir um valor para acionar uma pesquisa, provavelmente você está lidando com outro componente que lida com este formulário.

A maior vantagem de usar componentes para definir seu aplicativo é que essa abordagem permite encapsular partes diferentes da interface do usuário em partes independentes e reutilizáveis. Ter cada parte em seu próprio componente facilita o raciocínio, o teste e a reutilização de cada peça com facilidade. Quando você começa a se orientar com essa abordagem, você verá que ter uma árvore de componentes (que é o que obtém quando você divide tudo em componentes) também facilita a propagação de estado.


> "A maior vantagem de usar componentes para definir seu aplicativo é que essa abordagem permite encapsular diferentes partes da interface do usuário em partes independentes e reutilizáveis."


## Definindo Componentes em React

Agora que você aprendeu que os aplicativos React não são mais do que uma árvore de componentes, é necessário aprender como criar componentes no React. Então, basicamente, existem dois tipos de componentes do React que você pode criar: [Componentes Funcionais e Componentes de Classe](https://reactjs.org/docs/components-and-props.html#functional-and-class-components).

A diferença entre esses dois tipos é que os componentes funcionais são simplesmente componentes "burros" que não mantêm nenhum estado interno (tornando-os ótimos para manipular a apresentação), e os componentes de classe são componentes mais complexos que podem manter o estado interno. Por exemplo, se você estiver criando um componente que mostrará apenas o perfil do usuário autenticado, poderá criar um componente funcional da seguinte maneira:



```

function UserProfile(props) {
  return (
    <div className="user-profile">
      <img src={props.userProfile.picture} />
      <p>{props.userProfile.name}</p>
    </div>
  );
}

```



Não há nada particularmente interessante sobre o componente definido acima, já que nenhum estado interno é tratado. Como você pode ver, este componente simplesmente usa um `userProfile` que foi passado para definir um elemento `div` que mostra a imagem do usuário (o elemento `img`) e seu nome (dentro do elemento `p` ).

No entanto, se você for criar um componente para lidar com coisas que precisam manter algum estado e executar tarefas mais complexas, como um formulário de inscrição, você precisará de um componente de classe. Para criar um componente de classe no React, você deveria proceder da seguinte maneira:



```

class SubscriptionForm extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      acceptedTerms: false,
      email: '',
    };
  }

  updateCheckbox(checked) {
    this.setState({
      acceptedTerms: checked,
    });
  }

  updateEmail(value) {
    this.setState({
      email: value,
    });
  }

  submit() {
    // ... use email and acceptedTerms in an ajax request or similar ...
  }

  render() {
    return (
      <form>
        <input
          type="email"
          onChange={(event) => {this.updateEmail(event.target.value)}}
          value={this.state.email}
        />
        <input
            type="checkbox"
            checked={this.state.acceptedTerms}
            onChange={(event) => {this.updateCheckbox(event.target.checked)}}
          />
        <button onClick={() => {this.submit()}}>Submit</button>
      </form>
    )
  }
}

```



Como você pode ver, este novo componente está lidando com muito mais coisas do que o outro. Para iniciantes, este componente está definindo três elementos de entrada (na verdade, dois `input` tags e um `button`, mas o botão também é considerado um elemento de entrada). O primeiro permite que os usuários insiram seus endereços de e-mail. A segunda é uma caixa de seleção onde os usuários podem definir se concordam ou não com alguns termos arbitrários. O terceiro é um botão que os usuários terão que clicar para finalizar o processo de inscrição.

Além disso, você notará que este componente está definindo um estado interno (`this.state`) com dois campos: `acceptedTerms` e `email`. Nesse caso, o formulário usa o `acceptedTerms` campo para representar a escolha dos usuários em relação aos termos fictícios e ao `email` campo para manter seus endereços de e-mail. Então, quando os usuários clicam no botão enviar, este formulário usaria seu estado interno para emitir uma [solicitação AJAX]https://www.w3schools.com/xml/ajax_xmlhttprequest_send.asp).

Então, basicamente, se você precisa de um componente para lidar com as coisas dinâmicas que dependem de um estado interno, como a entrada do usuário, você precisará de um componente de classe. No entanto, se você precisar de um componente que não realize nenhuma lógica internamente que dependa de um estado interno, pode ficar com um componente funcional.


> **Nota:** Esta é apenas uma breve explicação sobre os diferentes componentes e como eles se comportam. Na verdade, o último componente criado nesta seção `SubscriptionForm`, poderia ser facilmente transformado em um componente funcional também. Nesse caso, você teria que mover seu estado interno para cima na árvore de componentes e passar para ele esses valores e funções para acionar mudanças de estado. Para saber mais sobre os componentes do React, [consulte este artigo](https://reactjs.org/docs/components-and-props.html#functional-and-class-components).


## Re-Renderizando os Componentes do React

Outro conceito muito importante que você precisa entender é como e quando o React processa novamente os componentes. Felizmente, este é um conceito fácil de aprender. Há apenas duas coisas que podem acionar uma nova renderização em um componente React: uma alteração no `props` que o componente recebe ou uma alteração em seu estado interno.

Embora a seção anterior não tenha entrado nos detalhes sobre como alterar o estado interno de um componente, ele mostrou como conseguir isso. Sempre que você usa um componente com estado (ou seja, um componente de classe), é possível acionar uma nova renderização alterando seu estado por meio do método `setState`. O que é importante ter em mente é que você **não deve** alterar campoo `state` diretamente. Você **tem que** chamar o método `setState` com o novo estado desejado:



```

// this won't trigger a re-render:
updateCheckbox(checked) {
  this.state.acceptedTerms = checked;
}

// this will trigger a re-render:
this.setState({
  acceptedTerms: checked,
});

```



Em outras palavras, você tem que tratar `this.state` como se fosse imutável.


**Nota:** Para obter um melhor desempenho, o React não garante que `setState()` será atualizado `this.state` imediatamente. A biblioteca pode esperar por uma oportunidade melhor quando há mais coisas para atualizar. Portanto, não é confiável ler `this.state` logo depois de ligar `setState()`. Para mais informações, [verifique a documentação oficial em setState()](https://reactjs.org/docs/react-component.html#setstate).


Agora, quando se trata de um componente sem estado (ou seja, um componente funcional), a única maneira de acionar uma nova renderização é alterar os `props` que são passados ​​para ela. Na última seção, você não teve a chance de ver todo o contexto de como um componente funcional é usado nem o que `props` realmente é. Felizmente, este é outro tópico fácil de entender. Em React, `props` nada mais são do que as propriedades (assim seu nome) passadas para um componente.

Assim, no componente `UserProfile` definido na última seção, houve apenas uma propriedade que está sendo passado / utilizado: `UserProfile`. Naquela seção, no entanto, havia uma parte faltante que era responsável por passar propriedades (`props`) para esse componente. Nesse caso, a peça que faltava era onde e como você usa esse componente. Para fazer isso, você só precisa usar o componente como se fosse um elemento HTML (esse é um bom recurso do JSX), como mostrado aqui:



```

import React from 'react';
import UserProfile from './UserProfile';

class App extends () {
  constructor(props) {
    super(props);
    this.state = {
      user: {
        name: 'Bruno Krebs',
        picture: 'https://cdn.auth0.com/blog/profile-picture/bruno-krebs.png',
      },
    };
  }

  render() {
    return (
      <div>
        <UserProfile userProfile={this.state.user} />
      </div>
    );
  }
}

```



É isso aí. É assim que você define e passa `props` para um componente filho. Agora, se você alterar o `user` no componente pai (`App`), isso acionará uma nova renderização em todo o componente e, subsequentemente, alterará também a `props` passagem para o `UserProfile` acionamento de uma nova renderização.


> **Nota:** O React também renderizará novamente os componentes da classe se eles `props` forem alterados. Este não é um comportamento específico de componentes funcionais.


## O que você vai construir com React

Tudo certo! Com os conceitos descritos na última seção em mente, você está pronto para começar a desenvolver seu primeiro aplicativo React. Nas seções a seguir, você criará um aplicativo simples de perguntas e respostas (perguntas e respostas) que permitirá que os usuários interajam entre si, perguntando e respondendo perguntas. Para tornar todo o processo mais realista, você usará o Node.js e o Express para criar uma API de backend aproximada. Não se preocupe se você não estiver familiarizado com o desenvolvimento de aplicativos de back-end com o Node.js. Este vai ser um processo muito simples, e você estará pronto e funcionando em nenhum momento.

No final deste tutorial, você terá um aplicativo React suportado por um backend do Node.js que se parece com isso:

![React Tutorial: Exemplo de aplicativo final de perguntas e respostas](https://cdn.auth0.com/blog/react-tutorial/q-and-a-app.png)

## Desenvolvendo uma API de back-end com o Node.js e Express

Antes de mergulhar no React, você criará rapidamente uma API de back-end para oferecer suporte ao seu aplicativo de perguntas e respostas. Nesta seção, você usará o Express juntamente com o Node.js para criar essa API. Se você não sabe o que é Express ou como funciona, não se preocupe, você não precisa entrar em detalhes agora. [Express](https://expressjs.com/), conforme declarado por sua documentação oficial, é um framework web minimalista e sem parentesco para o Node.js. Com essa biblioteca, como você verá aqui, você pode criar rapidamente aplicativos para serem executados em servidores (por exemplo, aplicativos de back-end).

Então, para começar as coisas, abra um terminal em seu sistema operacional, vá para um diretório onde você cria seus projetos e emita os seguintes comandos:



```

# create a directory for your project
mkdir qa-app

# move into it
cd qa-app

# create a directory for your Express API
mkdir backend

# move into it
cd backend

# use NPM to start the project
npm init -y

```



O último comando irá criar um arquivo chamado `package.json` dentro do seu diretório `backend`. Este arquivo conterá os detalhes (como as dependências) de sua API de back-end. Então, após esses comandos, execute o seguinte:



```

npm i body-parser cors express helmet morgan

```


Este comando irá instalar cinco dependências no seu projeto:

* [`body-parser`](https://github.com/expressjs/body-parser): Esta é uma biblioteca que você usará para converter o corpo de solicitações recebidas em objetos JSON.
* [`cors`](https://github.com/expressjs/cors): Esta é uma biblioteca que você usará para configurar o Express para adicionar cabeçalhos informando que sua API aceita solicitações provenientes de outras origens. Isso também é conhecido como [Compartilhamento de Recursos de Origem Cruzada (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) .
* [`express`](https://github.com/expressjs/express): Isso é o próprio Express.
* [`helmet`](https://github.com/helmetjs/helmet): Esta é uma biblioteca que ajuda a proteger aplicativos Express com vários cabeçalhos HTTP.
* [`morgan`](https://github.com/expressjs/morgan): Esta é uma biblioteca que adiciona alguns recursos de registro ao seu aplicativo Express.


**Nota:** Como o objetivo deste artigo é ajudá-lo a desenvolver seu primeiro aplicativo React, a lista acima contém uma breve explicação sobre o que cada biblioteca traz para a tabela. Você sempre pode consultar as páginas da Web oficiais dessas bibliotecas para saber mais sobre seus recursos.


Depois de instalar essas bibliotecas, você poderá ver que o NPM alterou seu arquivo `package.json` para incluí-las na propriedade `dependencies`. Além disso, você verá um novo arquivo chamado `package-lock.json`. O NPM usa esse arquivo para garantir que qualquer pessoa que use seu projeto (ou mesmo você mesmo em outros ambientes) [sempre obtenha versões compatíveis com as que você está instalando agora](https://docs.npmjs.com/files/package-lock.json).

Então, a última coisa que você precisa fazer é desenvolver o código-fonte de back-end. Então, crie um diretório chamado `src` dentro de seu diretório `backend` e crie um arquivo chamado `index.js` dentro deste novo diretório. Nesse arquivo, você pode adicionar o seguinte código:



```

//import dependencies
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');

// define the Express app
const app = express();

// the database
const questions = [];

// enhance your app security with Helmet
app.use(helmet());

// use bodyParser to parse application/json content-type
app.use(bodyParser.json());

// enable all CORS requests
app.use(cors());

// log HTTP requests
app.use(morgan('combined'));

// retrieve all questions
app.get('/', (req, res) => {
  const qs = questions.map(q => ({
    id: q.id,
    title: q.title,
    description: q.description,
    answers: q.answers.length,
  }));
  res.send(qs);
});

// get a specific question
app.get('/:id', (req, res) => {
  const question = questions.filter(q => (q.id === parseInt(req.params.id)));
  if (question.length > 1) return res.status(500).send();
  if (question.length === 0) return res.status(404).send();
  res.send(question[0]);
});

// insert a new question
app.post('/', (req, res) => {
  const {title, description} = req.body;
  const newQuestion = {
    id: questions.length + 1,
    title,
    description,
    answers: [],
  };
  questions.push(newQuestion);
  res.status(200).send();
});

// insert a new answer to a question
app.post('/answer/:id', (req, res) => {
  const {answer} = req.body;

  const question = questions.filter(q => (q.id === parseInt(req.params.id)));
  if (question.length > 1) return res.status(500).send();
  if (question.length === 0) return res.status(404).send();

  question[0].answers.push({
    answer,
  });

  res.status(200).send();
});

// start the server
app.listen(8081, () => {
  console.log('listening on port 8081');
});

```



Para manter as coisas curtas, a lista a seguir explica brevemente como as coisas funcionam neste arquivo (também, certifique-se de verificar os comentários no código acima):

* Tudo começa com cinco declarações `require`. Essas instruções carregam todas as bibliotecas instaladas com o NPM.

* Depois disso, você usa o Express para definir um novo aplicativo (`const app = express();`).

* Em seguida, você cria uma matriz que atuará como seu banco de dados (`const questions = [];`). Em um aplicativo do mundo real, você usaria um banco de dados real como Mongo, PostgreSQL, MySQL, etc.

* Em seguida, você chama o método `use` do seu aplicativo Express quatro vezes. Cada um para configurar as diferentes bibliotecas que você instalou junto com o Express.

* Logo depois, você define seu primeiro endpoint (`app.get('/', ...);`). Este endpoint é responsável por enviar a lista de perguntas para quem a solicitar. A única coisa a notar aqui é que, em vez de enviar o `answers` também, esse terminal os reúne para enviar apenas o número de respostas que cada pergunta possui. Você usará essas informações no seu aplicativo React.

* Após o primeiro endpoint, você define outro endpoint. Nesse caso, esse novo endpoint é responsável por responder a solicitações com uma única pergunta (agora, com todas as respostas).

* Após este endpoint, você define seu terceiro endpoint. Desta vez, você define um ponto de extremidade que será ativado sempre que alguém enviar uma solicitação HTTP POST para sua API. O objetivo aqui é levar a mensagem enviada no `body` pedido para inserir um `newQuestion` em seu banco de dados.

* Então, você tem o último ponto de extremidade na sua API. Este endpoint é responsável por inserir respostas em uma questão específica. Nesse caso, você usa um [parâmetro de rota](https://expressjs.com/en/guide/routing.html) chamado `id` para identificar em qual pergunta você deve adicionar a nova resposta.

* Por fim, você chama a função `listen` em seu aplicativo Express para executar sua API de back-end.

Com este arquivo no lugar, você está pronto para ir. Para executar seu aplicativo, basta emitir o seguinte comando:



```

# from the qa-app directory
node src

```


Então, para testar se tudo está realmente funcionando, abra um novo terminal e emita os seguintes comandos:



```

# issue an HTTP GET request
curl localhost:8081

# issue a POST request
curl -X POST -H 'Content-Type: application/json' -d '{
  "title": "How do I make a sandwich?",
  "description": "I am trying very hard, but I do not know how to make a delicious sandwich. Can someone help me?"
}' localhost:8081

curl -X POST -H 'Content-Type: application/json' -d '{
  "title": "What is React?",
  "description": "I have been hearing a lot about React. What is it?"
}' localhost:8081

# re-issue the GET request
curl localhost:8081

```



> Se você não sabe, [`curl` é uma interface de linha de comando que permite que você envie solicitações HTTP com facilidade](https://curl.haxx.se/docs/httpscripting.html). No snippet de código acima, você pode ver que, com apenas alguns ataques de tecla, pode emitir diferentes tipos de solicitações HTTP, definir quais cabeçalhos (`-H`) eles precisam e passar dados (`-d`) para os back-ends.


O primeiro comando acionará uma solicitação HTTP GET que resultará em uma matriz vazia sendo impressa (`[]`). Em seguida, o segundo e o terceiro comandos emitirão solicitações POST para inserir duas perguntas em sua API, e o quarto comando emitirá outra solicitação GET para verificar se essas perguntas foram inseridas corretamente.

Se você conseguir obter os resultados esperados, deixe seu servidor em execução e passe para a próxima seção.

## Desenvolvendo Aplicações com React

Com a API do back-end em funcionamento, você está finalmente pronto para começar a desenvolver seu aplicativo React. Não faz muito tempo, desenvolvedores dispostos a criar aplicativos com o React teriam dificuldade em configurar todas as ferramentas necessárias (por exemplo, [webpack](https://webpack.js.org/)) para criar um aplicativo React. No entanto (e felizmente), o cenário mudou depois que o Facebook publicou uma ferramenta chamada [*Create React App*](https://github.com/facebook/create-react-app) .

Com esta ferramenta, você pode criar um novo aplicativo React com apenas um comando. Assim, para criar seu aplicativo React, abra um novo terminal e vá para o mesmo diretório onde você criou o backend aplicativo Node.js (ou seja, do qa-app diretório). De lá, emita o seguinte comando:



```

# the npx command was introduced on npm@5.2.0
npx create-react-app frontend

```



Isso fará com que o download do NPM seja executado `create-react-app` em um único comando, passando para ele `frontend` como o diretório desejado para o novo aplicativo. O processo envolvido no scaffolding de uma nova aplicação, como você verá depois de executar o comando acima, não é tão simples assim. A ferramenta precisa mesmo de alguns segundos (ou alguns minutos, dependendo da sua conexão com a Internet) para criar a coisa toda. No entanto, quando essa ferramenta terminar, você poderá emitir os seguintes comandos para executar seu aplicativo React:



```

# move into the new directory
cd frontend

# start your React app
npm start

```



> **Nota:** Se você tiver o Yarn instalado, a ferramenta `create-react-app`  irá utilizá-lo para fazer o bootstrap do seu projeto. Como tal, você precisará usar `yarn start` ou você terá que executar `npm install` antes de executar `npm start`.


O último comando emitido acima iniciará um servidor de desenvolvimento que escuta na porta `3000` e abrirá o novo aplicativo no navegador da Web padrão.

![Bem-vindo à página inicial do React local](https://cdn.auth0.com/blog/react-tutorial/welcome-to-react-v2.png)

Depois de ver seu aplicativo, você pode parar o servidor pressionando `Ctrl` + `C` para poder instalar algumas dependências que serão necessárias em seu aplicativo. Então, de volta ao seu terminal e depois de parar o servidor, execute o seguinte comando:



```

npm i react-router react-router-dom

```


Este comando instalará duas bibliotecas para ajudá-lo a lidar com a navegação no seu aplicativo. O primeiro deles `react-router` é a biblioteca principal que permite a navegação contínua. O segundo `react-router-dom`, fornece ligações DOM para o React Router.


> **Nota:** Se você estivesse usando o [React Native](https://facebook.github.io/react-native/) para desenvolver um aplicativo para dispositivos móveis, seria necessário instalá-lo `react-router-native`.


Em seguida, depois de instalar essas bibliotecas, você poderá abrir seu projeto React em seu IDE preferencial para iniciar o trabalho real.


## Limpando seu aplicativo React

Bem, na verdade, antes de começar a desenvolver seu aplicativo, você pode remover alguns arquivos dele e limpar seu código um pouco. Para começar, você pode remover o arquivo `./src/App.test.js` porque não criará testes automatizados neste tutorial. Embora este seja um tópico importante, você irá ignorá-lo por enquanto, para que possa se concentrar no aprendizado do React.

> **Observação:** depois de aprender sobre o React, você pode se interessar em saber como adicionar testes automatizados ao seu aplicativo. Um bom recurso para ajudá-lo nessa questão é [a postagem no blog *Testing React Applications with Jest*](https://auth0.com/blog/testing-react-applications-with-jest/).

Além disso, você também pode remover dois outros arquivos como você não vai usá-los: `./src/logo.svg` e `./src/App.css`. Em seguida, após remover esses arquivos, abra o `./src/App.js` arquivo e substitua seu código por:



```

import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div>
        <p>Work in progress.</p>
      </div>
    );
  }
}

export default App;

```



Você não utilizará realmente a nova versão do seu componente `App`, pois em breve irá substituir o conteúdo deste arquivo novamente. No entanto, para evitar que o código não seja compilado, é uma boa ideia refatorar seu componente `App`.


## Configurando o roteador React no seu aplicativo

Depois de limpar as coisas, você precisará configurar o React Router no seu aplicativo. Este será um passo bem simples, como você verá. No entanto, lembre-se de que, para dominar o React Router, você precisará ler pelo menos um outro artigo que introduza especificamente o assunto e todos os seus recursos.

O problema é que o React Router é uma solução muito completa e, no seu primeiro aplicativo React, você tocará apenas na ponta do iceberg. Se você quiser [saber mais sobre o React Router, por favor, vá para a documentação oficial](https://reacttraining.com/react-router/).


> "O React Router é uma solução poderosa que pode ajudá-lo a criar aplicativos incríveis."

Tendo isso em mente, abra o arquivo `./src/index.js` e substitua seu conteúdo por isso:



```

import React from 'react';
import ReactDOM from 'react-dom';
import {BrowserRouter} from 'react-router-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
, document.getElementById('root'));

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.unregister();

```



Na nova versão deste arquivo, você está apenas importando `BrowserRouter` da `react-router-dom` biblioteca e encapsulando seu `App` componente dentro deste roteador. Isso é tudo que você precisa para começar a usar o Roteador React.


> **Nota:** Se você não viu este arquivo antes, esta é a lógica que faz com que seu aplicativo React seja renderizado. Mais especificamente, `document.getElementById('root')` define em qual elemento HTML o React deve renderizar seu aplicativo. Você pode encontrar este `root` elemento dentro do arquivo `./public/index.html`.


## Configurando o Bootstrap no seu aplicativo React

Para tornar seu aplicativo React mais atraente do ponto de vista da interface do usuário, você configurará o [Bootstrap](https://getbootstrap.com/) nele. Se você não conhece o Bootstrap, essa é uma biblioteca extremamente popular que ajuda os desenvolvedores a criar aplicativos da Web responsivos e de boa aparência com facilidade.

Existem várias maneiras de integrar o React e o Bootstrap juntos. No entanto, como os requisitos para o seu primeiro aplicativo serão bastante simples e como você não precisará de nenhum de [seus componentes interativos](https://getbootstrap.com/docs/4.1/components/buttons/) (ou seja, você está interessado apenas nos estilos básicos que essa biblioteca fornece), você seguirá a estratégia mais fácil. acessível. Ou seja, você simplesmente abrirá seu arquivo `./public/index.html` e o atualizará da seguinte maneira:



```

<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- ... tags above the title stay untouched ... -->
    <title>Q&App</title>
    <link rel="stylesheet" href="https://bootswatch.com/4/flatly/bootstrap.min.css">
  </head>
  <!-- ... body definition stays untouched ... -->
</html>

```



Nesse caso, você está realmente fazendo duas coisas: está mudando o title aplicativo React para *Q & App* e está fazendo o aplicativo carregar uma variação de Bootstrap chamada `flatly`. Se você estiver interessado, você pode usar qualquer variação disponível no [Bootswatch](https://bootswatch.com/) , ou você também pode usar o sabor padrão do Bootstrap. No entanto, você provavelmente achará as variações disponíveis no Bootswatch mais atraentes.

## Criando uma barra de navegação no seu aplicativo React

Agora que você configurou seu aplicativo para usar o Bootstrap, você está pronto para criar seu primeiro componente React. Nesta seção, você criará um componente chamado `NavBar` (que significa Barra de Navegação) e o adicionará ao seu aplicativo React.

Para fazer isso, crie um novo diretório chamado `NavBar` dentro do `src` diretório do seu aplicativo e insira um novo arquivo chamado `NavBar.js` dentro dele. Neste arquivo, insira o seguinte código:



```

import React from 'react';
import {Link} from 'react-router-dom';

function NavBar() {
  return (
    <nav className="navbar navbar-dark bg-primary fixed-top">
      <Link className="navbar-brand" to="/">
        Q&App
      </Link>
    </nav>
  );
}

export default NavBar;

```



Como você pode ver, o componente da barra de navegação que você está criando é um componente funcional. Você pode criá-lo como um componente sem estado (isto é, funcional) porque você realmente não precisa manter nenhum estado interno.

Agora, para usar seu novo componente, você pode abrir seu arquivo `./src/App.js` e atualizá-lo da seguinte maneira:



```

import React, { Component } from 'react';
import NavBar from './NavBar/NavBar';

class App extends Component {
  render() {
    return (
      <div>
        <NavBar/>
        <p>Work in progress.</p>
      </div>
    );
  }
}

export default App;

```



Em seguida, se você executar seu aplicativo emitindo `npm start` de um terminal, verá a barra de navegação na parte superior dele. No entanto, o que você não verá é a mensagem "trabalho em andamento" que o seu componente `App` contém. O problema aqui é que a barra de navegação que você criou está usando uma classe CSS (`fixed-top`) fornecida pelo Bootstrap que a torna fixa no topo. Isso significa que esse componente não está ocupando o espaço vertical padrão como se fosse um elemento `div` normal.

Para corrigir essa situação, abra o arquivo `./src/index.css` e adicione uma `margin-top` regra, conforme mostrado aqui:



```

body {
  /* ... other rules ... */
  margin-top: 100px;
}

/* ... other rules ... */

```



Agora, se você verificar seu aplicativo novamente, verá sua barra de navegação e a mensagem "trabalho em andamento".

![Aplicativo react com barra de navegação](https://cdn.auth0.com/blog/react-tutorial/react-app-with-navbar.png)

## Criando um componente de classe com React

Depois de criar a barra de navegação, o que você pode fazer é criar um componente com estado (um componente de classe) para buscar perguntas do seu back-end e mostrá-lo aos seus usuários. Para buscar essas perguntas, você precisará da ajuda de outra biblioteca, o Axios . Em poucas palavras, o [Axios](https://github.com/axios/axios) é um cliente HTTP baseado em promessas para o navegador e para o Node.js. Neste tutorial, você só vai usá-lo no navegador (ou seja, no seu aplicativo React).

Para instalar o Axios, pare o servidor de desenvolvimento do React e emita o seguinte comando:



```

npm i axios

```



Em seguida, crie um novo diretório chamado `Questions` inside `src` e um novo arquivo chamado `Questions.js` dentro dele. Neste arquivo, você pode inserir o seguinte código:



```

import React, {Component} from 'react';
import {Link} from 'react-router-dom';
import axios from 'axios';

class Questions extends Component {
  constructor(props) {
    super(props);

    this.state = {
      questions: null,
    };
  }

  async componentDidMount() {
    const questions = (await axios.get('http://localhost:8081/')).data;
    this.setState({
      questions,
    });
  }

  render() {
    return (
      <div className="container">
        <div className="row">
          {this.state.questions === null && <p>Loading questions...</p>}
          {
            this.state.questions && this.state.questions.map(question => (
              <div key={question.id} className="col-sm-12 col-md-4 col-lg-3">
                <Link to={`/question/${question.id}`}>
                  <div className="card text-white bg-success mb-3">
                    <div className="card-header">Answers: {question.answers}</div>
                    <div className="card-body">
                      <h4 className="card-title">{question.title}</h4>
                      <p className="card-text">{question.description}</p>
                    </div>
                  </div>
                </Link>
              </div>
            ))
          }
        </div>
      </div>
    )
  }
}

export default Questions;

```



Existem algumas coisas importantes acontecendo neste arquivo. Primeiro, como mencionado anteriormente, você está criando um componente com estado que manterá as perguntas disponíveis em sua API de back-end. Portanto, para fazer isso corretamente, você está iniciando seu componente com a propriedade `questions` definida como `null` e, quando o React concluir a montagem de seu componente (que aciona o método `componentDidMount`), você estará emitindo uma solicitação GET (por meio da chamada `axios.get`) para seu backend. Enquanto isso, entre o seu pedido e a resposta do backend, o React processa o seu componente com uma mensagem dizendo "carregando perguntas ..." (isso acontece porque você o instruiu a se comportar desse modo adicionando `this.state.questions === null &&` antes da mensagem).


> **Nota:** Este componente está tocando em um tópico que não foi tratado neste artigo, [o Lifecycle of React Components](https://reactjs.org/docs/react-component.html#the-component-lifecycle). Nesse caso, você está usando apenas um dos pontos de extensão fornecidos pelo React, o método `componentDidMount`. Você não precisa realmente entender como isso funciona para seguir este tutorial, mas, depois de terminá-lo, certifique-se de aprender sobre este tópico.


Então, sempre que o Axios obtiver uma resposta do backend, você coloca o `data` retornado dentro de uma constante chamada `questions` e atualiza o estado do componente (`this.setState`) com ele. Essa atualização, como você já aprendeu, aciona uma nova renderização e faz o React mostrar todas as perguntas recuperadas.

Agora, em relação a como as suas perguntas são mostradas, você está usando um monte de elementos `div` com classes CSS fornecidas pelo Bootstrap para criar um belo [componente *Card*](https://getbootstrap.com/docs/4.1/components/card/) . Se você quiser ajustar como esse cartão é exibido, verifique os documentos.

Além disso, note que você está usando um componente chamado `Link` (a partir `react-router-dom`) para fazer este redirecionar os usuários para o seguinte caminho quando clicado: `/question/${question.id}`. Na próxima seção, você criará um componente para mostrar as respostas a uma pergunta escolhida pelo usuário.

Então, como você já entende como o seu componente se comporta, a próxima coisa que você precisará fazer é atualizar o código do seu componente `App` para usar o novo componente:



```

import React, { Component } from 'react';
import NavBar from './NavBar/NavBar';
import Questions from './Questions/Questions';

class App extends Component {
  render() {
    return (
      <div>
        <NavBar/>
        <Questions/>
      </div>
    );
  }
}

export default App;

```



Em seguida, se você executar seu aplicativo novamente (`npm start`), verá esta bela página:


![React app usando o Axios para buscar dados de uma API de back-end.](https://cdn.auth0.com/blog/react-tutorial/react-app-showing-questions.png)

## Roteando Usuários com o Roteador React

Com todos esses recursos, uma etapa importante que você precisa aprender é como lidar com o roteamento no seu aplicativo React. Nesta seção, você aprenderá sobre esse tópico enquanto cria um componente que mostra os detalhes das perguntas disponíveis no seu back-end.

Para iniciantes, você pode criar um novo diretório chamado `Question` (singular now) e um arquivo chamado `Question.js` (também singular) dentro dele. Em seguida, você pode inserir o seguinte código neste arquivo:



```

import React, {Component} from 'react';
import axios from 'axios';

class Question extends Component {
  constructor(props) {
    super(props);
    this.state = {
      question: null,
    };
  }

  async componentDidMount() {
    const { match: { params } } = this.props;
    const question = (await axios.get(`http://localhost:8081/${params.questionId}`)).data;
    this.setState({
      question,
    });
  }

  render() {
    const {question} = this.state;
    if (question === null) return <p>Loading ...</p>;
    return (
      <div className="container">
        <div className="row">
          <div className="jumbotron col-12">
            <h1 className="display-3">{question.title}</h1>
            <p className="lead">{question.description}</p>
            <hr className="my-4" />
            <p>Answers:</p>
            {
              question.answers.map((answer, idx) => (
                <p className="lead" key={idx}>{answer.answer}</p>
              ))
            }
          </div>
        </div>
      </div>
    )
  }
}

export default Question;

```



A maneira como esse novo componente funciona é, na verdade, muito semelhante à maneira como o componente `Questions` funciona. Esse é um componente com estado que usa o Axios para emitir uma solicitação GET para o terminal que recupera todos os detalhes de uma pergunta e que atualiza a página sempre que receber uma resposta.

Nada realmente novo aqui. O que vai ser novo é a maneira como esse componente é renderizado.

Então, abra o arquivo `App.js` e substitua seu conteúdo por isso:



```

import React, { Component } from 'react';
import {Route} from 'react-router-dom';
import NavBar from './NavBar/NavBar';
import Question from './Question/Question';
import Questions from './Questions/Questions';

class App extends Component {
  render() {
    return (
      <div>
        <NavBar/>
        <Route exact path='/' component={Questions}/>
        <Route exact path='/question/:questionId' component={Question}/>
      </div>
    );
  }
}

export default App;

```



Na nova versão do seu componente `App`, você está usando dois `Route` elementos (fornecido por `react-router-dom`) para informar ao React quando deseja que o componente `Questions` seja renderizado e quando você deseja que o `Question` componente seja renderizado. Mais especificamente, você está dizendo para o React que, se os usuários navegarem até `/` (`exact path='/'`), você deseja que eles vejam `Questions` e, se eles navegarem até `/question/:questionId`, você deseja que eles vejam os detalhes de uma pergunta específica.

Note que a última rota define um parâmetro chamado `questionId`. Quando você criou o componente `Questions` (plural), adicionou um link que usa a `id` da pergunta. O React Router usa isso `id` para formar o link e, em seguida, fornece ao seu `Question` componente (`params.questionId`). Com isso `id`, seu componente usa o Axios para informar ao back-end qual pergunta está sendo solicitada.

Se você verificar sua inscrição agora, poderá ver todas as suas perguntas na página inicial e poderá navegar para uma pergunta específica. No entanto, você provavelmente não verá nenhuma resposta em seu novo componente porque nunca adicionou uma. Por enquanto, para adicionar respostas às suas perguntas, você pode emitir solicitações semelhantes à seguinte:



```

curl -X POST -H 'Content-Type: application/json' -d '{
  "answer": "Just spread butter on the bread, and that is it."
}' localhost:8081/answer/1

```



Depois disso, se você recarregar seu aplicativo e acessar [`http://localhost:3000/question/1`](http://localhost:3000/question/1), verá uma página semelhante a esta:


![React app Página de perguntas do aplicativo configurada com o Roteador React](https://cdn.auth0.com/blog/react-tutorial/react-app-with-react-router.png)

## Protegendo seu aplicativo React

Seu aplicativo atingiu um estado em que tem quase tudo que precisa para o horário nobre. Há apenas alguns recursos faltando. Por exemplo, no momento, seus usuários não têm meios de criar perguntas nem de respondê-las por meio do seu aplicativo. Outro exemplo é que não há como fazer login no seu aplicativo. Além disso, as perguntas e respostas não fornecem informações sobre seus autores.

Nesta seção, você aprenderá como implementar todos esses recursos com facilidade. Você começará assinando o [Auth0](https://auth0.com/) para ajudá-lo com o recurso de autenticação, protegerá seu back-end e, para finalizar, protegerá seu aplicativo React e refatorará o componente `Question` para que os usuários autenticados possam responder às perguntas.

## Configurando uma conta Auth0

Para começar, você precisará se inscrever no Auth0 para poder integrá-lo em seu aplicativo. Se você já tem uma conta existente, pode usá-la sem problemas. Se você não tiver um, agora é um bom momento para se [inscrever em uma conta do Auth0 gratuita](https://auth0.com/signup). Com sua conta gratuita, você terá acesso aos seguintes recursos:


* [Autenticação sem senha](https://auth0.com/passwordless)
* [Bloqueio para Web, iOS e Android](https://auth0.com/docs/libraries/lock/v11)
* [Até 2 provedores de identidade social (como Twitter e Facebook)](https://auth0.com/learn/social-login/)
* [Regras sem servidor ilimitadas](https://auth0.com/docs/rules)
* [Suporte da comunidade](https://community.auth0.com/)


Depois de se inscrever, você terá que criar um [aplicativo Auth0](https://auth0.com/docs/applications) para representar seu aplicativo. Assim, no seu painel, clique na [seção Aplicativos](https://manage.auth0.com/#/applications) no menu vertical e, em seguida, clique em *Criar Aplicativo*.

Na caixa de diálogo mostrada, você terá que inserir um nome para o seu aplicativo (por exemplo, "Q & App") e, em seguida, terá que escolher o *Aplicativo de Página Única* como seu tipo. Então, quando você clicar no botão *Criar* , o Auth0 criará seu Aplicativo e o redirecionará para a seção *Início Rápido*. A partir daí, você terá que clicar na guia *Configurações* para alterar a configuração do seu aplicativo Auth0 e copiar alguns valores dele.

![Criando um aplicativo React no Auth0](https://cdn.auth0.com/blog/react-tutorial/creating-a-react-application-at-auth0.png)

Assim, depois de ir para a guia *Configurações*, pesquise o campo *URLs de retorno de chamada permitidos* e insira `http://localhost:3000/callback` nele.

Você provavelmente está se perguntando o que esse URL significa e por que você precisa dele. O motivo pelo qual você precisa deste URL é que, enquanto estiver autenticando através de Auth0, seus usuários serão redirecionados para sua Página de Login Universal e, após o processo de autenticação (bem-sucedido ou não), eles serão redirecionados de volta para seu aplicativo. Por motivos de segurança, o Auth0 redirecionará seus usuários apenas para URLs registrados nesse campo.

Com esse valor, você pode clicar no botão Salvar alterações e deixar esta página aberta.

## Protegendo sua API de back-end com Auth0

Para proteger sua API do Node.js com Auth0, você terá que instalar e configurar apenas duas bibliotecas:


* [`express-jwt`](https://github.com/auth0/express-jwt): Um middleware que valida um JSON Web Token (JWT) e define o `req.user` com seus atributos.
* [`jwks-rsa`](https://github.com/auth0/node-jwks-rsa): Uma biblioteca para recuperar chaves públicas RSA de um ponto de extremidade JWKS (JSON Web Key Set).


Para instalar essas bibliotecas, pare sua API de back-end pressionando `Ctrl` + `C` e execute o seguinte comando:



```

# from the backend directory
npm i express-jwt jwks-rsa

```



Depois disso, abra seu arquivo `./src/index.js` e importe essas bibliotecas da seguinte maneira:



```

// ... other require statements ...
const jwt = require('express-jwt');
const jwksRsa = require('jwks-rsa');

```



Então, ainda neste arquivo, crie a seguinte constante logo antes do primeiro ponto final do POST (`app.post`):



```

// ... require statements ...

// ... app definitions ...

// ... app.get endpoints ...

const checkJwt = jwt({
  secret: jwksRsa.expressJwtSecret({
    cache: true,
    rateLimit: true,
    jwksRequestsPerMinute: 5,
    jwksUri: `https://<YOUR_AUTH0_DOMAIN>/.well-known/jwks.json`
  }),

  // Validate the audience and the issuer.
  audience: '<YOUR_AUTH0_CLIENT_ID>',
  issuer: `https://<YOUR_AUTH0_DOMAIN>/`,
  algorithms: ['RS256']
});

// ... app.post endpoints ...

// ... app.listen ...

```



Essa constante é na verdade um middleware Express que validará os [tokens de ID](https://auth0.com/docs/tokens/id-token) . Observe que, para que funcione, você terá que substituir o `<YOUR_AUTH0_CLIENT_ID>` espaço reservado pelo valor apresentado no campo *ID* do *cliente* do seu aplicativo Auth0. Além disso, você terá que substituir `<YOUR_AUTH0_DOMAIN>` pelo valor apresentado no campo *Domínio* (por exemplo `bk-tmp.auth0.com`).

Então, você terá que fazer com que seus dois pontos de extremidade POST usem o `checkJwt` middleware. Para fazer isso, substitua esses pontos de extremidade por isso:



```

// insert a new question
app.post('/', checkJwt, (req, res) => {
  const {title, description} = req.body;
  const newQuestion = {
    id: questions.length + 1,
    title,
    description,
    answers: [],
    author: req.user.name,
  };
  questions.push(newQuestion);
  res.status(200).send();
});

// insert a new answer to a question
app.post('/answer/:id', checkJwt, (req, res) => {
  const {answer} = req.body;

  const question = questions.filter(q => (q.id === parseInt(req.params.id)));
  if (question.length > 1) return res.status(500).send();
  if (question.length === 0) return res.status(404).send();

  question[0].answers.push({
    answer,
    author: req.user.name,
  });

  res.status(200).send();
});

```



Ambos os endpoints introduzem apenas duas alterações. Primeiro, os dois declaram que querem usar `checkJwt`, o que os torna indisponíveis para usuários não autenticados. Em segundo lugar, ambos adicionam uma nova propriedade chamada `author` perguntas e respostas. Essas novas propriedades recebem o nome (`req.user.name`) das solicitações de emissão dos usuários.

Com essas alterações, você pode iniciar sua API de backend novamente (`node src`) e começar a refatorar seu aplicativo React.

> **Nota:** Você não está incluindo o `checkJwt` middleware em seus terminais GET porque deseja que eles sejam publicamente acessíveis. Ou seja, você deseja que usuários não autenticados possam ver perguntas e respostas, mas não deseja que eles criem novas perguntas nem respondam aos existentes.


> **Segunda Nota:** Como sua API de back-end está apenas retendo dados na memória, reiniciá-los faz com que você perca todas as perguntas e respostas inseridas anteriormente. Para adicionar novas perguntas `curl`, você teria que buscar um ID Token de Auth0. No entanto, você pode esperar até concluir o aplicativo inteiro para adicionar perguntas e respostas por meio da interface do seu aplicativo.


## Protegendo seu aplicativo React com Auth0

Para garantir a sua Reagir aplicação com Auth0, você terá de instalar apenas uma biblioteca: `auth0-js`. Esta é a biblioteca oficial fornecida pelo Auth0 para proteger os SPAs como o seu. Para instalá-lo, pare o servidor de desenvolvimento e emita este comando:



```

# from the frontend directory
npm install auth0-js

```



Depois disso, você pode criar uma classe para ajudá-lo com o fluxo de trabalho de autenticação. Para isso, crie um novo arquivo chamado `Auth.js` dentro do `src` diretório e insira o seguinte código:



```

import auth0 from 'auth0-js';

class Auth {
  constructor() {
    this.auth0 = new auth0.WebAuth({
      // the following three lines MUST be updated
      domain: '<YOUR_AUTH0_DOMAIN>',
      audience: 'https://<YOUR_AUTH0_DOMAIN>/userinfo',
      clientID: '<YOUR_AUTH0_CLIENT_ID>',
      redirectUri: 'http://localhost:3000/callback',
      responseType: 'id_token',
      scope: 'openid profile'
    });

    this.getProfile = this.getProfile.bind(this);
    this.handleAuthentication = this.handleAuthentication.bind(this);
    this.isAuthenticated = this.isAuthenticated.bind(this);
    this.signIn = this.signIn.bind(this);
    this.signOut = this.signOut.bind(this);
  }

  getProfile() {
    return this.profile;
  }

  getIdToken() {
    return this.idToken;
  }

  isAuthenticated() {
    return new Date().getTime() < this.expiresAt;
  }

  signIn() {
    this.auth0.authorize();
  }

  handleAuthentication() {
    return new Promise((resolve, reject) => {
      this.auth0.parseHash((err, authResult) => {
        if (err) return reject(err);
        if (!authResult || !authResult.idToken) {
          return reject(err);
        }
        this.idToken = authResult.idToken;
        this.profile = authResult.idTokenPayload;
        // set the time that the id token will expire at
        this.expiresAt = authResult.idTokenPayload.exp * 1000;
        resolve();
      });
    })
  }

  signOut() {
    // clear id token, profile, and expiration
    this.idToken = null;
    this.profile = null;
    this.expiresAt = null;
  }
}

const auth0Client = new Auth();

export default auth0Client;

```



> **Nota:** Assim como antes, você terá que substituir `<YOUR_AUTH0_CLIENT_ID>` e `<YOUR_AUTH0_DOMAIN>` com os valores extraídos do seu aplicativo Auth0.


Como você pode ver, neste arquivo, você está criando um módulo que define a `Auth` classe com sete métodos:

* `constructor`: Aqui, você cria uma instância `auth0.WebAuth` com seus valores Auth0 e define algumas outras configurações importantes. Por exemplo, você está definindo que Auth0 redirecionará os usuários (`redirectUri`) para o `http://localhost:3000/callback` URL (o mesmo que você inseriu anteriormente no campo URLs permitidos de retorno de chamada ).
* `getProfile`: Este método retorna o perfil do usuário autenticado, se houver.
* `getIdToken`: Este método retorna o `idToken` gerado por Auth0 para o usuário atual. Isso é o que você usará ao emitir solicitações para os pontos de extremidade do POST.
* `handleAuthentication`: Esse é o método que seu aplicativo chamará logo após o usuário ser redirecionado do Auth0. Esse método simplesmente lê o segmento hash da URL para buscar os detalhes do usuário e o token de id.
* `isAuthenticated`: Este método retorna se há um usuário autenticado ou não.
* `signIn`: Este método inicializa o processo de autenticação. Em outras palavras, esse método envia seus usuários para a página de login do Auth0.
* `signOut`: Este método assina um usuário para fora, definindo o `profile`, `id_token` e `expiresAt` para `null`.


Por último, este módulo cria uma instância da `Auth` classe e a expõe ao mundo. Ou seja, no seu aplicativo, você não terá mais de uma instância da `Auth` turma.

Depois de definir essa classe auxiliar, você pode refatorar seu componente `NavBar` para permitir que os usuários se autentiquem. Então, abra o arquivo `NavBar.js` e substitua seu código pelo seguinte:



```

import React from 'react';
import {Link, withRouter} from 'react-router-dom';
import auth0Client from '../Auth';

function NavBar(props) {
  const signOut = () => {
    auth0Client.signOut();
    props.history.replace('/');
  };

  return (
    <nav className="navbar navbar-dark bg-primary fixed-top">
      <Link className="navbar-brand" to="/">
        Q&App
      </Link>
      {
        !auth0Client.isAuthenticated() &&
        <button className="btn btn-dark" onClick={auth0Client.signIn}>Sign In</button>
      }
      {
        auth0Client.isAuthenticated() &&
        <div>
          <label className="mr-2 text-white">{auth0Client.getProfile().name}</label>
          <button className="btn btn-dark" onClick={() => {signOut()}}>Sign Out</button>
        </div>
      }
    </nav>
  );
}

export default withRouter(NavBar);

```



A nova versão do componente da barra de navegação importa dois novos elementos:


* `withRouter`: Este é um componente fornecido pelo React Router para melhorar seu componente [com recursos de navegação](https://reacttraining.com/react-router/web/api/withRouter) (por exemplo, acesso ao objeto `history`).
* `auth0Client`: Esta é a [instância singleton](https://en.wikipedia.org/wiki/Singleton_pattern) da `Auth` classe que você acabou de definir.


Com a instância `auth0Client`, o usuário `NavBar` decide se deve processar um botão *Sign In* (que é usado para usuários não autenticados) ou um botão *Sign Out* (para usuários autenticados). Se o usuário estiver devidamente autenticado, esse componente também mostrará seu nome. E, se um usuário autenticado acessar o botão *Sign Out* , seu componente chamará o método `signOut` e `auth0Client`  redirecionará o usuário para a home page.

Após refatorar o componente `NavBar`, você terá que criar um componente para manipular a rota de retorno de chamada (`http://localhost:3000/callback`). Para definir este componente, crie um novo arquivo chamado `Callback.js` dentro do diretório `src` e insira o seguinte código nele:



```

import React, {Component} from 'react';
import {withRouter} from 'react-router-dom';
import auth0Client from './Auth';

class Callback extends Component {
  async componentDidMount() {
    await auth0Client.handleAuthentication();
    this.props.history.replace('/');
  }

  render() {
    return (
      <p>Loading profile...</p>
    );
  }
}

export default withRouter(Callback);

```



O componente que você acabou de definir é responsável por duas coisas. Primeiro, ele chama o método `handleAuthentication` para buscar as informações do usuário enviadas por Auth0. Em segundo lugar, ele redireciona seus usuários para a home page (`history.replace('/')`) depois de concluir o processo `handleAuthentication`. Enquanto isso, este componente mostra a seguinte mensagem: "Carregando perfil".

Então, para envolver a integração com o Auth0, você terá que abrir o arquivo `App.js` e atualizá-lo da seguinte maneira:



```

// ... other import statements ...
import Callback from './Callback';

class App extends Component {
  render() {
    return (
      <div>
        <!-- ... NavBar and the other two Routes ... -->
        <Route exact path='/callback' component={Callback}/>
      </div>
    );
  }
}

export default App;

```



Agora, se você executar seu aplicativo React novamente (`npm start`), poderá se autenticar por meio do Auth0. Após o processo de autenticação, você poderá ver seu nome na barra de navegação.

![React autenticação de usuário do aplicativo Q & A com Auth0](https://cdn.auth0.com/blog/react-tutorial/securing-react-apps-with-auth0.png)

## Adicionando Recursos a Usuários Autenticados

Agora que você concluiu a integração do Auth0 ao seu aplicativo React, é possível começar a adicionar recursos aos quais somente usuários autenticados terão acesso. Para concluir este tutorial, você implementará dois recursos. Primeiro, você permitirá que usuários autenticados criem novas perguntas. Em seguida, você refatorará o componente `Question` (singular) para mostrar um formulário para que os usuários autenticados possam responder a essas perguntas.

Para o primeiro recurso, você criará uma nova rota em seu aplicativo `/new-question`. Essa rota será protegida por um componente que verificará se o usuário está autenticado ou não. Se o usuário ainda não estiver autenticado, esse componente os redirecionará para Auth0 para que eles possam fazer isso. Se o usuário já estiver autenticado, o componente permitirá que o React renderize o formulário no qual novas perguntas serão criadas.

Então, para começar, você irá criar um novo diretório chamado `SecuredRoute` e criar um arquivo chamado `SecuredRoute.js` dentro dele. Então, neste arquivo, você irá inserir o seguinte código:



```

import React from 'react';
import {Route} from 'react-router-dom';
import auth0Client from '../Auth';

function SecuredRoute(props) {
  const {component: Component, path} = props;
  return (
    <Route path={path} render={() => {
        if (!auth0Client.isAuthenticated()) {
          auth0Client.signIn();
          return <div></div>;
        }
        return <Component />
    }} />
  );
}

export default SecuredRoute;

```



O objetivo deste componente é restringir o acesso a qualquer rota que você configurar nele. A implementação disso é bem simples. Nesse caso, você está criando um componente funcional que usa duas propriedades: outra `Component`, para poder renderizá-lo caso o usuário seja autenticado; e a `path`, para que possa configurar o componente `Route` padrão fornecido pelo Roteador React. No entanto, antes de processar qualquer coisa, este componente verifica se o usuário `isAuthenticated`. Se não estiverem, esse componente acionará o método `signIn` para redirecionar os usuários para a página de login.

Em seguida, após criar o componente `SecuredRoute`, você poderá criar o componente que renderizará o formulário no qual os usuários criarão perguntas. Para isso, crie um novo diretório chamado `NewQuestion` e um arquivo chamado `NewQuestion.js` dentro dele. Em seguida, insira este código no arquivo:



```

import React, {Component} from 'react';
import {withRouter} from 'react-router-dom';
import auth0Client from '../Auth';
import axios from 'axios';

class NewQuestion extends Component {
  constructor(props) {
    super(props);

    this.state = {
      disabled: false,
      title: '',
      description: '',
    };
  }

  updateDescription(value) {
    this.setState({
      description: value,
    });
  }

  updateTitle(value) {
    this.setState({
      title: value,
    });
  }

  async submit() {
    this.setState({
      disabled: true,
    });

    await axios.post('http://localhost:8081', {
      title: this.state.title,
      description: this.state.description,
    }, {
      headers: { 'Authorization': `Bearer ${auth0Client.getIdToken()}` }
    });

    this.props.history.push('/');
  }

  render() {
    return (
      <div className="container">
        <div className="row">
          <div className="col-12">
            <div className="card border-primary">
              <div className="card-header">New Question</div>
              <div className="card-body text-left">
                <div className="form-group">
                  <label htmlFor="exampleInputEmail1">Title:</label>
                  <input
                    disabled={this.state.disabled}
                    type="text"
                    onBlur={(e) => {this.updateTitle(e.target.value)}}
                    className="form-control"
                    placeholder="Give your question a title."
                  />
                </div>
                <div className="form-group">
                  <label htmlFor="exampleInputEmail1">Description:</label>
                  <input
                    disabled={this.state.disabled}
                    type="text"
                    onBlur={(e) => {this.updateDescription(e.target.value)}}
                    className="form-control"
                    placeholder="Give more context to your question."
                  />
                </div>
                <button
                  disabled={this.state.disabled}
                  className="btn btn-primary"
                  onClick={() => {this.submit()}}>
                  Submit
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    )
  }
}

export default withRouter(NewQuestion);

```



Embora seja longo, o código desse componente não é complexo. Como você pode ver, nesse caso, você precisou criar um componente de classe para poder manter o seguinte estado:

* `disabled`: Você está usando isso para desativar os elementos de entrada depois que o usuário pressiona o botão *Enviar*.
*`title`: Você está usando isso para permitir que os usuários definam o título da pergunta que está sendo feita.
* `description`: Você está usando isso para permitir que os usuários definam a descrição da pergunta.

Além disso, você pode ver que você precisava de três métodos além `constructor` e `render`:

* `updateDescription`: Este método é responsável por atualizar o `description` estado do componente.
* `updateTitle`: Este método é responsável por atualizar o `description` estado do componente.
* `submit`: Esse método é responsável por emitir a nova questão para o backend e bloquear os campos de entrada enquanto a solicitação está sendo feita.

Observe que, no método `submit`, você está usando `auth0Client` para obter o token de ID do usuário atual para incluí-lo na solicitação. Sem esse token, a API de back-end negaria a solicitação.

Da perspectiva da interface do usuário, esse componente está usando várias classes do Bootstrap para produzir uma boa forma. [Certifique-se de verificar este recurso depois de concluir o tutorial, se precisar aprender sobre formulários no Bootstrap](https://getbootstrap.com/docs/4.1/components/forms/) .

Agora, para ver isso funcionando, você terá que atualizar dois arquivos. Primeiro, você terá que registrar a nova rota no seu arquivo `App.js`:



```

// ... other import statements ...
import NewQuestion from './NewQuestion/NewQuestion';
import SecuredRoute from './SecuredRoute/SecuredRoute';

class App extends Component {
  render() {
    return (
      <div>
        <!-- ... navbar and other routes ... -->
        <SecuredRoute path='/new-question' component={NewQuestion} />
      </div>
    );
  }
}

export default App;

```



Em seguida, você terá que adicionar um link no arquivo `Questions.js` para essa nova rota. Para fazer isso, abra este arquivo e atualize-o da seguinte maneira:



```

// ... import statements ...

class Questions extends Component {
  // ... constructor and componentDidMount ...

  render() {
    return (
      <div className="container">
        <div className="row">
          <Link to="/new-question">
            <div className="card text-white bg-secondary mb-3">
              <div className="card-header">Need help? Ask here!</div>
              <div className="card-body">
                <h4 className="card-title">+ New Question</h4>
                <p className="card-text">Don't worry. Help is on the way!</p>
              </div>
            </div>
          </Link>
          <!-- ... loading questions message ... -->
          <!-- ... questions' cards ... -->
        </div>
      </div>
    )
  }
}

export default Questions;

```


Com essas alterações, você poderá criar novas perguntas após a autenticação.

![React app de perguntas e respostas para enviar conteúdo por meio de formulário protegido po Auth0](https://cdn.auth0.com/blog/react-tutorial/form-in-a-react-app.png)

Em seguida, para finalizar os recursos do seu aplicativo, você pode refatorar o componente `Question` para incluir um formulário no qual os usuários poderão responder a perguntas. Para definir este formulário, crie um novo arquivo chamado `SubmitAnswer.js` dentro do diretório `Question` com o seguinte código:



```

import React, {Component, Fragment} from 'react';
import {withRouter} from 'react-router-dom';
import auth0Client from '../Auth';

class SubmitAnswer extends Component {
  constructor(props) {
    super(props);
    this.state = {
      answer: '',
    };
  }

  updateAnswer(value) {
    this.setState({
      answer: value,
    });
  }

  submit() {
    this.props.submitAnswer(this.state.answer);

    this.setState({
      answer: '',
    });
  }

  render() {
    if (!auth0Client.isAuthenticated()) return null;
    return (
      <Fragment>
        <div className="form-group text-center">
          <label htmlFor="exampleInputEmail1">Answer:</label>
          <input
            type="text"
            onChange={(e) => {this.updateAnswer(e.target.value)}}
            className="form-control"
            placeholder="Share your answer."
            value={this.state.answer}
          />
        </div>
        <button
          className="btn btn-primary"
          onClick={() => {this.submit()}}>
          Submit
        </button>
        <hr className="my-4" />
      </Fragment>
    )
  }
}

export default withRouter(SubmitAnswer);

```



Esse componente funciona de maneira semelhante ao `NewQuestion` componente. A diferença aqui é que, em vez de manipular a solicitação POST sozinha, o componente a delega para outra pessoa. Além disso, se o usuário não for autenticado, esse componente não renderiza nada.

Para usar este componente, abra o arquivo `Question.js` e substitua seu conteúdo por:



```

import React, {Component} from 'react';
import axios from 'axios';
import SubmitAnswer from './SubmitAnswer';
import auth0Client from '../Auth';

class Question extends Component {
  constructor(props) {
    super(props);
    this.state = {
      question: null,
    };

    this.submitAnswer = this.submitAnswer.bind(this);
  }

  async componentDidMount() {
    await this.refreshQuestion();
  }

  async refreshQuestion() {
    const { match: { params } } = this.props;
    const question = (await axios.get(`http://localhost:8081/${params.questionId}`)).data;
    this.setState({
      question,
    });
  }

  async submitAnswer(answer) {
    await axios.post(`http://localhost:8081/answer/${this.state.question.id}`, {
      answer,
    }, {
      headers: { 'Authorization': `Bearer ${auth0Client.getIdToken()}` }
    });
    await this.refreshQuestion();
  }

  render() {
    const {question} = this.state;
    if (question === null) return <p>Loading ...</p>;
    return (
      <div className="container">
        <div className="row">
          <div className="jumbotron col-12">
            <h1 className="display-3">{question.title}</h1>
            <p className="lead">{question.description}</p>
            <hr className="my-4" />
            <SubmitAnswer questionId={question.id} submitAnswer={this.submitAnswer} />
            <p>Answers:</p>
            {
              question.answers.map((answer, idx) => (
                <p className="lead" key={idx}>{answer.answer}</p>
              ))
            }
          </div>
        </div>
      </div>
    )
  }
}

export default Question;

```



Aqui, você pode ver que está definindo o método `submitAnswer` que emitirá as solicitações para a API de back-end (com o ID do usuário) e que está definindo um método chamado `refreshQuestion`. Esse método atualizará o conteúdo da pergunta em duas situações, na primeira vez que o React renderizar esse componente (`componentDidMount`) e logo após a API de backend responder à solicitação POST do método `submitAnswer`.

Após refatorar o componente `Question`, você terá uma versão completa do seu aplicativo. Para testá-lo, você pode ir `http://localhost:3000/` e começar a usar seu aplicativo React completo. Depois de fazer o login, você poderá fazer perguntas e poderá respondê-las também. Quão legal é isso?

![Demonstração completa do tutorial de aplicativo de P & R React](https://cdn.auth0.com/blog/react-tutorial/creating-your-first-react-app.png)

## Mantendo os usuários conectados após uma atualização

Embora você tenha um aplicativo totalmente funcional, depois de fazer login no seu aplicativo, se atualizar seu navegador, você perceberá que será desconectado. Por que é que? Porque você está salvando seus tokens na memória (como deveria) e porque a memória é apagada quando você clica em Atualizar. Não é o melhor comportamento, certo?

Felizmente, resolver esse problema é fácil. Você terá que aproveitar a [*Autenticação Silenciosa*](https://auth0.com/docs/api-auth/tutorials/silent-authentication) fornecida por Auth0. Ou seja, sempre que seu aplicativo for carregado, ele enviará uma solicitação silenciosa para Auth0 para verificar se o usuário atual (na verdade, o navegador) tem uma sessão válida. Se o fizerem, o Auth0 enviará de volta para você um `idToken` e um `idTokenPayload`, assim como no retorno de chamada de autenticação.

Para usar a autenticação silenciosa, você terá que refatorar duas classes: `Auth` e `App`. No entanto, antes de refatorar essas classes, você precisará alterar algumas configurações em sua conta Auth0.

Para começar, você terá que ir para [a seção *Aplicativos* no seu painel Auth0](https://manage.auth0.com/#/applications) , abrir o aplicativo que representa seu aplicativo React e alterar dois campos:


1. *Origens da web permitidas*: como seu aplicativo emitirá uma solicitação AJAX para Auth0, você precisará adicionar `http://localhost:3000` a esse campo. Sem esse valor, o Auth0 negaria qualquer solicitação AJAX proveniente do seu aplicativo.
2. *URLs de logout permitidos*: para permitir que os usuários encerrem a sessão em Auth0, você precisará chamar [o ponto de extremidade de logout](https://auth0.com/docs/logout#log-out-a-user). Da mesma forma que o endpoint de autorização, o ponto de extremidade de logout apenas redireciona os usuários para URLs whitelisted após o processo. Como tal, você terá que adicionar `http://localhost:3000` neste campo também.


Depois de atualizar esses campos, você pode clicar no botão *Salvar alterações*. Então, a última coisa que você terá que fazer antes de se concentrar no código do seu aplicativo é substituir as chaves de desenvolvimento que o Auth0 está usando para permitir que os usuários se autentiquem pelo Google.

Você pode não ter notado, mas, mesmo que não tenha configurado nada relacionado ao Google em sua conta do Auth0, o botão de login social está lá e funciona bem. A única razão pela qual esse recurso funciona imediatamente é porque o Auth0 configura automaticamente todas as novas contas para usar as chaves de desenvolvimento registradas no Google. No entanto, quando os desenvolvedores começam a usar o Auth0 com mais seriedade, espera-se que eles substituam essas chaves por suas próprias. E, para forçar isso, toda vez que um aplicativo tentar executar uma autenticação silenciosa e esse aplicativo ainda estiver usando as chaves de desenvolvimento, o Auth0 retornará que não há sessão ativa (mesmo que isso não seja verdade).

Então, para alterar essas chaves, vá para [*as conexões sociais no seu painel*](https://manage.auth0.com/#/connections/social) e clique no Google. Lá, você verá dois campos, entre outros: *ID do cliente e Segredo do cliente*. É aqui que você irá inserir suas chaves. Para obter suas chaves, leia [o documento *Conecte seu aplicativo à documentação do Google* fornecido pelo Auth0](https://manage.auth0.com/#/connections/social/google).


> **Nota:** se não pretender utilizar as suas chaves Google, pode desativar esta ligação social e confiar apenas nos utilizadores que se inscrevem na sua aplicação através da autenticação de nome de [*utilizador e palavra-passe*](https://manage.auth0.com/#/connections/database) da Auth0.


Agora que você terminou de configurar sua conta do Auth0, pode voltar ao seu código. Lá, abra o arquivo `./src/Auth.js` do seu aplicativo React e atualize-o da seguinte maneira:



```

import auth0 from 'auth0-js';

class Auth {
  // ... constructor, getProfile, getIdToken, isAuthenticated, signIn ...

  handleAuthentication() {
    return new Promise((resolve, reject) => {
      this.auth0.parseHash((err, authResult) => {
        if (err) return reject(err);
        if (!authResult || !authResult.idToken) {
          return reject(err);
        }
        this.setSession(authResult);
        resolve();
      });
    })
  }

  setSession(authResult) {
    this.idToken = authResult.idToken;
    this.profile = authResult.idTokenPayload;
    // set the time that the id token will expire at
    this.expiresAt = authResult.idTokenPayload.exp * 1000;
  }

  signOut() {
    this.auth0.logout({
      returnTo: 'http://localhost:3000',
      clientID: '<YOUR_AUTH0_CLIENT_ID>',
    });
  }

  silentAuth() {
    return new Promise((resolve, reject) => {
      this.auth0.checkSession({}, (err, authResult) => {
        if (err) return reject(err);
        this.setSession(authResult);
        resolve();
      });
    });
  }
}

// ... auth0Client and export ...

```



> **Nota:** Você terá que substituir `<YOUR_AUTH0_CLIENT_ID>` pelo ID do cliente do seu aplicativo Auth0. Você terá que usar o mesmo valor que você está usando para configurar `audience` o objeto passado `auth0.WebAuth` no construtor desta classe.

Na nova versão desta classe, você é:

* a adição de um método para configurar detalhes dos usuários: `setSession`;
* refatorando o método `handleAuthentication` para usar o método `setSession`;
* adicionando um método chamado `silentAuth` para chamar a `checkSession` função fornecida por `auth0-js` (este método também usa `setSession`);
* e refatorar a função `signOut` para chamar o ponto de extremidade de logout em Auth0 e informar onde os usuários devem ser redirecionados depois disso (isto é, `returnTo`: `'http://localhost:3000'`);


Então, para finalizar as coisas, você terá que abrir o arquivo `./src/App.js` e atualizá-lo da seguinte maneira:



```

// ... other imports ...
import {Route, withRouter} from 'react-router-dom';
import auth0Client from './Auth';

class App extends Component {
  async componentDidMount() {
    if (this.props.location.pathname === '/callback') return;
    try {
      await auth0Client.silentAuth();
      this.forceUpdate();
    } catch (err) {
      if (err.error !== 'login_required') console.log(err.error);
    }
  }

  // ... render ...
}

export default withRouter(App);

```



Como você pode ver, a nova versão deste arquivo está definindo o que fazer quando seu aplicativo é carregado (`componentDidMount`):


1. Se a rota solicitada for `/callback`, o aplicativo não faz nada. Esse é o comportamento correto porque, quando os usuários estão solicitando a rota `/callback`, eles o fazem porque estão sendo redirecionados pelo Auth0 após o processo de autenticação. Nesse caso, você pode deixar o componente `callback` manipular o processo.
2. Se a rota solicitada é outra coisa, o aplicativo quer tentar um `silentAuth`. Então, se nenhum erro ocorrer, o aplicativo chamará `forceUpdate` para que o usuário possa ver o que foi solicitado.
3. Se houver um erro no `silentAuth`, o aplicativo verificará se o erro é diferente de `login_required`. Se este for o caso, o aplicativo registra o problema. Caso contrário, o aplicativo não faz nada porque significa que o usuário não está conectado (ou que você está usando chaves de desenvolvimento, o que você não deveria).


> By the way, você está colocando sua classe `App` dentro da `withRouter` função para que você possa verificar qual rota está sendo chamada (`this.props.location.pathname`). Sem `withRouter`, você não teria acesso ao objeto `location`.


## Evitando redirecionar usuários autenticados para Auth0

Antes que você chame um dia, há uma última coisa que você terá que fazer. A solução acima funcionará sem problemas se você estiver em qualquer rota, exceto a protegida. Se você estiver na rota protegida (ou seja, em `/new-question`) e atualizar seu navegador, será redirecionado para Auth0 para fazer login novamente. O problema aqui é que o componente `SecuredRoute` verifica se os usuários estão autenticados ou não (`if (!auth0Client.isAuthenticated())`) antes que o aplicativo receba uma resposta do processo de autenticação silenciosa. Dessa forma, o aplicativo acredita que seus usuários não estão autenticados e os redireciona para Auth0 (`auth0Client.signIn();`) para que eles possam fazer login.

Para corrigir esse mau comportamento, você terá que abrir o `SecuredRoute.js` arquivo e atualizá-lo da seguinte maneira:



```

// ... import statements ...
function SecuredRoute(props) {
  const {component: Component, path, checkingSession} = props;
  return (
    <Route path={path} render={() => {
      if (checkingSession) return <h3 className="text-center">Validating session...</h3>;
      // ... leave the rest untouched ...
     }} />
  );
}

export default SecuredRoute;

```



A diferença agora é que seu componente `SecuredRoute` irá verificar um chamado booleano `checkingSession` que vem `props` e, se este booleano estiver definido `true`, ele mostrará um `h3` elemento dizendo que o aplicativo está *validando a sessão* . Se essa propriedade for definida como `false`, o componente se comportará como antes.

Agora, para passar essa propriedade para `SecuredRoute`, você terá que abrir o arquivo `App.js` e atualizá-lo da seguinte maneira:



```

// ... import statements ...
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      checkingSession: true,
    }
  }

  async componentDidMount() {
    if (this.props.location.pathname === '/callback') {
      this.setState({checkingSession:false});
      return;
    }
    // ... leave try-catch untouched
    this.setState({checkingSession:false});
  }

  render() {
    // ... leave other routes untouched ...
    // replace SecuredRoute with this:
    <SecuredRoute path='/new-question'
                  component={NewQuestion}
                  checkingSession={this.state.checkingSession} />
  }
}

export default withRouter(App);

```



É isso aí! Após essas alterações, você finalmente terminou de desenvolver seu aplicativo React. Agora, se você fizer login e atualizar seu navegador (não importa em qual rota você esteja), verá que não perderá sua sessão e que não precisará fazer login novamente. Viva!


> "Acabei de criar o meu primeiro aplicativo React".


## Conclusão

Neste artigo, você teve a chance de jogar com várias tecnologias e conceitos interessantes. Primeiro, você aprendeu sobre alguns conceitos importantes que o React introduz (como a *arquitetura* do *componente* e a sintaxe do JSX). Em seguida, você aprendeu brevemente como criar uma API de back-end com o Node.js e o Express. Depois disso, você aprendeu como criar um aplicativo React legal e como proteger a coisa toda com Auth0.

Como o artigo introduziu muitos tópicos diferentes, você realmente não teve a chance de compreender todos eles. Por exemplo, você mal tocou a ponta do iceberg em alguns conceitos importantes, como o *ciclo de vida* do *componente*. Você também não teve a chance de aprender o que dá à React uma base sólida quando se trata de manipular elementos HTML. Infelizmente, mergulhar profundamente nesses tópicos não é possível, pois tornaria o artigo massivo (mais do que já é).

Então, agora que você terminou de desenvolver o seu primeiro aplicativo Reagir, certifique-se de verificar as ligações e referências deixadas durante todo o tutorial e, para aprender mais sobre como Reagir obras, não deixe de conferir [o *DOM e Internals Virtual* artigo](https://reactjs.org/docs/faq-internals.html) .

Além disso, se precisar de ajuda, não hesite em deixar uma mensagem na seção de comentários abaixo. Felicidades!

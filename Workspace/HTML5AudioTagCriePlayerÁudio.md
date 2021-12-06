# HTML5 Audio Tag: Crie um player de Áudio com HTML5

## Veja nesse artigo como desenvolver um player de áudio utilizando a nova Audio Tag. Tag que permite que arquivos de áudio sejam reproduzidos via HTML5.

- SUPORTE AO ALUNO
- ANOTAÇÕES
- FAVORITAR
- CONCLUÍDO
- **29**GOSTEI
- 

- **29**
- 
- 

[Este Artigo faz parte da RevistaFront-end Magazine 1Ver Revista](https://www.devmedia.com.br/revista-front-end-magazine-1/31029)

Por que eu devo ler este artigo:A criação de plugins customizáveis no mundo de desenvolvimento de softwares web sempre ocupou espaço de destaque entre os desenvolvedores front-end e web designers. Aliada ao uso das [tecnologias JavaScript](https://www.devmedia.com.br/curso/curso-de-javascript-completo/388), HTML 5 (em sua nova versão com muito mais recursos), e bibliotecas de script prontas como o jQuery e afins, assim como às documentações bem elaboradas, a produtividade para criar e usar tais plugins cresce exponencialmente. Neste artigo será apresentado um tutorial de como utilizar tais tecnologias e plugins para criar um player de música para browser, explorando recursos famosos em aplicativos desktop que podem ser traduzidos para o âmbito web.

Ver mais

Suporte ao alunoAnotarMarcar como concluídoCódigo fonte

[Artigos](https://www.devmedia.com.br/artigos/)[HTML e CSS](https://www.devmedia.com.br/artigos/front-end-web)HTML5 Audio Tag: Crie um player de Áudio com HTML5

Na maior parte dos casos, executar músicas no plano de fundo de um site é uma má ideia, uma vez que o usuário não está preparado para lidar com o fator subjetividade. As músicas podem influenciar na decisão de se o usuário deve ou não continuar no site ou visitá-lo novamente no futuro, tal como o design de uma aplicação também se torna extremamente importante nesse ponto de vista. Mas, especificamente em algumas páginas da web, pode ser uma ideia bem interessante, tais como em sites relacionados ao tema música, blogs com podcasts e afins.

Por muito tempo, as formas mais comuns de se ter este tipo de conteúdo era utilizando um player de música em flash ou através de plug-ins específicos de programas instalados no computador do usuário, como o Windows Media Player, o Real Player ou o Quick Time, por exemplo. Até então, havia um grande problema quando da utilização dos plug-ins citados: a impossibilidade de customização do player, já que sua aparência iria seguir o padrão do software instalado no computador do usuário. Veja na **Figura 1** um exemplo de player de música com o plugin do Windows Media Player no Internet Explorer.

![Plugin do Windows Media Player no Internet Explorer 10](https://arquivo.devmedia.com.br/revistas/front_end/imagens/5/image002.jpg)**Figura 1**. Plugin do Windows Media Player no Internet Explorer 10

De tal forma, o trabalho de projeção do site ficaria comprometido, uma vez que o mesmo estaria preso a elementos gráficos e de design específicos que, certamente, não encaixariam com a ideia original do desenvolvedor para o design do site.

Algumas soluções alternativas poderiam ser usadas para burlar esse problema. A tecnologia Flash é um bom exemplo disso, já que não sofria com esse tipo de problema de customização, mas tinha os seus próprios. Desempenho era um deles. O Flash nunca teve um desempenho muito bom fora do Windows e esse tipo de problema ultrapassa o universo dos computadores desktop chegando a acontecer também no mundo móvel. Além disso, o Flash não está presente em todos os dispositivos móveis. O iOS, por exemplo, nunca ofereceu suporte. Já o Android possui em algumas versões da plataforma, mas não é algo tão indicado para um smartphone, pelo alto consumo de recursos de CPU, bateria, etc.

Outra opção mais recente e interessante é a [HTML5](https://www.devmedia.com.br/curso/curso-de-html5/275), que traz consigo a possibilidade de adicionar músicas e vídeos nas páginas sem a necessidade de plug-ins, deixando a responsabilidade de reproduzir os arquivos por conta do browser. A vantagem é que os esforços podem ser focados no desenvolvimento do restante do escopo, deixando todo o resto com o browser. Os pontos negativos são a incompatibilidade com alguns browsers, assim como o fato de que cada navegador assume um design próprio para exibir o player (**Figura 2**).

![Players dos navegadores Internet Explorer, Firefox, Opera e Chrome (respectivamente)](https://arquivo.devmedia.com.br/revistas/front_end/imagens/5/image003.jpg)**Figura 2**. Players dos navegadores Internet Explorer, Firefox, Opera e Chrome (respectivamente)

Felizmente a **HTML5** provê uma API bastante flexível que permite que a comunidade de desenvolvedores crie novas soluções para tornar o processo de inserção de conteúdo multimídia nas páginas mais simples e prático.

### A construção do player

O objetivo deste artigo será mostrar como fazer um player simples de áudio, utilizando uma biblioteca para a jQuery bastante flexível, chamada **jPlayer**, que funciona tanto para browsers modernos (com suporte à API de áudio do HTML5), quanto para os mais antigos. Essa compatibilidade de browsers é proporcionada através da utilização do Flash quando o browser do usuário não suporta a API de áudio do HTML5. Além disso, utilizando essa biblioteca, o player desenvolvido estará pronto para reproduzir áudio em dispositivos móveis.

O [player de áudio](https://www.devmedia.com.br/html5-audio-player-dica/28576) que criaremos aqui foi testado nos navegadores Chrome, Opera, Internet Explorer 7+ e Firefox, assim como os browsers mobile padrão do Android 4, Opera mobile no Android 4, Internet Explorer no Windows Phone e Safari no iOS. O leitor pode ficar a vontade para testar em outros browsers de sua preferência.

Para conseguir entender e, consequentemente, aproveitar este tutorial ao máximo, você precisará ter alguns conhecimentos de JavaScript, tal como saber o que são e como usar objetos, arrays, funções etc., além de ter tido algum contato com a jQuery e trabalhar razoavelmente bem com HTML e CSS. Quanto mais personalização você quiser no seu player, mais você deverá saber sobre estas linguagens, especialmente JavaScript.

Conforme falado anteriormente, iremos utilizar essencialmente a biblioteca jQuery e o plugin jPlayer, os links de download para ambos podem ser encontrados na seção de **Links** no final desse artigo.

### Preparando o ambiente

Para facilitar o acompanhamento do tutorial, crie a seguinte estrutura de pastas para o projeto, conforme mostra a **Listagem 1**.

```
|-- root
|  |-- css
|  |-- js
|  |  |--plugins
|  |  |  |-- jplayer
|  |-- songs
```

**Listagem 1**. Estrutura de pastas para o projeto do player

A estrutura é simples e bem intuitiva. Mas fique à vontade para modificá-la como quiser, caso não se sinta confortável com a distribuição ou julgue outra ser melhor.

Em seguida, selecione algumas músicas em formato mp3 de sua preferência e coloque-as na pasta “songs”. Para facilitar, deixe-as com nomes curtos, sem espaços ou acentos. Neste exemplo, foram utilizadas a “technologic.mp3” e a “human-after-all.mp3”.

### Marcação e Estilização

Primeiramente vamos criar um molde para marcar nossa página, que servirá como modelo para o local onde o player será inserido. Iremos utilizar um simples e que nos permita focar no objetivo principal, que é a criação do player, tal como exibido na **Figura 3**.

![Modelo para marcar aparência do player](https://arquivo.devmedia.com.br/revistas/front_end/imagens/5/image004.jpg)**Figura 3**. Modelo para marcar aparência do player

Vamos aos detalhes:

- O **item 1** contém os controles para o player. A partir deles conseguiremos iniciar e interromper a execução do som e percorrer a playlist.
- O **item 2** exibe a barra de progresso. A parte mais clara indica o quanto da música já foi reproduzido, e a parte escura quanto ainda está por vir.
- O **item 3** mostra ao usuário o nome da banda e o título da música que está sendo reproduzida.

Tanto os controles quanto todos os outros elementos podem ser estilizados usando CSS. Os elementos também podem ser removidos ou novos podem ser adicionados.

### Codificando

A codificação começa com o HTML. Crie um documento HTML na raiz do seu projeto e nomeie-o “index.html”. Adicione ao mesmo a marcação exibida na **Listagem 2**.

```
<!doctype html>
<html lang="pt-br">
<head>
   <meta charset="utf-8" />
   <title>jPlayer Tutorial</title>

</head>
<body>
   <div class="top-bar">
       <div class="container">
           <div class="player-controls">
               <span class="player-prev">Prev</span>
               <span class="player-play">Play</span>
               <span class="player-pause">Pause</span>
               <span class="player-stop">Stop</span>
               <span class="player-next">Next</span>
           </div>
           <div class="player"></div>
           <div class="player-timeline">
               <div class="player-timeline-control"></div>
           </div>
           <div class="player-display">
               Playing: <span class="player-current-track"></span>
           </div>
       </div>
   </div>
</body>
</html>
```

**Listagem 2**. Marcação HTML inicial para a página do player

Esta é uma marcação bastante simples. A parte relevante para o player é a que está dentro da div que tem a classe “top-bar”.

Vamos analisar cada um dos elementos para entender seus papeis, identificando-os por suas classes CSS.

- .player-controls: este elemento abriga os controles do player. Não é obrigatório, mas ajuda a manter as coisas organizadas;
- .player-prev, .player-pause, .player-stop, .player-next: estes elementos são, de fato, os controles do player. Para que o mesmo ofereça corretamente as funcionalidades esperadas, precisamos destes elementos com estas classes.
- .player: este é um elemento (div) vazio dentro da página no player, isso porque o jPlayer precisa de um elemento do documento para criar o player e seus controles. Iremos então fornecer este, mas ele não terá nada de especial na nossa interface, por isso está vazio. É importante também fornecer um elemento específico, único e que os controles do player não fiquem dentro dele.
- .player-timeline, .player-timeline-control: irão atuar como a barra de progresso, conforme o item 2 da Figura 3.
- .player-display, .layer-current-track: iremos utilizar estes elementos para exibir informações da faixa atual ao usuário. Neste exemplo, serão exibidos apenas o nome do artista e o título da faixa.

Após isso, é necessário agora incluir o arquivo de estilo que será usado na página. Para tanto, crie um novo arquivo na dentro da pasta “css” de nome “default.css” e inclua nele o código contigo na **Listagem 3.** Este código será responsável por adicionar as propriedades padrão para o corpo (body) da página, tais como margem e fonte.

```
body {
   padding: 0;
   margin: 0;
   font-family: sans-serif;
}
```

**Listagem 3**. Conteúdo inicial do arquivo default.css

Neste mesmo arquivo CSS, adicione agora o CSS para o restante dos componentes da página, de forma a deixar as coisas mais agradáveis visualmente. O código referente encontra-se na **Listagem 4**.

**Nota**: A inclusão foi feita em duas listagens para que o leitor possa atentar ao que é CSS principal e secundário. Na **Listagem 3** estamos estilizando o conteúdo geral da página, enquanto na **Listagem 4** estão sendo adicionados recursos de estilo para a barra superior e organização interna dos componentes.

```
.container {
   margin: auto;
   width: 960px;
}
.top-bar{
   width: 100%;
   height: 30px;
   background: #141414;
   color: #888;
   line-height: 30px;
}
.top-bar .player-controls {
   float: left;
}
.top-bar .player-controls span{
   cursor: pointer;
   padding: 0 5px;
   -webkit-transition: all linear 0.2s;
}
.top-bar .player-controls span:hover {
   color: #EEE;
}
.top-bar .player-display {
   float: left;
   float: right;
   margin-left: 50px;
}
.top-bar .player-display .player-current-track {
   color: white;
}
.top-bar .player {
   float: left;
}
.top-bar .player-timeline {
   float: left;
   max-width: 200px;
   width: 200px;
   height: 4px;
   margin-top: 13px;
   background: #555;
   margin-left: 20px;
}
.top-bar .player-timeline-control {
   height: 4px;
   background: #999;
}
```

**Listagem 4**. Restante do conteúdo CSS do arquivo default.css

Finalmente, referencie no arquivo “index.html” a chamada ao arquivo CSS criado, adicionando o código contido na **Listagem 5** ao elemento da mesma.

```
<link rel="stylesheet" href="css/default.css" />
```

**Listagem 5**. Importação do arquivo default.css na página index.html

Não há nada de especial no nosso CSS, mas atente ao estilo das classes “.player-timeline” e “.player-timeline-control”. O elemento “player-timeline-control” irá ficar por cima do “player-timeline” e seu tamanho irá aumentar conforme a música for sendo reproduzida, enquanto o “player-timeline” irá exibir o tamanho total da reprodução. É interessante deixá-las com certo contraste de cores, para que o usuário consiga identificar o que está acontecendo.

Agora é hora de implementar o JavaScript. Paralelo a isso, precisaremos fazer uso também da jQuery. Neste tutorial utilizaremos a sua versão 1.8.3. Se houver versões mais recentes quando o leitor estiver lendo esse artigo, é possível que funcione também, assim como funciona com versões mais antigas. Além disso, utilizaremos o CDN (**ver BOX 1**) do Google para agilizar o processo de importação e uso da jQuery.

**CDN**:

Significa Content Delivery Network ou Rede de Distribuição de Conteúdo. É um sistema distribuído entre múltiplos servidores para fornecer aos utilizadores acesso rápido e confiável a determinado conteúdo. Carregando a jQuery pelo CDN da Google torna, em vários casos, desnecessário que o browser do cliente faça o download do script, já que ele pode ter acessado algum outro site que o utiliza também e armazenado em cache.

Veja na **Listagem 6** como importar a jQuery no nosso projeto, especificamente na tag do arquivo HTML.

```
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"
></script>
```

**Listagem 6**. Importando a jQuery na página

Com a jQuery pronta, é hora de baixar os arquivos da biblioteca jPlayer. Efetue o download dos arquivos citados através do link disponibilizado na seção **Links** e coloque-os no diretório “js/plugins/jplayer”. O primeiro arquivo baixado corresponde à “biblioteca jPlayer”. O segundo, o “swf”, é o responsável por reproduzir os arquivos de áudio quando o browser não oferecer o suporte à [API de áudio do HTML5](https://www.devmedia.com.br/html5-as-tags-audio-e-video/26018).

Adicione também a chamada ao import do arquivo JavaScript da biblioteca jPlayer, tal como na **Listagem 7**.

```
<script type="text/JavaScript" src="js/plugins/jplayer/jquery
.jplayer.min.js"></script>
```

**Listagem 7**. Importando o arquivo JavaScript do jPlayer

Para que o player funcione, todavia, é necessário que se faça uso de um script JavaScript personalizado, utilizando as referências às funções disponibilizadas pela biblioteca jPlayer. Para tal, crie um arquivo JavaScript chamado “default.js” no diretório “js” da estrutura de pastas e acrescente o código da **Listagem 8** ao mesmo. Adicione também a chamada na página index.html, tal como na **Listagem 9**.

```
$(function() {
   // Definir playlist
   var playlist = [{
       artist: 'Daft Punk',
       title: 'Technologic',
       mp3: 'songs/technologic.mp3'
   }, {
       artist: 'Daft Punk',
       title: 'Human After All',
       mp3: 'songs/human-after-all.mp3'
   }];
});
```

**Listagem 8**. Script personalizado com configurações da playlist

```
<script type="text/JavaScript" src="js/default.js"></script>
```

**Listagem 9**. Importando arquivo default.js à página index.html

A Playlist nada mais é do que um vetor de objetos que representam as músicas. Cada objeto deve representar um arquivo de áudio que deverá ser reproduzido. No código da **Listagem 8** podemos perceber a criação de objetos JavaScript representando cada uma das músicas a serem exibidas, com seus atributos (artist, title, etc) no formato “chave-valor”. A informação mais importante é a que está na chave “mp3”, que representa a url do caminho onde o arquivo de som no formato MP3. O jPlayer consegue lidar com vários tipos de arquivos de som e vídeo, como mp3, m4a, m4v e oga. Se você pretende utilizar o player dentro de um CMS (**ver BOX 2**), por exemplo, é bem mais provável que seus clientes tenham os arquivos em mp3 do que em outros formatos, por essa e muitas outras razões este foi o formato escolhido. A documentação do plugin fornece mais detalhes sobre como utilizar vários formatos.

Repare que na chave mp3, colocamos os nomes dos arquivos adicionados à pasta “songs” no início do artigo. Se seus arquivos de música são diferentes (e certamente serão), então modifique os valores das chaves para contemplar os mesmos. As demais informações definidas nos nossos objetos de música são completamente opcionais, mas é interessante mantê-las, pois é daí que extrairemos a informação que será exibida ao usuário na interface da página. Você pode adicionar, remover ou alterar estas outras chaves como quiser, tudo depende do que você quer exibir para o usuário.

**CMS**:

Significa Content Management System ou Sistema de Gerenciamento de Conteúdo. É um sistema que permite a adição e edição de informações numa interface centralizada. O Wordpress é um exemplo que, após a instalação, permite que os usuários alterem o conteúdo à vontade, mesmo sem entender de programação.

Agora criaremos duas variáveis que irão nos ajudar a controlar a reprodução da playlist. A primeira é a currentTrack, dê a ela o valor **0**. Ela irá controlar qual é a entrada na playlist que está em execução no momento. O zero foi definido como valor padrão, que irá representar a primeira música no nosso array “playlist”. Se você quiser que a reprodução comece pela segunda, terceira ou outra posição qualquer, basta alterar este número, embora seja recomendado que você organize sua playlist exatamente como pretende que as músicas sejam reproduzidas, para facilitar o entendimento do código posteriormente. A segunda variável será criada com o objetivo de obter, de forma prática e rápida, o número de faixas presentes na playlist. A **10** exemplifica como fazer isso. Note que a inclusão destes códigos deve ser feita logo abaixo da criação do array “playlist” da **Listagem 9**.

```
var currentTrack = 0;
var numTracks = playlist.length;
```

**Listagem 10**. Variáveis auxiliares para controlar faixa atual e número de faixas

Logo abaixo, inclua o código referente à **Listagem 11**, que será responsável por criar o player, propriamente dito.

```
var player = $(".player").jPlayer({
   ready: function () {
       // configura a faixa inicial do jPlayer
       player.jPlayer("setMedia", playlist[currentTrack])

       // reproduzir a faixa atual. Se não quiser que o player comece a tocar
       automaticamente
             // retirar esta linha
         player.playCurrent();
     },
     ended: function() {
         // quando terminar de tocar uma música, ir para a próxima
         $(this).playNext();
     },
     play: function(){
         // quando começar a tocar, escrever o nome da faixa sendo executada
         $('.player-current-track').text(playlist[currentTrack].artist+'
         - '+playlist[currentTrack].title);
     },
     swfPath: 'js/plugins/jplayer/',
     supplied: "mp3",
     cssSelectorAncestor: "",
     cssSelector: {
         play: '.player-play',
         pause: ".player-pause",
         stop: ".player-stop",
         seekBar: ".player-timeline",
         playBar: ".player-timeline-control"
     },
     size: {
         width: "1px",
         height: "1px"
     }
 });
```

**Listagem 11**. Código de criação do player

Resumindo, foi criada uma variável (player) para abrigar o nosso player e utilizamos a função jPlayer() na div que criamos para receber os elementos responsáveis pela execução do arquivo de áudio. O jPlayer cria outros elementos dentro da mesma que possibilitam a reprodução do som, mas não precisamos nos preocupar com eles no momento. O parâmetro que passamos para a função jPlayer() é um objeto com a configuração necessária para o funcionamento do player. Vamos analisar cada uma dessas opções:

- ready: Evento disparado quando o player é construído e está pronto para receber instruções. Neste caso, queremos o player com “autoplay”, então neste momento definimos a faixa atual e chamamos o método do nosso player responsável pela reprodução da faixa corrente. Este método é o “playCurrent()”. Ele ainda não foi definido, mas chegaremos nele logo mais. Se não quiser que a faixa comece a ser reproduzida automaticamente, basta remover a chamada ao método playCurrent().

- ended: Este evento é disparado sempre que a reprodução de alguma faixa chega ao fim. Utilizamos para que a próxima faixa da playlist seja definida e a reprodução se inicie. Para isso, chamamos o método “playNext()”, que irá identificar a próxima faixa e executá-la.

- play: Este evento é disparado no início da reprodução de um arquivo de áudio. Este é o momento ideal para atualizarmos o elemento na nossa página, que irá exibir o nome do artista e o título da faixa. O que fazemos aqui é simplesmente buscar esta informação da nossa playlist e escrever no elemento “.player-current-track”, que definimos na nossa marcação. Nesse caso, como já falado, apenas o nome do artista e o título da faixa serão exibidos, mas você pode adicionar qualquer outra informação.

- swfPath: O jPlayer utiliza o elemento do HTML5 para reproduzir as músicas. Porém, em browsers que não tem suporte, ele utiliza um pequeno player em Flash. Ao executar o download do jPlayer, junto dele nota-se a existência de um arquivo “jplayer.swf”. Você precisa salvá-lo em algum lugar dentro do seu projeto e colocar o endereço do diretório nessa propriedade. No nosso caso, colocamos o swf na mesma pasta da biblioteca (/js/plugins/jplayer), então colocamos o caminho da pasta do jPlayer relativo ao documento no qual estamos inserindo o mesmo.

- supplied: A propriedade “supplied” especifica os tipos de arquivos que iremos utilizar. Como os arquivos definidos serão apenas mp3, então o conteúdo da mesma propriedade será uma string contendo ‘mp3’. você pode especificar mais de um tipo. Por exemplo, se tiver arquivos mp3 e m4a, pode usar o valor ‘mp3,m4a’.

- cssSelectorAncestor: Esta propriedade define o elemento base onde os controles serão colocados quando o player for criado. Como estamos utilizando uma marcação completamente personalizada e flexível, iremos definir uma string vazia para termos controle sobre os elementos, assim o jPlayer não irá criar nada na nossa marcação.

- cssSelector

  : A propriedade “

  cssSelector

  ” permite que especifiquemos o que cada controle pode fazer. Precisaremos definir um objeto onde as chaves representam a ação e os valores representam o seletor do elemento responsável. As seguintes chaves serão utilizadas:

  - play: passando o elemento .player-play, que é o botão play;
  - pause: passando o elemento .player-pause, que é o botão pause;
  - stop: passando o elemento .player-stop, que é o botão stop;
  - seekBar: passando o elemento .player-timeline, que representa a barra de progresso. Esta é a que mostra o tempo total do som;
  - playBar: passando o elemento .player-timeline-control, que mostra o progresso da execução. O usuário poderá ir para momentos específicos da faixa clicando sobre este controle;

- size: A propriedade “size” define o tamanho do player criado pelo jPlayer. Dentro deste elemento, o jPlayer irá criar o elemento ou incluir o Jplayer.swf.

Nas explanações anteriores sobre cada um dos atributos do player, você pode notar a referência a três métodos para controle da navegação entre as músicas. O primeiro deles é o “playCurrent()”. Este método será responsável por solicitar ao jPlayer a reprodução da música atual. Para implementá-lo, vamos utilizar o método jPlayer() duas vezes. Na primeira, serão passados dois parâmetros: a string “setMedia” para dizer ao jPlayer qual arquivo será trabalhado a partir de então, e o segundo, o objeto que representa o arquivo (neste caso o item “currentTrack” dentro da playlist). Na segunda chamada ao método jPlayer(), apenas o parâmetro “play” será passado por parâmetro, este que informa ao jPlayer que ele já pode reproduzir o arquivo que está “setado”.

**Nota**: Todos os métodos de navegação serão criados adicionando-se uma nova function às propriedades playX do objeto player.

O segundo método é o “playNext()” que, por sua vez, irá identificar qual é a próxima faixa, defini-la como faixa atual e utilizar o método que criamos no passo anterior (playCurrent) para executá-la. A variável numTracks, criada na **Listagem 10**, vai auxiliar a reiniciar a execução da playlist quando ela chegar ao fim. Além disso, é importante ater-se ao estado atual de execução, considerando que se a música atual for a última da playlist, então iremos executar a primeira, senão executaremos a próxima.

Finalmente, o terceiro método, o “playPrevious()”, será responsável por voltar a execução para a faixa anterior. Se a faixa atual for a primeira da nossa playlist, então ele irá executar a última.

A **Listagem 12** exemplifica a aplicação desses três métodos. Adicione-a ao final da **Listagem 11**.

```
player.playCurrent = function() {
  player.jPlayer("setMedia", playlist[currentTrack]).jPlayer("play");
}

player.playNext = function() {
 currentTrack = (currentTrack == (numTracks -1)) ? 0 : ++currentTrack;
 player.playCurrent();
};

player.playPrevious = function() {
   currentTrack = (currentTrack == 0) ? numTracks - 1 : --currentTrack;
   player.playCurrent();
};
```

**Listagem 12**. Implementação dos métodos playCurrent(), playNext() e playPrevious()

Por fim iremos tratar os cliques nos botões de “próxima faixa” e “anterior”. Para isso, será necessário ouvir o evento “click” nesses elementos e chamar a função apropriada à ação desejada pelo usuário, utilizando as funções definidas anteriormente para a navegação. Veja no código da **Listagem 13** como fazer isso.

```
$('.player-next').click(function() {
   player.playNext();
});

$('.player-prev').click(function() {
  player.playPrevious();
});
```

**Listagem 13**. Ouvintes de cliques nos botões de próxima e anterior

Agora é testar no seu navegador. Se tudo estiver correto, você irá ouvir sua música sendo reproduzida e poderá avançar e voltar na sua playlist. O resultado pode ser visualizado na **Figura 3**. Caso a música não esteja sendo reproduzida, verifique se seguiu todos os passos corretamente. Verifique também o console do seu navegador. Ele é muito útil para identificar problemas no código em execução e o jPlayer costuma colocar várias informações lá quando encontra algum erro.

Depois que o desenvolvedor se acostuma com a biblioteca, fazer alterações no player se tornam bem simples. Por exemplo, se quiser adicionar o nome do álbum ao playlist, modifique o array playlist para que ele fique tal como na **Listagem 14**.

```
var playlist = [{
         artist: 'Daft Punk',
         title: 'Technologic',
   album: 'Human After All',
   mp3: 'songs/technologic.mp3'
}, {
    artist: 'Daft Punk',
         title: 'Human After All',
         album: 'Human After All',
   mp3: 'songs/human-after-all.mp3'
}];
```

**Listagem 14**. Playlist com inclusão do nome do álbum

Agora nossa playlist contém o título do álbum de cada faixa. E para que o player funcione, é preciso modificar o que fazemos no evento play.

Localize a **linha 15** da **Listagem 11** e substitua-a pelo código da **Listagem 15**.

```
$('.player-current-track').text(playlist[currentTrack].artist+' - '
+playlist[currentTrack].title+' - '+playlist[currentTrack].album);
```

**Listagem 15**. Código de alteração para exibição do nome do álbum

Pronto! Agora o player irá mostrar também o nome do álbum.

A mesma coisa pode ser feita se você quiser colocar a capa do álbum. Basta colocar a url da capa do álbum na playlist e a imagem no lugar em que você queira que apareça. Pode criar dinamicamente um novo elemento img ou pode reutilizar um criado especificamente pra isso. Tudo depende de como você queira montar o seu player.

### Criando uma playlist

Com posse de todos estes conhecimentos você já será capaz de ­manipular diversos recursos interessantes do plugin jPlayer.

Uma reclamação muito comum entre desenvolvedores das mais diversas linguagens está relacionada à quantidade de código necessário para se desenvolver determinadas soluções, muitas delas simplistas e comuns. A melhor forma de mensurar isso é experiência. Quanto mais experiência você tiver em determinada tecnologia, mais produtivo será com relação ao tempo que leva pra fazer as coisas simplistas e/ou mais complexas. Por exemplo, considere o cenário de que não ficou satisfeito apenas com a criação de um player básico. Suponha que você necessita de algo um pouco mais arrojado, uma funcionalidade onde você possa criar uma lista de reprodução e disponibilizar para o usuário a visão de que ele pode escolher qualquer música dentre as opções disponíveis, suponha que você queira criar uma playlist.

As características de uma playlist não mudam muito do player que criamos até então, uma vez que a diferença mais significativa é a exibição da lista de músicas junto aos botões de execução, tal como pode ser visto em players como o Windows Media Player para Windows.

**Nota**: É preciso saber a distinção entre player e playlist. Um player é a ferramenta que executa as músicas. A playlist é apenas uma lista de execução.

O JPlayerPlaylist é um add-on (extensão) para o plugin jPlayer. Ele foi feito com o objetivo de complementar o plugin do jPlayer no que concerne ao desenvolvimento especificamente de playlists. Trabalhar com ele é tão simples quanto usar o jPlayer, os comandos são semelhantes, a forma de implementar a estrutura de chamadas também, entretanto ele exigirá que você tenha uma estrutura HTML montada de acordo com as definições dos arquivos JavaScript e CSS do mesmo.

O primeiro passo é efetuar o download do plugin, um arquivo de extensão .js. Você poderá encontrar o link para download na seção **Links** no final do artigo. Coloque o arquivo baixado na pasta "js" do projeto que estamos desenvolvendo.

Após isso, [crie um novo arquivo HTML](https://www.devmedia.com.br/curso/curso-de-html-basico/371) na raiz do projeto e nomeie-o como "playlist.html". O arquivo conterá o conteúdo de uma nova página HTML preparada para executar um player mais completo. Com lista de músicas, links para cada uma, botões de próximo, anterior, pausa e play, e até opções de aumentar e diminuir o volume da música tocada.

Veja na **Listagem 16** o conteúdo da página.

```
<!doctype html>
<html lang="pt-br">
<head>
   <meta http-equiv="Content-Type" content="text/html;
   charset=ISO-8859-1">
   <title>JPlayer Playlist - Web Magazine Devmedia<
   /title>
   <link href="css/jplayer.blue.monday.css" rel="stylesheet"
   type="text/css">
   <script src="http://ajax.googleapis.com/ajax/libs/jquery/
   1.8.3/jquery.min.js"></script>
   <script type="text/JavaScript" src="http://demo.chapmanit.
   com/jplayerPlaylist/js/jquery.jplayer.min.js"></script>
   <script type="text/JavaScript">
   <!--
   $(document).ready(function(){
         // Variável responsável por guardar o item atual de execução
         var playItem = 0;

         /*
            Lista com todas as músicas a serem executadas na playlist.
            Em uma aplicação dinâmica, os valores provavelmente serão
            montados a partir de uma linguagem server side.
         */
         var minhaPlayList = [
            {name:"Daft Punk - Human After All", mp3:
            "songs/human-after-all.mp3"},
            {name:"Amy Winehouse - You Know I'm No Good", mp3:
            "songs/you-know-im-no-good.mp3"},
            {name:"Black Eyed Peas - Shut Up", mp3:"songs/shut-up.mp3"},
            {name:"Nightwish - Ghost River", mp3:"songs/ghost-river.mp3"},
            {name:"Daft Punk - Technologic", mp3:"songs/technologic.mp3"}
         ];

         /* Cópias locais para os seletores jQuery,
         apenas para performance */
         // Guarda o tempo atual de execução
         var jpTempoExecucao = $("#jplayer_tempo_execucao");
         // Guarda o tempo total de execução
         var jpTempoTotal = $("#jplayer_tempo_total");

         // Função de criação e configuração do player.
         $("#jquery_jplayer").jPlayer({
            ready: function() {
               exibirPlayList();
               playListInit(true); // Parâmetro é um para autoplay.
            },
            oggSupport: false
         })
          // Configurações gerais do player
         .jPlayer("onProgressChange", function(loadPercent,
         playedPercentRelative, playedPercentAbsolute, playedTime,
         totalTime) {
            jpTempoExecucao.text($.jPlayer.convertTime(playedTime));
            jpTempoTotal.text($.jPlayer.convertTime(totalTime));
         })
         .jPlayer("onSoundComplete", function() {
            playListProximo();
         });

         // Captura o evento de clique para o botão de anterior
         $("#jplayer_anterior").click(function() {
            playListAnterior();
            $(this).blur();
            return false;
         });

         // Captura o evento de clique para o botão de próximo
         $("#jplayer_proximo").click(function() {
            playListProximo();
            $(this).blur();
            return false;
         });

         // Método interno de montagem e exibição da playlist
         function exibirPlayList() {
            $("#jplayer_playlist ul").empty();
            for (i=0; i < minhaPlayList.length; i++) {
               var listItem = (i == minhaPlayList.length-1) ?
               "<li class='jplayer_playlist_ultimo_item'>" :
               "<li>";
                 listItem<a href='#' id='jplayer_playlist_item_"
                 +i+"' tabindex='1'>"+ minhaPlayList[i].name</a>
                 (<a id='jplayer_playlist_get_mp3_"+i+"' href='"
                 + minhaPlayList[i].mp3 + "' tabindex='1'
                 >mp3</a>)</li>";
               $("#jplayer_playlist ul").append(listItem);
               $("#jplayer_playlist_item_"+i).data("index", i)
               .click(function() {
                  var index = $(this).data("index");
                  if (playItem != index) {
                        mudarPlayList(index);
                  } else {
                        $("#jquery_jplayer").jPlayer("play");
                  }
                  $(this).blur();
                  return false;
               });
               $("#jplayer_playlist_get_mp3_"+i).data("index", i)
               .click(function() {
                  var index = $(this).data("index");
                  $("#jplayer_playlist_item_"+index)
                  .trigger("click");
                  $(this).blur();
                  return false;
               });
            }
         }

         // Inicializa a playlist
         function playListInit(autoplay) {
            if(autoplay) {
               mudarPlayList(playItem);
            } else {
               playListConfig(playItem);
            }
         }

         // Configura a playlist (quando a mesma não está
         por padrão como autoplay)
        function playListConfig(index) {
           $("#jplayer_playlist_item_"+playItem)
           .removeClass("jplayer_playlist_current").parent()
           .removeClass("jplayer_playlist_current");
           $("#jplayer_playlist_item_"+index)
           .addClass("jplayer_playlist_current").parent()
           .addClass("jplayer_playlist_current");
           playItem = index;
           $("#jquery_jplayer").jPlayer("setFile",
           minhaPlayList[playItem].mp3, minhaPlayList[playItem].ogg);
        }

        function mudarPlayList(index) {
           playListConfig(index);
           $("#jquery_jplayer").jPlayer("play");
        }

        // Executa a próxima faixa
        function playListProximo() {
           var index = (playItem+1 < minhaPlayList.length) ?
           playItem + 1 : 0;
           mudarPlayList(index);
        }

        // Executa a faixa anterior
        function playListAnterior() {
           var index = (playItem-1 >= 0) ? playItem-1 :
           minhaPlayList.length-1;
           mudarPlayList(index);
        }
  });
  -->
  </script>
</head>
<body>
  <!-- Código para forçar a execução da primeira música
   quando a página abre. -->
  <div id="jquery_jplayer" style="position: absolute;
  top: 0px; left: -9999px;">
        <audio id="jqjp_audio_0" preload="none"
        src="songs/human-after-all.mp3"></audio>

        <div id="jqjp_force_0" style="text-indent:
        -9999px;">0.3245763930026442</div>
  </div>

  <div class="jp-playlist-player">
    <div class="jp-interface">
       <ul class="jp-controls">
          <li><a href="#" id="jplayer_play"
          class="jp-play" tabindex="1" title="Executar"
          >play</a></li>
          <li><a href="#" id="jplayer_pause"
          class="jp-pause" tabindex="1" style="display:
          block;" title="Pausar">pause</a></li>
          <li><a href="#" id="jplayer_stop"
          class="jp-stop" tabindex="1" title="Parar"
          >stop</a></li>
          <li><a href="#" id="jplayer_volume_min"
          class="jp-volume-min" tabindex="1" title="Mínimo"
          >min volume</a></li>
          <li><a href="#" id="jplayer_volume_max"
          class="jp-volume-max" tabindex="1" title="Máximo"
          >max volume</a></li>
          <li><a href="#" id="jplayer_anterior"
          class="jp-previous" tabindex="1" title="Anterior"
          >previous</a></li>
          <li><a href="#" id="jplayer_proximo"
          class="jp-next" tabindex="1" title="Próximo"
          >next</a></li>
       </ul>
     <div class="jp-progress">
        <div id="jplayer_load_bar" class="jp-load-bar"
        style="width: 0%;">
           <div id="jplayer_play_bar" class="jp-play-bar"
           style="width: 0%;"></div>
        </div>
     </div>
     <div id="jplayer_volume_bar" class="jp-volume-bar">
        <div id="jplayer_volume_bar_value" class="jp-volume-bar-value"
        style="width: 80%;"></div>
     </div>
     <div id="jplayer_tempo_execucao" class="jp-play-time"
     >00:00</div>
     <div id="jplayer_tempo_total" class="jp-total-time"
     >00:00</div>
    </div>
    <div id="jplayer_playlist" class="jp-playlist">
       <ul>
          <li class="jplayer_playlist_current">
             <a href="#" id="jplayer_playlist_item_0"
             tabindex="1" class="jplayer_playlist_current">
             Daft Punk - Human After All</a>
          </li>
          <li>
             <a href="#" id="jplayer_playlist_item_1"
             tabindex="1">Amy Winehouse - You Know I'm
             No Good</a>
          </li>
          <li>
             <a href="#" id="jplayer_playlist_item_2"
             tabindex="1">Black Eyed Peas - Shut Up</a>
          </li>
          <li>
             <a href="#" id="jplayer_playlist_item_3"
             tabindex="1">Nightwish - Ghost River</a>
          </li>
          <li class="jplayer_playlist_ultimo_item">
             <a href="#" id="jplayer_playlist_item_5"
             tabindex="1">Daft Punk - Techonologic</a>
          </li>
       </ul>
    </div>
  </div>
</body>
</html>
```

**Listagem 16**. Página HTML da playlist

Note que o código está comentado, o suficiente para que você possa embasar o que cada parte faz e as responsabilidades de cada uma.

Note também que adicionamos mais músicas à lista disponível. Se for utilizar suas próprias músicas, lembre-se de mudar corretamente os nomes dos arquivos no JavaScript do início da página, assim como as descrições nos links ao final do artigo.

Após isso, você deve adicionar os arquivos de estilo (CSS) e a imagem nas pastas correspondentes. Os mesmos arquivos podem ser encontrados no link de download deste mesmo artigo. Certifique-se de criar também uma pasta “img” dentro da raiz do projeto para guardar todas as imagens usadas.

Se tudo tiver sido feito corretamente, execute a página HTML e você verá como resultado o player exibido na **Figura 4**.

![Resultado da criação da playlist com a extensão jPlayerPlaylist](https://arquivo.devmedia.com.br/revistas/front_end/imagens/5/image005.jpg)**Figura 4**. Resultado da criação da playlist com a extensão jPlayerPlaylist

### Mais sobre o jPlayer

#### Formatos de áudio

Os formatos de mídia que são essenciais para o JPlayer são aqueles que são suportados por ambas soluções Flash e os navegadores HTML5 que não suportam Flash, tais como iOS. É importante que um desses formatos seja fornecido para JPlayer para que os navegadores populares sejam capazes de reproduzir as mídias. Depois de um dos formatos essenciais ter sido fornecido, formatos de contrapartida adicionais podem ser fornecidos para aumentar o apoio cross-browser da solução HTML5. A opção jPlayer ({"supplied": "formats"}) oferece mais detalhes de como esse processo funciona. Em suma, pelo menos um dos formatos de áudio e vídeo deve ser fornecido pelo browser que está a executar o player, são eles: MP3 ou M4A para áudio e MP4 para vídeo.

#### Regras de segurança Flash

As regras de segurança para o arquivo SWF do JPlayer foram melhoradas usando o código da **Listagem 17** que pode ser chamado a partir de qualquer domínio.

```
flash.system.Security.allowDomain ( " * " ) ;
flash.system.Security.allowInsecureDomain ( " * " ) ;
```

**Listagem 17**. Código de segurança Flash

Geralmente, você irá fazer o upload do arquivo SWF com o arquivo JavaScript para um diretório chamado "js " no seu domínio . Use a opção construtor jPlayer({" swfPath " : caminho }) para alterar o caminho.

Tentar executar o JPlayer localmente em seu computador irá gerar violações de segurança em Flash e você precisa permitir o acesso de arquivos locais usando o Gerenciador de configurações do Flash. Consulte a Ajuda do Flash Player para obter mais informações.

Para desenvolver localmente, instale um servidor no seu sistema, como o Apache, para permitir um host local no seu computador.

#### Tipos MIME

Quando a sua aplicação lida com a publicação final, ou seja, a publicação em um servidor você deve ter sempre em mente que o ambiente de publicação final é, em muitos casos, diferente do ambiente de desenvolvimento. Em vista disso, é necessário que o seu servidor tenha todas as configurações corretamente feitas para evitar conflitos entre os tipos manipulados.

MIME (Multipurpose Internet Mail Extensions) é um padrão de internet que é utilizado para descrever o conteúdo de vários arquivos. Enquanto o nome MIME quer dizer "Mail", ele também é usado para páginas da web.

O tipo MIME para HTML é “text/html”, para arquivos Excel é “application/vnd.ms-excel” e etc.

Tipos MIME são definidos no HTML pelo atributo “type” em links, objetos e tags de script e estilo.

O servidor do seu domínio deve dar o tipo MIME correto para todas as URLs de mídia.

A falta o tipo MIME correto vai fazer com que a mídia não funcione corretamente em alguns navegadores HTML5. Esta é uma causa comum de problemas que afetam somente o Firefox e o Opera. Outros navegadores são menos rigorosos, mas o tipo MIME sempre deve ser verificado se está correto, dado se você estiver tendo problemas para ter a mídia executando em qualquer navegador.

Veja na **Listagem 18** alguns exemplos comuns para o jPlayer.

```
MP3: audio/mpeg
MP4: audio/mp4 video/mp4
OGG: audio/ogg video/ogg
WebM: audio/webm video/webm
WAV: audio/wav
```

**Listagem 18**. Exemplos de Tipos MIME comuns para o plugin jPlayer

Se você usar uma extensão comum para mídias de áudio e vídeo, como audio.mp4 e video.mp4 por exemplo, então simplesmente use a versão em vídeo do tipo MIME para ambos, isto é, “video/mp4”.

Em servidores Apache, você pode usar o arquivo de extensão “.htaccess” para definir o tipo MIME com base na extensão do arquivo (**Listagem 19**).

```
#AddType TIPO/EXTENSÃO DO SUBTIPO
AddType audio/mpeg mp3
AddType audio/mp4 m4a
AddType audio/ogg ogg
AddType audio/ogg oga
AddType audio/webm webma
AddType audio/wav wav

AddType video/mp4 mp4
AddType video/mp4 m4v
AddType video/ogg ogv
AddType video/webm webm
AddType video/webm webm
```

**Listagem 19**. Tipos MIME para configuração do Apache Server

**Não use GZIP nas Mídias**

Desative a codificação GZIP (ver **BOX 3**) de todos os arquivos de mídia. Os arquivos de mídia já estão compactados e o GZIP só vai perder CPU em seu servidor. O plugin do Adobe Flash vai ter problemas se você usar GZIP nas mídias. Não GZIP o arquivo Jplayer.swf também. Sinta-se livre para GZIP o JavaScript.

**GZI**: GZIP é um software criado com a finalidade de comprimir dados sem perdê-los. Baseado no algoritmo DEFLATE, ele gera um arquivo comprimido de extensão “.gz”. O nome se origina da abreviação dos nomes GNU zip e é comumente usado em sistemas UNIX.

#### Requisições Byte-Range

Seu servidor deve habilitar solicitações de “extensão”. Isso é fácil de verificar vendo se a resposta do seu servidor inclui os “Accept-Ranges” em seu cabeçalho. A maioria dos navegadores HTML5 permitirá a busca das novas posições dos arquivos durante um download, por isso, o servidor deve permitir que o novo Range a seja solicitado.

A não aceitação dos pedidos de intervalo de bytes vai causar problemas em alguns navegadores HTML5. Muitas vezes a duração não pode ser lida a partir do arquivo, tal como alguns formatos requerem que o início e o fim do arquivo sejam lidos para saber a sua duração. O Chrome tende a ser o navegador que tem a maioria dos problemas se a requisição de Range não estiver habilitada no servidor, mas todos os navegadores terão algum problema. Mesmo que seja só isso, você tem que esperar por todas as mídias antes de ir até o fim com as indagações.

Este problema é conhecido por afetar os servidores Jetty 6 com a sua configuração padrão. Uma função PHP foi escrita pela comunidade jPlayer que pode servir arquivos de mídia com suporte a solicitações de extensões.

#### Protegendo suas mídias

Tenha cuidado ao tentar restringir o acesso aos seus arquivos de mídia. A URL da mídia deve ser acessível através da internet pelo usuário e sua resposta deve estar no formato esperado.

Usar a resposta do servidor para desativar o cache local de mídia pode causar problemas com alguns navegadores HTML5. Isso pode fazer com que a duração das mídias seja desconhecida, o que irá mostrar um “NaN” (Not a Number) quando solicitar o tempo de duração do jPlayer.

Há inúmeras formas de se colocar áudio em páginas na web. Aqui exploramos uma forma simples e flexível, que possui um mecanismo com detalhes visuais personalizáveis e lista de arquivos para reprodução.

Os exemplos no início do artigo mostram como a biblioteca jPlayer pode ser utilizada de várias formas, desde tocar trechos de músicas em lojas online, quanto em aplicações web das mais diversas finalidades.

**Links**:

- [Documentação oficial do jPlayer](http://www.jplayer.org/latest/developer-guide/).
- [Site da jQuery](http://jquery.com/).
- [Site do jPlayer](http://www.jplayer.org/).
- [Página do jPlayerPlaylist](http://www.jplayer.org/latest/demo-02-jPlayerPlaylist/).

Tecnologias:

- [CSS](https://www.devmedia.com.br/css/)
-  

- [HTML](https://www.devmedia.com.br/html/)
-  

- [JavaScript](https://www.devmedia.com.br/javascript/)
# Como capturar áudio em javascript?

Atualmente, estou usando `getUserMedia()`, que está funcionando apenas no Firefox e Chrome, mas foi preterido e funciona apenas em https (no Chrome). Existe alguma outra/melhor maneira de obter a entrada de fala em javascript que funcione em todas as plataformas?

Por exemplo. como sites como o aplicativo web.whatsapp.com gravam áudio? `getUserMedia()` solicita que os usuários iniciantes permitam a gravação de áudio, enquanto o aplicativo Whatsapp não requer a permissão do usuário.

A `getUserMedia()` que estou usando atualmente se parece com isso:

```javascript
navigator.getUserMedia(
    {
        "audio": {
            "mandatory": {
                "googEchoCancellation": "false",
                "googAutoGainControl": "false",
                "googNoiseSuppression": "false",
                "googHighpassFilter": "false"
            },
            "optional": []
        },
    }, gotStream, function(e) {
        console.log(e);
    });
```

**[javascript](https://www.ti-enxame.com/pt/javascript/)****[audio](https://www.ti-enxame.com/pt/audio/)****[speech](https://www.ti-enxame.com/pt/speech/)****[getusermedia](https://www.ti-enxame.com/pt/getusermedia/)****[voice-recording](https://www.ti-enxame.com/pt/voice-recording/)**

 20

15 de jan. de 2016[user2212461](https://stackoverflow.com/users/2212461/user2212461)







O Chrome 60 ou superior [requer o uso de **https** ](https://addpipe.com/blog/microphone-camera-access-no-longer-works-insecure-origins/), pois `getUserMedia` é um poderoso [recurso](https://sites.google.com/a/chromium.org/dev/Home/chromium-security/deprecating-powerful-features-on-insecure-origins) =. O acesso à API não deve funcionar em domínios não seguros, pois esse acesso à API pode se espalhar para atores não seguros. O Firefox ainda suporta `getUserMedia` over **http** .

Eu tenho usado [RecorderJS](https://github.com/mattdiamond/Recorderjs) e isso serviu bem aos meus propósitos. Aqui está um exemplo de código. ( [origem](https://stackoverflow.com/a/30910347/1967704) )

```javascript
function RecordAudio(stream, cfg) {

  var config = cfg || {};
  var bufferLen = config.bufferLen || 4096;
  var numChannels = config.numChannels || 2;
  this.context = stream.context;
  var recordBuffers = [];
  var recording = false;
  this.node = (this.context.createScriptProcessor ||
    this.context.createJavaScriptNode).call(this.context,
    bufferLen, numChannels, numChannels);

  stream.connect(this.node);
  this.node.connect(this.context.destination);

  this.node.onaudioprocess = function(e) {
    if (!recording) return;
    for (var i = 0; i < numChannels; i++) {
      if (!recordBuffers[i]) recordBuffers[i] = [];
      recordBuffers[i].Push.apply(recordBuffers[i], e.inputBuffer.getChannelData(i));
    }
  }

  this.getData = function() {
    var tmp = recordBuffers;
    recordBuffers = [];
    return tmp; // returns an array of array containing data from various channels
  };

  this.start() = function() {
    recording = true;
  };

  this.stop() = function() {
    recording = false;
  };
}
```

O uso é direto:

```javascript
var recorder = new RecordAudio(userMedia);
recorder.start();
recorder.stop();
var recordedData = recorder.getData()
```

Edit: Você também pode querer verificar isso [resposta](https://stackoverflow.com/a/22420137/1967704) se nada funcionar.

 28

21 de jan. de 2016[George Netu](https://stackoverflow.com/users/1967704/george-netu)



O Recorder JS faz o trabalho mais fácil para você. Funciona com nós da API de áudio da Web

Os navegadores Chrome e Firefox evoluíram agora. Existe uma API embutida `MediaRecoder` que grava áudio para você.

```javascript
navigator.mediaDevices.getUserMedia({audio:true})
    .then(stream => {
        rec = new MediaRecorder(stream);
        rec.ondataavailable = e => {
            audioChunks.Push(e.data);
            if (rec.state == "inactive"){
               // Use blob to create a new Object URL and playback/download
            }
        }
    })
    .catch(e=>console.log(e));
```

Trabalhando [demo](https://jsfiddle.net/sasivarunan/bv55z5fe/)

`MediaRecoder` o suporte começa em

Suporte do Chrome: 47

Suporte do Firefox: 25.0

 17

20 de fev. de 2017[Sasi Varunan](https://stackoverflow.com/users/4146454/sasi-varunan)

A `getUserMedia()` não está obsoleta, está obsoleta usando-a sobre `http`. Até onde eu sei o único navegador que requer `https` para `getUserMedia()` no momento é Chrome, o que eu acho que é a abordagem correta.

Se você quiser `ssl/tls` para o seu teste, você pode usar a versão gratuita do CloudFlare.

A página do Whatsapp não fornece nenhuma função de gravação, apenas permite iniciar o aplicativo.
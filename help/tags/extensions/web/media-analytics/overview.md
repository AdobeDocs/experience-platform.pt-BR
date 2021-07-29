---
title: Visão geral da extensão do Adobe Media Analytics para áudio e vídeo
description: Saiba mais sobre a extensão da tag Adobe Medium Analytics for Audio and Video no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 91%

---

# Visão geral da extensão do Adobe Media Analytics para áudio e vídeo

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Use esta documentação para obter informações sobre como instalar, configurar e implementar a extensão Adobe Media Analytics for Audio and Video (extensão do Media Analytics). Estão incluídas as opções disponíveis ao usar esta extensão para criar uma regra, juntamente com exemplos e links para amostras.

A extensão do Media Analytics (MA) adiciona a principal SDK de mídia JavaScript (Media 2.x SDK). Essa extensão fornece a funcionalidade necessária para adicionar a instância do rastreador `MediaHeartbeat` a um site ou projeto de tag. A extensão do MA exige duas extensões adicionais:

* [Extensão do Analytics](../analytics/overview.md)
* [Extensão do Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>O rastreamento de áudio requer a extensão do Analytics versão 1.6 ou superior.

Depois de incluir todas as três extensões mencionadas acima em seu projeto de tags, você pode prosseguir de uma das duas formas a seguir:

* Use APIs `MediaHeartbeat` do aplicativo web
* Com a inclusão ou criação de uma extensão específica para um reprodutor que mapeie eventos específicos daquele reprodutor de mídia para as APIs na instância do rastreador do `MediaHeartbeat`. Essa instância é exposta por meio da extensão do MA.

## Instalação e configuração da extensão do MA

* **Instalar -** para instalar a extensão do MA, abra a propriedade da extensão e selecione **[!UICONTROL Extensões > Catálogo]**, passe o mouse sobre a extensão **[!UICONTROL Adobe Media Analytics para áudio e vídeo]** e selecione **[!UICONTROL Instalar]**.

* **Configurar -** para configurar a extensão do MA, abra a guia [!UICONTROL Extensões], passe o mouse sobre a extensão e selecione **[!UICONTROL Configurar]**:

![Configuração de extensão do MA](../../../images/ext-va-config.jpg)

### Opções de configuração:

| Opção | Descrição |
| :--- | :--- |
| Servidor de rastreamento | Define o servidor usado para rastrear “pulsações de mídia” (esse não é o mesmo servidor que o seu servidor de rastreamento de análises) |
| Application Version | A versão do aplicativo do reprodutor de vídeo/SDK |
| Nome do reprodutor | Nome do reprodutor de vídeo em uso (por exemplo, &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Canal | Propriedade do nome do canal |
| Online Video Provider | Nome da plataforma de vídeo online pela qual o conteúdo é distribuído |
| Debug Logging | Ativar ou desativar registro |
| Enable SSL | Ativar ou desativar o envio de pings em HTTPS |
| Export APIs to Window Object | Ativar ou desativar a exportação de APIs do Media Analytics para o escopo global |
| Variable Name | Uma variável usada para exportar as APIs do Media Analytics sob o objeto `window` |

**Lembrete**: a extensão do MA exige as extensões do [Analytics](../analytics/overview.md) e da [Experience Cloud ID](../id-service/overview.md). Você também deve adicionar essas extensões à propriedade da sua extensão e configurá-las.

## Uso da extensão do MA

### Uso de uma página web/aplicativo JS

A extensão do MA exporta as APIs do MediaHeartbeat no objeto da janela global ao ativar a configuração &quot;Exportar APIs para objeto da janela&quot; na página [!UICONTROL Configuração]. Exporta as APIs sob o nome da variável configurada. Por exemplo, se o nome da variável estiver configurado para ser `ADB`, o MediaHeartbeat pode ser acessado em `window.ADB.MediaHeartbeat`.

>[!IMPORTANT]
>
>A extensão do MA exporta as APIs apenas quando `window["CONFIGURED_VARIABLE_NAME"]` está indefinido e não substitui as variáveis existentes.

1. **Criar instância do MediaHeartbeat:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance`

   **Params:** um objeto delegado válido que expõe essas funções.

   | Método |  Descrição   |
   | :--- | :--- |
   | `getQoSObject()` | Retorna a instância `theMediaObject` que contém as informações de QoS atuais. Esse método será chamado várias vezes durante uma sessão de reprodução. A implementação do player sempre deve retornar os dados de QoS mais recentes. |
   | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. Para rastreamento VOD, o valor é especificado em segundos a partir do início do item de mídia. Para rastreamento LIVE/LIVE, o valor é especificado em segundos a partir do início do programa. |

   **Valor de retorno:** uma promessa que resolve uma instância do `MediaHeartbeat` ou a rejeita com uma mensagem de erro.

1. **Acessar constantes do MediaHeartbeat:** `window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat`

   Isso expõe todas as constantes e métodos estáticos da classe [`MediaHeartbeat`](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

   Você pode obter o player de amostra aqui: [reprodutor MA de amostra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/2.x). O reprodutor usado de exemplo atua como uma referência para mostrar como usar a extensão do MA para suportar o Media Analytics diretamente de um aplicativo web.

1. Crie a instância do rastreador de MediaHeartbeat da seguinte maneira:

   ```javascript
   var MediaHeartbeat = window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat;
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   };
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   };
   
   var self = this;
   MediaHeartbeat.getInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   ```

### Com o uso a partir de outras extensões

A extensão do MA expõe os módulos `get-instance` e os módulos compartilhados `media-heartbeat` a outras extensões. (Para obter informações adicionais sobre Módulos compartilhados, consulte a [documentação Módulos compartilhados](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Os módulos compartilhados podem ser acessados somente a partir de outras extensões. Ou seja, uma página web ou aplicativo JS não podem acessar os módulos compartilhados ou usar `turbine` (consulte um exemplo de código abaixo) fora de uma extensão.

1. **Criar instância de MediaHeartbeat:** módulo compartilhado `get-instance`

   **Params:**

   * Um objeto delegado válido que expõe essas funções:

      | Método |  Descrição   |
      | :--- | :--- |
      | `getQoSObject()` | Retorna a instância `MediaObject` que contém as informações de QoS atuais. Esse método será chamado várias vezes durante uma sessão de reprodução. A implementação do reprodutor sempre deve retornar os dados de QoS mais recentes. |
      | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. Para rastreamento VOD, o valor é especificado em segundos a partir do início do item de mídia. Para rastreamento LIVE/LIVE, o valor é especificado em segundos a partir do início do programa. |

   * Um objeto de configuração opcional que expõe essas propriedades:

      | Propriedade | Descrição | Obrigatório |
      | :--- | :--- | :--- |
      | Provedor de Vídeo Online | Nome da plataforma de vídeo online pela qual o conteúdo é distribuído. | Não. Se estiver presente, substituirá o valor definido durante a configuração da extensão. |
      | Nome do reprodutor | Nome do reprodutor de vídeo em uso (por exemplo, &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) | Não. Se estiver presente, substituirá o valor definido durante a configuração da extensão. |
      | Canal | Propriedade do nome do canal | Não. Se estiver presente, substituirá o valor definido durante a configuração da extensão. |
   **Valor de retorno:** uma promessa que resolve uma instância do `MediaHeartbeat` ou a rejeita com uma mensagem de erro.

1. **Constantes de acesso do MediaHeartbeat:** módulo compartilhado `media-heartbeat`

   Esse módulo expõe todas as constantes e métodos estáticos dessa classe: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html).

1. Crie a instância do rastreador de MediaHeartbeat da seguinte maneira:

   ```javascript
   var getMediaHeartbeatInstance =
     turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   
   var MediaHeartbeat =
     turbine.getSharedModule('adobe-video-analytics', 'media-heartbeat');
     ...
   
   var delegate = {
       getCurrentPlaybackTime: this._getCurrentPlaybackTime.bind(this),
       getQoSObject: this._getQoSObject.bind(this),
   }
   
   var config = {
       playerName: "Custom Player",
       ovp: "Custom OVP",
       channel: "Custom Channel"
   }
   ...
   
   var self = this;
   getMediaHeartbeatInstance(delegate, config).then(function(instance) {
       self._mediaHeartbeat = instance;
       ...
       // Do Tracking using the MediaHeartbeat instance.
   }).catch(function(err){
       // Getting MediaHeartbeat instance failed.
   });
   
   ...
   ```

1. Usando a instância Media Heartbeat, siga a [documentação da Media SDK JS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-javascript/set-up-js-2.html?lang=pt_BR) e a [documentação da API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html) para implementar o rastreamento de mídia.

>[!NOTE]
>
>**Testes:** nessa versão, para testar sua extensão, você deve carregá-la no [ Platform ](../../../extension-dev/submit/upload-and-test.md), onde você tem acesso a todas as extensões dependentes.


<!--
## Leveraging the sample HTML5 player

You can obtain the MA extension sample HTML5 player here: [HTML5 Sample Player](https://github.com/adobe/reactor-adobe-va-sample-player). The sample player acts as a reference to create video player extensions and to showcase using the MA extension to support media tracking.

### Sample player extension action types

This section describes the action types available in the Sample Player extension.

#### Open Video

The _Open Video_ action provides various configurations for creating and customizing an HTML5 player, providing a video to play and enabling/disabling Adobe Video Analytics tracking.

**Action Configuration / Player Settings:** Note the CSS Selector setting which specifics the `<div>` in the web page where the player is added. Note also that the _Enable Adobe Analytics_ checkbox is checked in the Analytics Settings pane.

![Player Extension Action Configuration](../../../images/ext-va-sp-action.png)

![Player Extension Action Configuration](../../../images/ext-va-sp-action1.png)

* [\[...\]/openVideo/openVideo.jsx](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/view/actions/openVideo/openVideo.jsx) -

  UI Code to configure the Action is defined here.

* [\[...\]/actions/openVideo.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/actions/openVideo.js) - This file exports a function that gets executed when the Action is triggered as part of the tag rule.

  This is a code snippet from `openVideo.js` where the `openVideo` Action is executed:

  ```javascript
    function openVideo(settings) {
        let player;
        try {
            Logger.info(LOG_TAG, `Executing action with ${JSON.stringify(settings)}`);

            player = new PlayerFacade(settings);
            PlayerStore.registerPlayer(player);
            player.load(settings.media);
        } catch (ex) {
            Logger.error(LOG_TAG, `Creating player for action openVideo failed with error ${ex.message}`);

            // Cleanup from DOM.
            if (player) {
                player.destroy();
            }
        }
    }
    ...
  ```

* [\[...\]/analytics/adobeAnalyticsProvider.js](https://github.com/adobe/reactor-adobe-va-sample-player/blob/master/src/lib/helpers/analytics/adobeAnalyticsProvider.js) - This file implements Video Analytics tracking by using Shared Modules exposed by the VA extension.

### Sample player extension basic deployment

Once the Sample Player extension is installed, you'll need to create at least one rule to properly deploy it. The Image below shows a sample rule that opens the specified video when the core extension fires the `DOMLoaded` event.

![Player Extension Sample Rule](../../../images/ext-va-sp-rule.png)

After you have saved this rule, you will need to add it to a Library, and then build and deploy so that you can test the behavior.

-->

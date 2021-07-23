---
title: Visão geral da extensão Adobe Medium Analytics (3.x SDK) for Audio and Video
description: Saiba mais sobre a extensão de tag Adobe Medium Analytics (3.x SDK) for Audio and Video no Adobe Experience Platform.
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 87%

---

# Visão geral da extensão do Adobe Media Analytics (3.x SDK) para áudio e vídeo

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Use esta documentação para obter informações sobre como instalar, configurar e implementar a extensão Adobe Media Analytics (3.x SDK) for Audio and Video (extensão do Media Analytics). Estão incluídas as opções disponíveis ao usar esta extensão para criar uma regra, juntamente com exemplos e links para amostras.

A extensão do Media Analytics (MA) adiciona a principal SDK de mídia JavaScript (Media 3.x SDK). Essa extensão fornece a funcionalidade necessária para adicionar a instância do rastreador `Media` a um site ou projeto habilitado para tags. A extensão do MA exige duas extensões adicionais:

* [Extensão do Analytics](../analytics/overview.md)
* [Extensão do Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>Essa extensão é implantada com o SDK do Media 3.x, que não é compatível com o SDK do Media 2.x. Se sua página já usa o SDK do Media 2.x, use a [Extensão Adobe Media Analytics for Audio and Video](../media-analytics/overview.md) em vez dessa extensão.

Depois de incluir todas as três extensões mencionadas acima em seu projeto habilitado para tags, você pode prosseguir de uma das duas formas a seguir:

* Use APIs `Media` do aplicativo web
* Com a inclusão ou criação de uma extensão específica para um reprodutor que mapeie eventos específicos daquele reprodutor de mídia para as APIs na instância do rastreador do `Media`. Essa instância é exposta por meio da extensão do MA.

## Instalação e configuração da extensão do MA

* **Instalar:** para instalar a extensão do MA, abra sua propriedade de extensão, selecione **[!UICONTROL Extensões > Catálogo]**, passe o mouse sobre o **[!UICONTROL Adobe Media Analytics (3.x SDK) para Extensão de áudio e]** vídeo e selecione **[!UICONTROL Instalar]**.

* **Configurar:** para configurar a extensão do MA, abra a guia [!UICONTROL Extensões], passe o mouse sobre a extensão e selecione **[!UICONTROL Configurar]**:

![Configuração de extensão do MA](../../../images/ext-ma-config.png)

### Opções de configuração:

| Opção | Descrição |
| :--- | :--- |
| Collection API Server | Define o Collection API Server de mídia (Entre em contato com seu representante da Adobe para obter este servidor) |
| Application Version | A versão do aplicativo do reprodutor de vídeo/SDK |
| Nome do reprodutor | Nome do reprodutor de vídeo em uso (por exemplo, &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom VideoPlayer&quot;) |
| Canal | Propriedade do nome do canal |
| Debug Logging | Ativar ou desativar registro |
| Enable SSL | Ativar ou desativar o envio de pings em HTTPS |
| Export APIs to Window Object | Ativar ou desativar a exportação de APIs do Media Analytics para o escopo global |
| Variable Name | Uma variável usada para exportar as APIs do Media Analytics sob o objeto `window` |

**Lembrete**: a extensão do MA exige as extensões do [Analytics](../analytics/overview.md) e da [Experience Cloud ID](../id-service/overview.md). Você também deve adicionar essas extensões à propriedade da sua extensão e configurá-las.

## Uso da extensão do MA

### Uso de uma página web/aplicativo JS

A extensão do MA exporta as APIs de mídia no objeto de janela global, habilitando a configuração &quot;Exportar APIs para objeto de janela&quot; na página [!UICONTROL Configuração]. Exporta as APIs sob o nome da variável configurada. Por exemplo, se o nome da variável estiver configurado para ser `ADB`, as APIs de mídia podem ser acessadas em `window.ADB.Media`.

>[!IMPORTANT]
>
>A extensão do MA exporta as APIs apenas quando `window["CONFIGURED_VARIABLE_NAME"]` está indefinido e não substitui as variáveis existentes.

1. **APIs de mídia:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Isso expõe todas as APIs e constantes do SDK de mídia: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Criar instância do Media Tracker:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Valor de retorno:** uma instância do rastreador `Media` para rastrear uma sessão de mídia.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Usando a instância do Media Tracker, siga a [documentação da API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) para implementar o rastreamento de mídia.

Você pode obter o player de amostra aqui: [reprodutor MA de amostra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). O reprodutor usado de exemplo atua como uma referência para mostrar como usar a extensão do MA para suportar o Media Analytics diretamente de um aplicativo web.


### Com o uso a partir de outras extensões

A extensão do MA expõe `media` como um módulo compartilhado a outras extensões. (Para obter informações adicionais sobre Módulos compartilhados, consulte a [documentação Módulos compartilhados](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Os módulos compartilhados podem ser acessados somente a partir de outras extensões. Ou seja, uma página web ou aplicativo JavaScript não podem acessar os módulos compartilhados ou usar `turbine` (consulte um exemplo de código abaixo) fora de uma extensão.

1. **APIs de mídia:** `media` módulo compartilhado

   Isso expõe todas as APIs e constantes do SDK de mídia: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Crie a instância do Media Tracker da seguinte maneira:

   **Valor de retorno:** uma instância do rastreador `Media` para rastrear uma sessão de mídia.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Usando a instância do Media Tracker, siga a [documentação da API JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) para implementar o rastreamento de mídia.

>[!NOTE]
>
>**Testes:** nessa versão, para testar sua extensão, você deve carregá-la no [ Platform ](../../../extension-dev/submit/upload-and-test.md), onde você tem acesso a todas as extensões dependentes.

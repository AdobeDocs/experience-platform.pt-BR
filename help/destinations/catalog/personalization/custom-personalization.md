---
keywords: personalização personalizada, destino, destino personalizado da experience platform,
title: Conexão de personalização personalizada
description: Esse destino fornece personalização externa, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados no site uma maneira de recuperar informações de público-alvo do Adobe Experience Platform. Esse destino fornece personalização em tempo real com base na associação do público-alvo do perfil do usuário.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 44a4d5c592e13cdd1d4d75787dee5e1763fae9a4
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 9%

---


# Conexão de personalização personalizada {#custom-personalization-connection}

## Log de alterações de destino {#changelog}

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Maio de 2023 | Atualização de funcionalidade e documentação | A partir de maio de 2023, a conexão **[!UICONTROL Custom personalization]** oferecerá suporte à [personalização baseada em atributos](../../ui/activate-edge-personalization-destinations.md#map-attributes) e estará disponível para todos os clientes. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, você deve usar a [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) ao configurar o destino **[!UICONTROL Custom Personalization]** para personalização baseada em atributos. Todas as chamadas de API do Edge Network devem ser feitas em um [contexto autenticado](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication).
>
><br>Você pode recuperar atributos de perfil por meio da [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) adicionando uma integração do lado do servidor que utiliza a mesma sequência de dados que você já está usando para a implementação da Web ou do Mobile SDK.
>
><br>Se você não seguir os requisitos acima, a personalização será baseada somente na associação ao público-alvo.

## Visão geral {#overview}

Configure esse destino para permitir que plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos em execução nos sites do cliente recuperem informações de público do Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Esse destino requer o uso de um dos seguintes métodos de coleta de dados, dependendo de sua implementação:

* Use o [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) se desejar coletar dados do seu site.
* Use o [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) se desejar coletar dados do seu aplicativo móvel.
* Use a [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) se não estiver usando o [Web SDK](/help/web-sdk/home.md) ou o [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/), ou se quiser personalizar a experiência do usuário com base nos atributos do perfil.

>[!IMPORTANT]
>
>**Requisitos de personalização baseados em atributos:** Se você quiser personalizar com base em atributos de perfil (não apenas na associação de público-alvo), **deverá** usar a [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) com integração autenticada no lado do servidor, independentemente de você também estar usando o Web SDK ou o Mobile SDK para coleta de dados.
>
>O Web SDK e o Mobile SDK somente oferecem suporte à personalização com base na associação ao público. A API do Edge Network é **necessária** para recuperar com segurança os atributos de perfil para personalização.

>[!IMPORTANT]
>
>Antes de criar uma conexão de personalização personalizada, leia o guia sobre como [ativar dados de público-alvo para destinos de personalização de borda](../../ui/activate-edge-personalization-destinations.md). Este guia aborda as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página em vários componentes do Experience Platform.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!DNL Profile request]** | Você está solicitando todos os públicos mapeados no destino de personalização personalizado para um único perfil. Destinos de personalização personalizados diferentes podem ser configurados para [sequências de dados de Coleção de dados da Adobe](../../../datastreams/overview.md) diferentes. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre sequências de dados"
>abstract="Essa opção determina em qual sequência de coleção de dados os públicos-alvo serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Você deve configurar uma sequência de dados de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR" text="Saiba como configurar uma sequência de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Integration alias]**: esse valor é enviado para o Experience Platform Web SDK como um nome de objeto JSON.
* **[!UICONTROL Datastream]**: isso determina em qual sequência de dados de Coleção de Dados os públicos serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurando uma sequência de dados](../../../datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia [Ativar perfis e públicos-alvo para destinos de personalização de borda](../../ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados {#exported-data}

Se você estiver usando [Tags no Adobe Experience Platform](../../../tags/home.md) para implantar o Experience Platform Web SDK, use a funcionalidade [enviar evento concluído](../../../tags/extensions/client/web-sdk/event-types.md) e sua ação de código personalizado terá uma variável `event.destinations` que você pode usar para ver os dados exportados.

Este é um exemplo de valor para a variável `event.destinations`:

```
[
   {
      "type":"profileLookup",
      "destinationId":"7bb4cb8d-8c2e-4450-871d-b7824f547111",
      "alias":"personalizationAlias",
      "segments":[
         {
            "id":"399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         },
         {
            "id":"499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
         }
      ]
   }
]
```

Se você não estiver usando [Tags](/help/tags/home.md) para implantar o Experience Platform Web SDK, use [respostas de comando](/help/web-sdk/commands/command-responses.md) para ver os dados exportados.

A resposta JSON do Adobe Experience Platform pode ser analisada para encontrar o alias de integração correspondente do aplicativo que você está integrando com o Adobe Experience Platform. As IDs de público-alvo podem ser passadas para o código do aplicativo como parâmetros de direcionamento. Abaixo está uma amostra do que isso pareceria específico para a resposta de destino.

```
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
}).then(function(result) {
    if(result.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = result.destinations.filter(x => x.alias == "personalizationAlias")
        if(personalizationDestinations.length > 0) {
             // Code to pass the audience IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = result.destinations.filter(x => x.alias == "adServerAlias")
        if(adServerDestinations.length > 0) {
            // Code to pass the audience IDs into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```

### Exemplo de resposta para [!UICONTROL Custom Personalization With Attributes]

Ao usar **[!UICONTROL Custom Personalization With Attributes]**, a resposta da API será semelhante ao exemplo abaixo.

A diferença entre **[!UICONTROL Custom Personalization With Attributes]** e **[!UICONTROL Custom Personalization]** é a inclusão da seção `attributes` na resposta da API.

```json
[
    {
        "type": "profileLookup",
        "destinationId": "7bb4cb8d-8c2e-4450-871d-b7824f547130",
        "alias": "personalizationAlias",
        "attributes": {
             "countryCode": {
                   "value" : "DE"
              },
             "membershipStatus": {
                   "value" : "PREMIUM"
              }
         },         
        "segments": [
            {
                "id": "399eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            },
            {
                "id": "499eb3e7-3d50-47d3-ad30-a5ad99e8ab77"
            }
        ]
    }
]
```

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](../../../data-governance/home.md).

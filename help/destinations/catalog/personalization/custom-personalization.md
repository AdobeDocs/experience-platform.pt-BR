---
keywords: personalização personalizada, destino, destino personalizado da experience platform,
title: Conexão Personalization personalizada
description: Saiba como configurar o destino do Personalization personalizado para recuperar dados de público-alvo do Adobe Experience Platform e personalizá-los no site em tempo real.
exl-id: 2382cc6d-095f-4389-8076-b890b0b900e3
source-git-commit: 3779531814cbf7e5718db0ac88aca266f14a1b21
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 9%

---


# Conexão Personalization personalizada {#custom-personalization-connection}

## Log de alterações de destino {#changelog}

Use esse changelog para rastrear atualizações no destino do Personalization personalizado.

| Mês de lançamento | Tipo de atualização | Descrição |
| --- | --- | --- |
| Maio de 2023 | Atualização de funcionalidade e documentação | A partir de maio de 2023, a conexão **[!UICONTROL Custom personalization]** oferecerá suporte à [personalização baseada em atributos](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) e estará disponível para todos os clientes. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Os atributos do perfil podem conter dados confidenciais. Para proteger esses dados, use a [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) ao configurar o destino **[!UICONTROL Custom Personalization]** para personalização baseada em atributos. Todas as chamadas de API do Edge Network devem ser feitas em um [contexto autenticado](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication).
>
>Recupere atributos de perfil por meio da [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) adicionando uma integração do lado do servidor que usa a mesma sequência de dados que você já está usando para a implementação da Web ou do SDK Móvel.
>
>Se você não seguir os requisitos acima, a personalização será baseada somente na associação ao público-alvo.

## Visão geral {#overview}

Configure este destino para permitir que plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos em execução nos sites do cliente recuperem informações de público do [!DNL Adobe Experience Platform].

## Pré-requisitos {#prerequisites}

Dependendo da sua implementação, esse destino exige um dos seguintes métodos de coleta de dados:

* Use o [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) para coletar dados do seu site.
* Use o [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) para coletar dados do seu aplicativo móvel.
* Use a [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) se não estiver usando o Web SDK ou o Mobile SDK, ou se quiser personalizar a experiência do usuário com base nos atributos do perfil.

>[!IMPORTANT]
>
>**Requisitos de personalização baseados em atributos:** para personalizar com base em atributos de perfil (não apenas na associação de público-alvo), você **deve** usar a [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/) com integração autenticada do lado do servidor, independentemente de você também estar usando o Web SDK ou o Mobile SDK para coleta de dados.
>
>O Web SDK e o Mobile SDK oferecem suporte à personalização somente com base na associação ao público-alvo. A API do Edge Network é **necessária** para recuperar com segurança os atributos de perfil para personalização.

>[!IMPORTANT]
>
>Antes de criar uma conexão Personalization personalizada, leia o guia sobre como [ativar dados de público-alvo para destinos de personalização de borda](/help/destinations/ui/activate-edge-personalization-destinations.md). Este guia aborda as etapas de configuração necessárias para casos de uso de personalização de mesma página e próxima página em vários componentes do Experience Platform.

## Públicos-alvo compatíveis {#supported-audiences}

A tabela a seguir lista os tipos de público-alvo que você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sim | Públicos-alvo gerados pelo [Serviço de Segmentação](/help/segmentation/home.md) da Experience Platform. |
| Todas as outras origens de público-alvo | Sim | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li>carregar audiências personalizadas [importadas](/help/segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV,</li><li>públicos-alvo semelhantes,</li><li>públicos federados,</li><li>públicos-alvo gerados em outros aplicativos Experience Platform, como [!DNL Adobe Journey Optimizer],</li><li>e muito mais.</li></ul> |

{style="table-layout:auto"}

Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Direcione grupos específicos de pessoas com base nos perfis dos clientes. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake [!DNL Adobe Experience Platform]. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

A tabela a seguir descreve o tipo de exportação e a frequência desse destino.

| Item | Tipo | Notas |
| --- | --- | --- |
| Tipo de exportação | **[!UICONTROL Profile request]** | Solicita todos os públicos mapeados no destino do Personalization personalizado para um único perfil. Diferentes destinos de Personalization Personalizado podem ser configurados para diferentes [sequências de dados de Coleção de dados da Adobe](/help/datastreams/overview.md). |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões sempre ativas baseadas em API. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_custom_personalization_datastream"
>title="Sobre sequências de dados"
>abstract="Essa opção determina em qual sequência de coleção de dados os públicos-alvo serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Você deve configurar uma sequência de dados de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR" text="Saiba como configurar uma sequência de dados"

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](/help/destinations/ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](/help/destinations/ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Integration alias]**: uma cadeia de caracteres necessária que identifica este destino na resposta de personalização. O valor do alias é retornado ao seu site ou aplicativo, juntamente com os públicos-alvo (e, se configurado, os atributos) associados a esse destino. Use o alias no código do lado do cliente ou do lado do servidor para localizar e processar o objeto de personalização correto quando vários destinos de personalização estiverem ativos no mesmo fluxo de dados. O alias deve ser exclusivo em uma sandbox em todos os destinos do Personalization personalizado.
* **[!UICONTROL Datastream]**: isso determina em qual sequência de dados de Coleção de Dados os públicos serão incluídos na resposta à página. O menu suspenso mostra apenas as sequências de dados com a configuração de destino habilitada. Consulte [Configurando uma sequência de dados](/help/datastreams/overview.md) para obter mais detalhes.

### Ativar alertas {#enable-alerts}

Ative os alertas para receber notificações sobre o status do fluxo de dados para esse destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](/help/destinations/ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
>
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Leia [Ativar perfis e públicos-alvo para destinos de personalização de borda](/help/destinations/ui/activate-edge-personalization-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados {#exported-data}

Se você estiver usando [Tags no Adobe Experience Platform](/help/tags/home.md) para implantar o Experience Platform Web SDK, use a funcionalidade [enviar evento concluído](/help/tags/extensions/client/web-sdk/event-types.md). Sua ação de código personalizado terá uma variável `event.destinations` que você pode usar para ver os dados exportados.

Este é um exemplo de valor para a variável `event.destinations`:

```json
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

Se você não estiver usando [Tags](/help/tags/home.md) para implantar o Experience Platform Web SDK, use [respostas de comando](/help/collection/js/commands/command-responses.md) para ver os dados exportados.

Analise a resposta JSON de [!DNL Adobe Experience Platform] para encontrar o alias de integração do aplicativo que você está integrando com o [!DNL Adobe Experience Platform]. Transmita as IDs de público-alvo para o código do aplicativo como parâmetros de direcionamento. Abaixo está uma amostra do que isso parece específico para a resposta de destino.

```js
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

### Exemplo de resposta para Personalization personalizado com atributos {#example-response-attributes}

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

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

---
keywords: personalização personalizada; destino; destino personalizado da experience platform;
title: Conexão de personalização personalizada (Beta)
description: Esse destino fornece personalização externa, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em seu site para recuperar informações de segmento do Adobe Experience Platform. Esse destino fornece 1:1 em tempo real e personalização com base na associação de segmento de um perfil de usuário.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# Conexão de personalização personalizada (Beta) {#custom-personalization-connection}

## Visão geral {#overview}

>[!IMPORTANT]
>
>A conexão de personalização personalizada no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

Esse destino fornece uma maneira de recuperar informações do segmento do Adobe Experience Platform para plataformas de personalização externas, sistemas de gerenciamento de conteúdo, servidores de anúncios e outros aplicativos que estão sendo executados em sites do cliente.

## Pré-requisitos {#prerequisites}

Essa integração é disponibilizada pelo [Adobe Experience Platform Web SDK](../../../edge/home.md). Você deve usar esse SDK para usar esse destino.

## Tipo de exportação {#export-type}

**Solicitação de perfil**  - você está solicitando todos os segmentos que estão mapeados no destino de personalização personalizada para um único perfil. Diferentes destinos de personalização personalizados podem ser configurados para diferentes [Data Collection datastreams](../../../edge/fundamentals/datastreams.md) do Adobe.

## Casos de uso {#use-cases}

Esse destino compartilha públicos com servidores de anúncios e aplicativos de personalização que não sejam Adobe, a serem usados em tempo real, para decidir quais usuários de anúncios devem ver em um site.

### Caso de uso nº 1

**Personalização de uma página inicial**

Um site de aluguel doméstico e vendas deseja personalizar sua página inicial com base nas qualificações de segmento no Adobe Experience Platform. A empresa pode selecionar quais públicos-alvo devem obter uma experiência personalizada e mapeá-los para o destino de personalização personalizado que foi configurado para seu aplicativo de personalização que não é Adobe como critério de direcionamento.

**Anúncios no site direcionados**

Usando um destino de personalização personalizado separado para o servidor de publicidade, o mesmo site pode direcionar a publicidade no site usando um conjunto diferente de segmentos do Adobe Experience Platform como critérios de definição de metas.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **[!UICONTROL Alias]** da integração: Esse valor é enviado para o SDK da Web do Experience Platform como um nome de objeto JSON.
* **[!UICONTROL ID]** do conjunto de dados: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Consulte [Configurar um conjunto de dados](../../../edge/fundamentals/datastreams.md) para obter mais detalhes.

## Ativar segmentos para este destino {#activate}

Leia [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

Se estiver usando [Tags do Adobe](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use a funcionalidade [enviar evento concluído](../../../edge/extension/event-types.md) e sua ação de código personalizado terá uma variável `event.destinations` que poderá ser usada para ver os dados exportados.

Se você não estiver usando [Tags do Adobe](../../../tags/home.md) para implantar o SDK da Web do Experience Platform, use a funcionalidade [manipular respostas de eventos](../../../edge/fundamentals/tracking-events.md#handling-responses-from-events) para ver os dados exportados.

A resposta JSON do Adobe Experience Platform pode ser analisada para encontrar o alias de integração correspondente do aplicativo que você está integrando com o Adobe Experience Platform. As IDs de segmento podem ser passadas para o código do aplicativo como parâmetros de direcionamento. Abaixo está uma amostra do que seria específico para a resposta de destino.

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
}).then(function(results) {
    if(results.destinations) { // Looking to see if the destination results are there
 
        // Get the destination with a particular alias
        var personalizationDestinations = results.destinations.filter(x => x.alias == “personalizationAlias”)
        if(personalizationDestinations.length > 0) {
             // Code to pass the segment IDs into the system that corresponds to personalizationAlias
        }
        var adServerDestinations = results.destinations.filter(x => x.alias == “adServerAlias”)
        if(adServerDestinations.length > 0) {
            // Code to pass the segment ids into the system that corresponds to adServerAlias
        }
     }
   })
  .catch(function(error) {
    // Tracking the event failed.
  });
```


## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](../../../data-governance/home.md).

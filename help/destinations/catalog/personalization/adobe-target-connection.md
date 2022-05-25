---
keywords: personalização do target; destino; destino do target da experience platform; destino do adobe target;
title: Conexão Adobe Target
description: O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação alimentados por IA em tempo real em todas as interações de entrada do cliente em sites, aplicativos móveis e muito mais.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 0868d81bcd1968b3223c79abb5a7bb8f279a4130
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---

# Conexão Adobe Target {#adobe-target-connection}

## Visão geral {#overview}

O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação alimentados por IA em tempo real em todas as interações de entrada do cliente em sites, aplicativos móveis e muito mais.

Adobe Target é uma conexão de personalização no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Ao configurar a conexão do Adobe Target com o [usar uma ID do datastream](#parameters), você deve ter o [Adobe Experience Platform Web SDK](../../../edge/home.md) implementado.

Configurar a conexão do Adobe Target sem usar uma ID de armazenamento de dados não requer a implementação do SDK da Web.

>[!IMPORTANT]
>
>Antes de criar uma [!DNL Adobe Target] leia o guia sobre como [configurar destinos de personalização para a personalização da mesma página e da próxima página](../../ui/configure-personalization-destinations.md). Este guia o orienta pelas etapas de configuração necessárias para casos de uso de personalização de página mesma e próxima, em vários componentes de Experience Platform. A personalização de mesma página e próxima requer o uso de uma ID de armazenamento de dados ao configurar a conexão do Adobe Target.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!DNL Profile request]** | Você está solicitando todos os segmentos que estão mapeados no destino Adobe Target para um único perfil. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

**Personalização de um banner de página inicial**

Uma empresa de aluguel e vendas da casa deseja personalizar sua página inicial com um banner, com base nas qualificações do segmento do cliente no Adobe Experience Platform. A empresa pode selecionar quais públicos-alvo devem obter uma experiência personalizada e enviá-los para o Adobe Target como critérios de direcionamento para sua oferta do Target.

## Conecte-se ao destino {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Sobre IDs de fluxo de dados"
>abstract="Essa opção determina em qual conjunto de dados de coleta os segmentos serão incluídos. O menu suspenso mostra apenas os conjuntos de dados que têm a configuração do Target ativada. Para usar a segmentação de borda, você deve selecionar uma ID de armazenamento de dados. Selecionar Nenhum desativa todos os casos de uso que usam segmentação de borda."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Saiba mais sobre a seleção de conjuntos de dados."

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Experience Platform se conecta automaticamente à instância do Adobe Target de sua empresa. Não é necessária nenhuma autenticação.

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **Nome**: Preencha o nome preferencial para esse destino.
* **Descrição**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **ID do fluxo de dados**: Isso determina em qual armazenamento de dados da Coleta de dados os segmentos serão incluídos. O menu suspenso mostra apenas os conjuntos de dados que têm o destino do Target ativado. Consulte [configuração de um armazenamento de dados](../../../edge/datastreams/overview.md#target) para obter informações detalhadas sobre como configurar um conjunto de dados para o Adobe Target.
   * **[!UICONTROL Nenhum]**: Selecione essa opção se precisar configurar a personalização do Adobe Target, mas não puder implementar o [Experience Platform Web SDK](../../../edge/home.md). Ao usar essa opção, os segmentos exportados do Experience Platform para o Target são compatíveis apenas com a personalização da próxima sessão e a segmentação de borda é desativada. Consulte a tabela abaixo para obter mais informações.

| Nenhum armazenamento de dados selecionado | Datastream selecionado |
|---|---|
| <ul><li>[Segmentação de borda](../../../segmentation/ui/edge-segmentation.md) não é suportado.</li><li>[Personalização de mesma página e próxima página](../../ui/configure-personalization-destinations.md) não são compatíveis.</li><li>É possível compartilhar segmentos na conexão do Adobe Target somente para a sandbox de produção.</li><li>Para configurar a personalização da próxima sessão sem usar uma ID de armazenamento de dados, use [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>A segmentação de borda funciona conforme o esperado.</li><li>[Personalização de mesma página e próxima página](../../ui/configure-personalization-destinations.md) são compatíveis.</li><li>O compartilhamento de segmentos é compatível com outras sandboxes.</li></ul> |

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

O Adobe Target lê os dados do perfil da Adobe Experience Platform Edge Network, de modo que nenhum dado é exportado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

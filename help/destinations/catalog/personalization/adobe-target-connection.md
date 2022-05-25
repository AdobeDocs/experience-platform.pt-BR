---
keywords: personalização do target; destino; destino do target da experience platform; destino do adobe target;
title: Conexão Adobe Target
description: O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação alimentados por IA em tempo real em todas as interações de entrada do cliente em sites, aplicativos móveis e muito mais.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Conexão Adobe Target {#adobe-target-connection}

## Visão geral {#overview}

O Adobe Target é um aplicativo que fornece recursos de personalização e experimentação alimentados por IA em tempo real em todas as interações de entrada do cliente em sites, aplicativos móveis e muito mais.

Adobe Target é uma conexão de personalização no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Essa integração é alimentada pela variável [Adobe Experience Platform Web SDK](../../../edge/home.md). Você deve usar esse SDK para usar esse destino.

>[!IMPORTANT]
>
>Antes de criar uma [!DNL Adobe Target] leia o guia sobre como [configurar destinos de personalização para a personalização da mesma página e da próxima página](../../ui/configure-personalization-destinations.md). Este guia o orienta pelas etapas de configuração necessárias para casos de uso de personalização de página mesma e próxima, em vários componentes de Experience Platform.

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
>abstract="Essa opção determina em qual conjunto de dados de coleta os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Você deve configurar um armazenamento de dados antes de configurar seu destino."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Saiba como configurar um armazenamento de dados"

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Experience Platform se conecta automaticamente à instância do Adobe Target de sua empresa. Não é necessária nenhuma autenticação.

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **Nome**: Preencha o nome preferencial para esse destino.
* **Descrição**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **ID do fluxo de dados**: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Consulte [Configurar um conjunto de dados](../../../edge/datastreams/overview.md) para obter mais detalhes.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

O Adobe Target lê os dados do perfil da Adobe Experience Platform Edge Network, de modo que nenhum dado é exportado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

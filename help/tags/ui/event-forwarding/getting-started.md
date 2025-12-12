---
title: Introdução ao encaminhamento de eventos
description: Siga este tutorial passo a passo para começar a usar o encaminhamento de eventos na Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 67%

---

# Introdução ao encaminhamento de eventos

>[!NOTE]
>
>O encaminhamento de eventos é um recurso pago incluído como parte das ofertas de Conexões da Adobe Real-Time Customer Data Platform, Prime ou Ultimate.

Para usar a Adobe Experience Platform, os dados devem ser enviados à borda da rede da Adobe Experience Platform usando uma ou mais das três seguintes opções:

* [SDK da Web da Adobe Experience Platform](../../extensions/client/web-sdk/overview.md)
* [SDK móvel da Adobe Experience Platform](https://sdkdocs.com)
* [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/)

>[!NOTE]
>A Experience Platform Web SDK e o Experience Platform Mobile SDK não exigem implantação por meio de tags na Adobe Experience Platform. No entanto, a utilização de tags para implantar esses SDKs é a abordagem recomendada.

Depois de enviar dados para a rede de borda, você pode alternar entre as soluções da Adobe para enviar dados para lá. Para enviar dados a uma solução que não seja da Adobe, configure-os no encaminhamento de eventos.

## Pré-requisitos

* Adobe Real-Time CDP Connections, Prime ou Ultimate (Entre em contato com a equipe de conta da Adobe para obter preços)
* Encaminhamento de eventos na Adobe Experience Platform
* Adobe Experience Platform Web SDK, Mobile SDK ou API do Edge Network configurada para enviar dados para o Edge Network
* Mapear dados para o Experience Data Model (XDM) (esse mapeamento pode ser feito usando tags)

## Criar um esquema do XDM

Na Adobe Experience Platform, crie seu esquema.

1. Crie um novo esquema selecionando **[!UICONTROL Schemas]** > **[!UICONTROL Create Schema]** e a opção **[!UICONTROL XDM ExperienceEvent]**.

1. Dê um nome e uma breve descrição ao esquema.

1. Você pode adicionar o campo &quot;Detalhes da Web do ExperienceEvent&quot; selecionando **[!UICONTROL Add]** ao lado de **[!UICONTROL Field Groups]**.

   >[!NOTE]
   >
   >É possível adicionar vários grupos de campo, se desejado.

1. Salve o esquema e anote o nome que você deu a ele.

Para obter mais informações sobre esquemas, consulte [Ajuda do sistema do Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

## Criar uma propriedade de encaminhamento de evento

No espaço de trabalho **[!UICONTROL Tags]**, crie uma propriedade do tipo **[!UICONTROL Edge]**.

1. Selecione **[!UICONTROL New Property]**.

1. Nomeie a propriedade.

1. Escolha o tipo de plataforma &quot;Edge&quot;.

1. Selecione **[!UICONTROL Save]**.

Depois de criar a propriedade, vá para a guia **[!UICONTROL Environments]** da nova propriedade e
anote as IDs de ambiente. Se a Organização do Adobe usada no fluxo de dados for diferente da Organização do Adobe usada no encaminhamento de eventos, será possível copiar a ID do ambiente da guia **[!UICONTROL Environments]** e colá-la ao criar um fluxo de dados. Caso contrário, você pode selecionar o ambiente em um menu suspenso.

## Criar um fluxo de dados

Para criar o fluxo de dados na Adobe Experience Platform, use a ID de ambiente gerada ao criar a propriedade de encaminhamento de eventos.

1. Selecione **[!UICONTROL Datastreams]** na navegação à esquerda.

1. Nomeie a configuração e forneça uma descrição opcional.
A descrição ajuda a identificar configurações em uma lista de várias configurações.

1. Selecione **[!UICONTROL Save]**.

## Habilitar o encaminhamento de eventos {#enable-event-forwarding}

Em seguida, configure o Edge Network para enviar dados ao encaminhamento de eventos e a outros produtos da Adobe.

1. No espaço de trabalho **[!UICONTROL Datastreams]**, selecione a propriedade que você criou.

1. Selecione Desenvolvimento, Produção ou Ambiente de preparo.

   Ou, para enviar dados a um ambiente de encaminhamento de eventos fora da organização da Adobe, selecione **[!UICONTROL Switch to Advanced Mode]** e cole em uma ID. A ID é fornecida quando você cria uma propriedade de encaminhamento de eventos.

1. Ative as ferramentas necessárias e configure conforme necessário.

   * A Adobe Analytics exige uma ID de conjunto de relatórios.

   * O encaminhamento de eventos na Adobe Experience Platform exige uma ID de propriedade e uma ID de ambiente. Esse é o caminho de publicação da propriedade de encaminhamento de eventos.

Depois de configurar, anote as IDs de ambiente para a nova propriedade.

## Configure a extensão Experience Platform Web SDK para enviar dados ao fluxo de dados criado anteriormente

Crie sua propriedade no espaço de trabalho **[!UICONTROL Tags]**, navegue até **[!UICONTROL Extensions]** e selecione a extensão Experience Platform Web SDK no catálogo para configurá-la e instalá-la.

Consulte a [documentação de extensão do Web SDK](../../extensions/client/web-sdk/overview.md) para obter detalhes sobre as opções de configuração.

## Criar uma regra de tag para enviar dados ao Experience Platform Web SDK

Depois que tudo estiver configurado, crie definições de dados, regras e assim por diante, que usam encaminhamento de eventos e tags, mas que só precisam de uma única solicitação da página.

Crie uma regra de carregamento de página usando a extensão do Experience Platform Web SDK e o tipo de ação &quot;Enviar evento&quot;:

1. Abra a guia **[!UICONTROL Rules]** e selecione **[!UICONTROL Create New Rule]**.

1. Atribua um nome à regra.

1. Selecione **[!UICONTROL Events Add]**.

1. Adicione um evento escolhendo uma extensão e um dos tipos de eventos disponíveis para essa extensão e, em seguida, defina as configurações para o evento. Por exemplo, selecione **[!UICONTROL Core - Window Loaded]**.

1. Adicione uma ação usando a extensão Experience Platform Web SDK. Selecione **[!UICONTROL Send Event]** na lista **[!UICONTROL Action Type]**, selecione a Instância desejada (instância Alloy configurada anteriormente) e, em seguida, selecione um elemento de dados para adicionar ao Bloco de dados do XDM no hit Alloy.

1. Deixe o restante das configurações como padrão para este exemplo e selecione **[!UICONTROL Save]**.

Em outro exemplo, você pode criar uma regra que enviará a camada de dados para o Edge se o usuário passar o mouse sobre um botão especificado.

## Resumo

Com os itens a seguir preparados, agora é possível criar regras de encaminhamento de eventos para encaminhar dados a destinos que não são da Adobe.

* Esquema do Experience Data Model (Anote o nome que você deu a ele.)
* Uma propriedade de encaminhamento de eventos (mantenha o controle da ID de propriedade e das IDs de ambiente).
* Um fluxo de dados (observe a ID de ambiente, que não deve ser confundida com a ID de ambiente do encaminhamento de eventos).
* Uma propriedade de tag

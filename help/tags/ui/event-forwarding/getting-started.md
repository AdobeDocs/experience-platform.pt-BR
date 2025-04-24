---
title: Introdução ao encaminhamento de eventos
description: Siga este tutorial passo a passo para começar a usar o encaminhamento de eventos na Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 71%

---

# Introdução ao encaminhamento de eventos

>[!NOTE]
>
>O encaminhamento de eventos é um recurso pago incluído como parte das ofertas de Conexões da Adobe Real-Time Customer Data Platform, Prime ou Ultimate.

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

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

1. Crie um esquema selecionando **[!UICONTROL Esquemas]** > **[!UICONTROL Criar esquema]** e escolhendo a opção **[!UICONTROL XDM ExperienceEvent]**.

1. Dê um nome e uma breve descrição ao esquema.

1. Você pode adicionar o campo &quot;Detalhes da Web do ExperienceEvent&quot; selecionando **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos do Campo]**.

   >[!NOTE]
   >
   >É possível adicionar vários grupos de campo, se desejado.

1. Salve o esquema e anote o nome que você deu a ele.

Para obter mais informações sobre esquemas, consulte [Ajuda do sistema do Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

## Criar uma propriedade de encaminhamento de evento

No espaço de trabalho **[!UICONTROL Marcas]**, crie uma propriedade do tipo **[!UICONTROL Edge]**.

1. Selecione **[!UICONTROL Nova propriedade]**.

1. Nomeie a propriedade.

1. Escolha o tipo de plataforma &quot;Edge&quot;.

1. Selecione **[!UICONTROL Salvar]**.

Depois de criar a propriedade, vá para a guia **[!UICONTROL Ambientes]** da nova propriedade e
anote as IDs de ambiente. Se a Organização do Adobe usada na sequência de dados for diferente da Organização do Adobe usada no encaminhamento de eventos, será possível copiar a ID do ambiente da guia **[!UICONTROL Ambientes]** e colá-la ao criar uma sequência de dados. Caso contrário, você pode selecionar o ambiente em um menu suspenso.

## Criar um fluxo de dados

Para criar o fluxo de dados na Adobe Experience Platform, use a ID de ambiente gerada ao criar a propriedade de encaminhamento de eventos.

1. Selecione **[!UICONTROL Datastreams]** na navegação à esquerda.

1. Nomeie a configuração e forneça uma descrição opcional.
A descrição ajuda a identificar configurações em uma lista de várias configurações.

1. Selecione **[!UICONTROL Salvar]**.

## Ativar o encaminhamento de eventos {#enable-event-forwarding}

Em seguida, configure o Edge Network para enviar dados ao encaminhamento de eventos e a outros produtos da Adobe.

1. No espaço de trabalho **[!UICONTROL Datastreams]**, selecione a propriedade que você criou.

1. Selecione Desenvolvimento, Produção ou Ambiente de preparo.

   Ou, para enviar dados a um ambiente de encaminhamento de eventos fora da organização da Adobe, selecione **[!UICONTROL Alternar para o modo avançado]** e cole uma ID. A ID é fornecida quando você cria uma propriedade de encaminhamento de eventos.

1. Ative as ferramentas necessárias e configure conforme necessário.

   * A Adobe Analytics exige uma ID de conjunto de relatórios.

   * O encaminhamento de eventos na Adobe Experience Platform exige uma ID de propriedade e uma ID de ambiente. Esse é o caminho de publicação da propriedade de encaminhamento de eventos.

Depois de configurar, anote as IDs de ambiente para a nova propriedade.

## Configure a extensão Experience Platform Web SDK para enviar dados ao fluxo de dados criado anteriormente

Crie a propriedade no espaço de trabalho **[!UICONTROL Tags]**, navegue até **[!UICONTROL Extensões]** e selecione a extensão Experience Platform Web SDK no catálogo para configurá-la e instalá-la.

Consulte a [documentação de extensão do Web SDK](../../extensions/client/web-sdk/overview.md) para obter detalhes sobre as opções de configuração.

## Criar uma regra de tag para enviar dados ao Experience Platform Web SDK

Depois que tudo estiver configurado, crie definições de dados, regras e assim por diante, que usam encaminhamento de eventos e tags, mas que só precisam de uma única solicitação da página.

Crie uma regra de carregamento de página usando a extensão do Experience Platform Web SDK e o tipo de ação &quot;Enviar evento&quot;:

1. Abra a guia **[!UICONTROL Regras]** e selecione **[!UICONTROL Criar nova regra]**.

1. Atribua um nome à regra.

1. Selecione **[!UICONTROL Adicionar eventos]**.

1. Adicione um evento escolhendo uma extensão e um dos tipos de eventos disponíveis para essa extensão e, em seguida, defina as configurações para o evento. Por exemplo, selecione **[!UICONTROL Principal - Janela carregada]**.

1. Adicione uma ação usando a extensão Experience Platform Web SDK. Selecione **[!UICONTROL Enviar evento]** na lista **[!UICONTROL Tipo de ação]**, selecione a instância desejada (instância do Alloy configurada anteriormente) e, em seguida, selecione um elemento de dados para adicionar ao bloco de dados XDM dentro da ocorrência do Alloy.

1. Deixe o restante das configurações como padrão para este exemplo e selecione **[!UICONTROL Salvar]**.

Em outro exemplo, você pode criar uma regra que enviará a camada de dados para o Edge se o usuário passar o mouse sobre um botão especificado.

## Resumo

Com os itens a seguir preparados, agora é possível criar regras de encaminhamento de eventos para encaminhar dados a destinos que não são da Adobe.

* Esquema do Experience Data Model (Anote o nome que você deu a ele.)
* Uma propriedade de encaminhamento de eventos (mantenha o controle da ID de propriedade e das IDs de ambiente).
* Um fluxo de dados (observe a ID de ambiente, que não deve ser confundida com a ID de ambiente do encaminhamento de eventos).
* Uma propriedade de tag

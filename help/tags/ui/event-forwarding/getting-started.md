---
title: Introdução ao encaminhamento de eventos
description: Siga este tutorial passo a passo para começar a usar o encaminhamento de eventos na Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: efe88b582b4539a14f32c6e2c80a8b35cde1626e
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 79%

---

# Introdução ao encaminhamento de eventos

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Para usar a Adobe Experience Platform, os dados devem ser enviados à borda da rede da Adobe Experience Platform usando uma ou mais das três seguintes opções:

* [SDK da Web da Adobe Experience Platform](../../extensions/client/web-sdk/overview.md)
* [SDK móvel da Adobe Experience Platform](https://sdkdocs.com)
* [API servidor para servidor](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=pt-BR)

>[!NOTE]
>O SDK da Web da Platform e o SDK móvel da Platform não exigem implantação por meio de tags na Adobe Experience Platform. No entanto, a utilização de tags para implantar esses SDKs é a abordagem recomendada.

Depois de enviar dados para a rede de borda, você pode alternar entre as soluções da Adobe para enviar dados para lá. Para enviar dados a uma solução que não seja da Adobe, configure-os no encaminhamento de eventos.

## Pré-requisitos

* Adobe Real-Time CDP Connections, Prime ou Ultimate (Entre em contato com a equipe de conta do Adobe para obter preços)
* Encaminhamento de eventos na Adobe Experience Platform
* SDK da Web ou móvel da Adobe Experience Platform, configurado para enviar dados para a rede de borda
* Mapear dados para o Experience Data Model (XDM) (esse mapeamento pode ser feito usando tags)

## Criar um esquema do XDM

Na Adobe Experience Platform, crie seu esquema.

1. Crie um esquema selecionando **[!UICONTROL Esquemas]** > **[!UICONTROL Criar esquema]** e escolhendo a opção **[!UICONTROL XDM ExperienceEvent]**.

1. Dê um nome e uma breve descrição ao esquema.

1. Você pode adicionar o campo &quot;Detalhes da Web do ExperienceEvent&quot; selecionando **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de campos]**.

   >[!NOTE]
   >
   >É possível adicionar vários grupos de campo, se desejado.

1. Salve o esquema e anote o nome que você deu a ele.

Para obter mais informações sobre esquemas, consulte [Ajuda do sistema do Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

## Criar uma propriedade de encaminhamento de evento

No **[!UICONTROL Tags]** espaço de trabalho, crie uma propriedade do tipo **[!UICONTROL Edge]**.

1. Selecione **[!UICONTROL Nova propriedade]**.

1. Nomeie a propriedade.

1. Escolha o tipo de plataforma &quot;Borda&quot;.

1. Selecione **[!UICONTROL Salvar]**.

Depois de criar a propriedade, vá para a guia **[!UICONTROL Ambientes]** da nova propriedade e
anote as IDs de ambiente. Se a Organização de Adobe usada no fluxo de dados for diferente da Organização de Adobe usada no encaminhamento de eventos, será possível copiar a ID do ambiente da **[!UICONTROL Ambientes]** e cole-a ao criar um fluxo de dados. Caso contrário, você pode selecionar o ambiente em um menu suspenso.

## Criar um fluxo de dados

Para criar o fluxo de dados na Adobe Experience Platform, use a ID de ambiente gerada ao criar a propriedade de encaminhamento de eventos.

1. Selecionar **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

1. Nomeie a configuração e forneça uma descrição opcional.
A descrição ajuda a identificar configurações em uma lista de várias configurações.

1. Selecione **[!UICONTROL Salvar]**.

## Ativar o encaminhamento de eventos

Em seguida, configure o Edge Network para enviar dados ao encaminhamento de eventos e a outros produtos da Adobe.

1. No **[!UICONTROL Datastreams]** selecione a propriedade que você criou.

1. Selecione Desenvolvimento, Produção ou Ambiente de preparo.

   Ou, para enviar dados a um ambiente de encaminhamento de eventos fora da organização da Adobe, selecione **[!UICONTROL Alternar para o modo avançado]** e cole uma ID. A ID é fornecida quando você cria uma propriedade de encaminhamento de eventos.

1. Ative as ferramentas necessárias e configure conforme necessário.

   * A Adobe Analytics exige uma ID de conjunto de relatórios.

   * O encaminhamento de eventos na Adobe Experience Platform exige uma ID de propriedade e uma ID de ambiente. Esse é o caminho de publicação da propriedade de encaminhamento de eventos.

Depois de configurar, anote as IDs de ambiente para a nova propriedade.

## Configure a extensão SDK da Web da Platform para enviar dados ao fluxo de dados criado anteriormente

Crie sua propriedade no **[!UICONTROL Tags]** espaço de trabalho e navegue até **[!UICONTROL Extensões]** e selecione a extensão SDK da Web do Experience Platform no catálogo para configurá-la e instalá-la.

Consulte a [Documentação da extensão SDK da Web](../../extensions/client/web-sdk/overview.md) para obter detalhes sobre as opções de configuração.

## Criar uma regra de tag para enviar dados ao SDK da Web da Platform

Depois que tudo estiver configurado, crie definições de dados, regras e assim por diante, que usam encaminhamento de eventos e tags, mas que só precisam de uma única solicitação da página.

Crie uma regra de carregamento de página usando a extensão SDK da Web da plataforma e o tipo de ação &quot;Enviar evento&quot;:

1. Abra a guia **[!UICONTROL Regras]** e selecione **[!UICONTROL Criar nova regra]**.

1. Atribua um nome à regra.

1. Selecione **[!UICONTROL Adicionar eventos]**.

1. Adicione um evento escolhendo uma extensão e um dos tipos de eventos disponíveis para essa extensão e, em seguida, defina as configurações para o evento. Por exemplo, selecione **[!UICONTROL Principal - Janela carregada]**.

1. Adicione uma ação usando a extensão SDK da Web da plataforma. Selecione **[!UICONTROL Enviar evento]** na lista **[!UICONTROL Tipo de ação]**, selecione a instância desejada (instância do Alloy configurada anteriormente) e, em seguida, selecione um elemento de dados para adicionar ao bloco de dados XDM dentro da ocorrência do Alloy.

1. Deixe o restante das configurações como padrão para este exemplo e selecione **[!UICONTROL Salvar]**.

Em outro exemplo, você pode criar uma regra que enviará a camada de dados para o Edge se o usuário passar o mouse sobre um botão especificado.

## Resumo

Com os itens a seguir preparados, agora é possível criar regras de encaminhamento de eventos para encaminhar dados a destinos que não são da Adobe.

* Esquema do Experience Data Model (Anote o nome que você deu a ele.)
* Uma propriedade de encaminhamento de eventos (mantenha o controle da ID de propriedade e das IDs de ambiente).
* Um fluxo de dados (observe a ID de ambiente, que não deve ser confundida com a ID de ambiente do encaminhamento de eventos).
* Uma propriedade de tag

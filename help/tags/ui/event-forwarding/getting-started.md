---
title: Introdução ao encaminhamento de eventos
description: Siga este tutorial passo a passo para começar a usar o encaminhamento de eventos no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 46%

---

# Introdução ao encaminhamento de eventos

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Para usar o encaminhamento de eventos no Adobe Experience Platform, os dados devem ser enviados para a Rede de borda da Adobe Experience Platform usando uma ou mais das três opções a seguir:

* [SDK da Web da Adobe Experience Platform](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [API servidor para servidor](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>O SDK da Web da plataforma e o SDK móvel da plataforma não exigem implantação por meio de tags no Adobe Experience Platform. No entanto, usar tags para implantar esses SDKs é a abordagem recomendada.

Depois de enviar dados para a rede de borda, você pode alternar entre as soluções da Adobe para enviar dados para lá. Para enviar dados para uma solução que não seja o Adobe, configure-os no encaminhamento de eventos.

## Pré-requisitos

* Adobe Experience Platform Collection Enterprise (Entre em contato com seu gerente de conta para obter preços)
* Encaminhamento de eventos no Adobe Experience Platform
* SDK da Web ou móvel da Adobe Experience Platform, configurado para enviar dados para a rede de borda
* Mapear dados para o Experience Data Model (XDM) (esse mapeamento pode ser feito usando tags)

## Criar um esquema do XDM

Na Adobe Experience Platform, crie seu esquema.

1. Crie um esquema selecionando **[!UICONTROL Esquemas]** > **[!UICONTROL Criar esquema]** e escolhendo a opção **[!UICONTROL XDM ExperienceEvent]**.

1. Dê um nome e uma breve descrição ao esquema.

1. Você pode adicionar o grupo de campos &quot;Detalhes da Web do ExperienceEvent&quot; selecionando **[!UICONTROL Adicionar]** ao lado de **[!UICONTROL Grupos de Campo]**.

   >[!NOTE]
   >
   >Vários grupos de campos podem ser adicionados, se desejado.

1. Salve o esquema e anote o nome que você deu a ele.

Para obter mais informações sobre esquemas, consulte [Ajuda do sistema do Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

## Criar uma propriedade de encaminhamento de evento

Na interface do usuário da coleta de dados, crie uma propriedade do tipo &quot;Edge&quot;.

1. Selecione **[!UICONTROL Nova propriedade]**.

1. Nomeie a propriedade.

1. Escolha o tipo de plataforma &quot;Borda&quot;.

1. Selecione **[!UICONTROL Salvar]**.

Depois de criar a propriedade, vá para a guia **[!UICONTROL Ambientes]** da nova propriedade e
anote as IDs de ambiente. Se a Organização do Adobe usada no datastream for diferente da Organização do Adobe usada no encaminhamento de eventos, você poderá copiar a ID do ambiente da guia **[!UICONTROL Ambientes]** e colá-la ao criar um datastreamento. Caso contrário, você pode selecionar o ambiente em um menu suspenso.

## Criar um conjunto de dados

Para criar seu armazenamento de dados no Adobe Experience Platform, use a ID de ambiente gerada ao criar a propriedade de encaminhamento de eventos.

1. Use o link no painel à esquerda da interface do usuário da Coleta de dados para abrir a interface dos conjuntos de dados.

1. Selecione **[!UICONTROL Datastreams]**.

1. Nomeie a configuração e forneça uma descrição opcional.
A descrição ajuda a identificar configurações em uma lista de várias configurações.

1. Selecione **[!UICONTROL Salvar]**.



## Ativar encaminhamento de eventos

Em seguida, configure a Edge Network para enviar dados para o encaminhamento do evento e para outros produtos do Adobe.

1. Na interface do usuário do datastreams, selecione a propriedade criada.

1. Selecione Desenvolvimento, Produção ou Ambiente de preparo.

   Ou, para enviar dados para um ambiente de encaminhamento de eventos fora da organização do Adobe, selecione **[!UICONTROL Alternar para o modo avançado]** e cole em uma ID. A ID é fornecida ao criar uma propriedade de encaminhamento de evento.

1. Ative as ferramentas necessárias e configure conforme necessário.

   * A Adobe Analytics exige uma ID de conjunto de relatórios.

   * O encaminhamento de eventos no Adobe Experience Platform exige uma ID de propriedade e uma ID de ambiente. Esse é o caminho de publicação da propriedade de encaminhamento do evento.

Depois de configurar, anote as IDs de ambiente para a nova propriedade.

## Configure a extensão SDK da Web da tag para enviar dados para o armazenamento de dados criado anteriormente

Crie sua propriedade na interface do usuário da Coleta de dados, em seguida, use a extensão Adobe Experience Platform Web SDK para configurá-la.

1. Nomeie a propriedade.

   Você pode ter várias instâncias do Alloy. Por exemplo, você pode ter diferentes propriedades de rastreamento antes e depois do acesso pago.

1. Selecione a ID da organização.

1. Selecione o Domínio de borda.

Consulte a [documentação da extensão SDK da Web](../../extensions/web/sdk/overview.md) para obter mais opções de configuração.

## Criar uma regra de tag para enviar dados para o SDK da Web da plataforma

Depois que o acima estiver em vigor, crie definições de dados, regras e assim por diante, que utilizem o encaminhamento de eventos e tags , mas precisem apenas de uma única solicitação da página.

Crie uma nova regra de carregamento de página usando a extensão SDK da Web da plataforma e o tipo de ação &quot;Enviar evento&quot;:

1. Abra a guia **[!UICONTROL Regras]** e selecione **[!UICONTROL Criar nova regra]**.

1. Atribua um nome à regra.

1. Selecione **[!UICONTROL Adicionar eventos]**.

1. Adicione um evento escolhendo uma extensão e um dos tipos de eventos disponíveis para essa extensão e, em seguida, defina as configurações para o evento. Por exemplo, selecione **[!UICONTROL Principal - Janela carregada]**.

1. Adicione uma ação usando a extensão SDK da Web da plataforma. Selecione **[!UICONTROL Enviar evento]** na lista **[!UICONTROL Tipo de ação]**, selecione a instância desejada (instância do Alloy configurada anteriormente) e, em seguida, selecione um elemento de dados para adicionar ao bloco de dados XDM dentro da ocorrência do Alloy.

1. Deixe o restante das configurações como padrão para este exemplo e selecione **[!UICONTROL Salvar]**.

Em outro exemplo, você pode criar uma regra que enviará a camada de dados para o Edge se o usuário passar o mouse sobre um botão especificado.

## Resumo

Com o seguinte em vigor, agora você pode criar regras de encaminhamento de eventos para encaminhar dados para destinos que não sejam Adobe.

* Esquema do Experience Data Model (Anote o nome que você deu a ele.)
* Uma propriedade de encaminhamento de evento (rastreie a ID de propriedade e as IDs de ambiente).
* Um armazenamento de dados (observe a ID do ambiente, para não ser confundido com a ID do ambiente do encaminhamento do evento).
* Uma propriedade de tag

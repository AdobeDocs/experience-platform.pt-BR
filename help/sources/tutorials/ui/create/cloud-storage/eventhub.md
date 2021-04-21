---
keywords: Experience Platform, home, tópicos populares, Hubs de eventos do Azure, Hubs de eventos, Hubs de eventos do azure
solution: Experience Platform
title: Criar uma conexão de origem de Hubs de Eventos do Azure na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Hubs de Eventos do Azure usando a interface do usuário do Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Event Hubs] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Azure Event Hubs] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para autenticar um conector de origem [!DNL Azure Event Hubs] (a seguir chamado &quot;[!DNL Event Hubs]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Event Hubs], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/streaming/cloud-storage-streaming.md).

### Obter credenciais necessárias

Para autenticar seu conector de origem [!DNL Event Hubs], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `sasKey` | A assinatura de acesso compartilhado gerada. |
| `namespace` | O namespace do [!DNL Event Hubs] que você está acessando. |

Para obter mais informações sobre esses valores, consulte [this [!DNL Event Hubs] document](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Conecte sua conta [!DNL Event Hubs]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Event Hubs] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A guia **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Cloud Storage]**, selecione **[!UICONTROL Azure Event Hubs]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector de Hubs de eventos.

![](../../../../images/tutorials/create/eventhub/catalog.png)

A caixa de diálogo **[!UICONTROL Connect to Azure Event Hubs]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New Account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Event Hubs]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/eventhub/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Event Hubs] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Próximas etapas

Ao seguir este tutorial, você conectou sua conta [!DNL Event Hubs] a [!DNL Platform]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento de nuvem para [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).

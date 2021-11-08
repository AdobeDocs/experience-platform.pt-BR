---
keywords: Experience Platform, home, tópicos populares, Hubs de eventos do Azure, Hubs de eventos, Hubs de eventos do azure
solution: Experience Platform
title: Criar uma conexão de origem de Hubs de Eventos do Azure na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Hubs de Eventos do Azure usando a interface do usuário do Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 855b6414981c6d7ee79bc674e5a4087dd79dde5b
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Crie um [!DNL Azure Event Hubs] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para a autenticação de um [!DNL Azure Event Hubs] (a seguir designado por &quot;[!DNL Event Hubs]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Event Hubs] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/streaming/cloud-storage-streaming.md).

### Obter credenciais necessárias

Para autenticar seu [!DNL Event Hubs] conector de origem, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `sasKey` | A chave primária do [!DNL Event Hubs] namespace. O `sasPolicy` que `sasKey` corresponde a deve ter `manage` direitos configurados para [!DNL Event Hubs] lista a ser preenchida. |
| `namespace` | O namespace do [!DNL Event Hubs] você está acessando. |

Para obter mais informações sobre esses valores, consulte [this [!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Conecte seu [!DNL Event Hubs] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Event Hubs] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** A guia exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Armazenamento na nuvem]** categoria , selecione **[!UICONTROL Hubs de Eventos do Azure]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector de Hubs de evento.

![](../../../../images/tutorials/create/eventhub/catalog.png)

O **[!UICONTROL Conectar-se aos Hubs de Eventos do Azure]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Event Hubs] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/eventhub/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Event Hubs] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Próximas etapas

Ao seguir este tutorial, você conectou seu [!DNL Event Hubs] para [!DNL Platform]. Agora você pode continuar para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento na nuvem para [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).

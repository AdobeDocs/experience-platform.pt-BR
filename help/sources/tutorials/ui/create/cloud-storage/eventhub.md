---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem de Hubs de Evento do Azure na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# Criar um conector [!DNL Azure Event Hubs] de origem na interface do usuário

>[!NOTE]
> O [!DNL Azure Event Hubs] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um conector de origem [!DNL Azure Event Hubs] (a seguir denominado &quot;[!DNL Event Hubs]&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Event Hubs] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/streaming/cloud-storage.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector [!DNL Event Hubs] de origem, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `sasKey` | A assinatura de acesso compartilhado gerada. |
| `namespace` | A namespace do [!DNL Event Hubs] que você está acessando. |

Para obter mais informações sobre esses valores, consulte [ [!DNL Event Hubs] este documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Conectar sua [!DNL Event Hubs] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Event Hubs] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A guia **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria do Armazenamento **[!UICONTROL da]** nuvem, selecione Hubs **[!UICONTROL do Evento]** do Azure. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector de Hubs de Evento.

![](../../../../images/tutorials/create/eventhub/catalog.png)

A caixa de diálogo **[!UICONTROL Conectar-se aos Hubs]** de Eventos do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Event Hubs] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/eventhub/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Event Hubs] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Próximas etapas

Ao seguir este tutorial, você conectou sua [!DNL Event Hubs] conta a [!DNL Platform]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para [!DNL Platform]](../../dataflow/streaming/cloud-storage.md)dentro.
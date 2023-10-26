---
title: Criar uma conexão de origem dos Hubs de eventos do Azure na interface
description: Saiba como criar uma conexão de origem do Azure Event Hubs usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1680cc4e1d5c1576767053a74e560bc2eb8c24cb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# Criar um [!DNL Azure Event Hubs] conexão de origem na interface

>[!IMPORTANT]
>
>A variável [!DNL Azure Event Hubs] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Este tutorial fornece etapas para criar um [!DNL Azure Event Hubs] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Event Hubs] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/streaming/cloud-storage-streaming.md).

### Coletar credenciais necessárias

Para autenticar seu [!DNL Event Hubs] conector de origem, você deve fornecer valores para as seguintes propriedades de conexão:

>[!BEGINTABS]

>[!TAB Autenticação padrão]

| Credencial | Descrição |
| --- | --- |
| Nome da chave SAS | O nome da regra de autorização, que também é conhecido como o nome da chave SAS. |
| Chave SAS | A chave primária do [!DNL Event Hubs] namespace. A variável `sasPolicy` que o `sasKey` corresponde a deve ter `manage` direitos configurados para a variável [!DNL Event Hubs] lista a ser preenchida. |
| Namespace | O namespace do [!DNL Event Hubs] que você está acessando. Um [!DNL Event Hubs] O namespace fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |

>[!TAB Autenticação SAS]

| Credencial | Descrição |
| --- | --- |
| Nome da chave SAS | O nome da regra de autorização, que também é conhecido como o nome da chave SAS. |
| Chave SAS | A chave primária do [!DNL Event Hubs] namespace. A variável `sasPolicy` que o `sasKey` corresponde a deve ter `manage` direitos configurados para a variável [!DNL Event Hubs] lista a ser preenchida. |
| Namespace | O namespace do [!DNL Event Hubs] que você está acessando. Um [!DNL Event Hubs] O namespace fornece um contêiner de escopo exclusivo, no qual você pode criar um ou mais [!DNL Event Hubs]. |
| Nome do Hub de Eventos | O nome do seu [!DNL Event Hubs] origem. |

>[!ENDTABS]

Para obter mais informações sobre esses valores, consulte [este documento de Hubs de Eventos](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Event Hubs] conta para Experience Platform.

## Conecte seu [!DNL Event Hubs] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL Hubs de Eventos do Azure]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com os Hubs de Eventos do Azure selecionados.](../../../../images/tutorials/create/eventhub/catalog.png)

A variável **[!UICONTROL Conectar-se aos Hubs de Eventos do Azure]** será exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Event Hubs] conta que deseja usar e selecione **[!UICONTROL Próxima]** para continuar.

![Uma lista de contas de origem dos Hubs de Eventos do Azure existentes.](../../../../images/tutorials/create/eventhub/existing.png)

### Nova conta

>[!TIP]
>
>Depois de criado, não é possível alterar o tipo de autenticação de um [!DNL Event Hubs] conexão básica. Para alterar o tipo de autenticação, você deve criar uma nova conexão base.

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL Event Hubs] conta.

![A nova interface de criação de conta para os Hubs de Eventos do Azure.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Autenticação padrão]

Para criar uma [!DNL Event Hubs] conta com autenticação padrão, selecione **[!UICONTROL Autenticação padrão]** e forneça valores para o [!UICONTROL Nome da chave SAS], [!UICONTROL Chave SAS], e [!UICONTROL Namespace].

Depois de inserir suas credenciais de autenticação, selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação padrão para os Hubs de Eventos do Azure.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB Autenticação SAS]

Para criar uma [!DNL Event Hubs] com autenticação SAS, selecione **[!UICONTROL Autenticação SAS]** e forneça valores para o [!UICONTROL Nome da chave SAS], [!UICONTROL Chave SAS], [!UICONTROL Namespace], e [!UICONTROL Nome dos Hubs de Eventos].

Depois de inserir suas credenciais de autenticação, selecione **[!UICONTROL Conectar à origem]**.

![A interface de autenticação SAS para os Hubs de Eventos do Azure.](../../../../images/tutorials/create/eventhub/sas.png)

>[!ENDTABS]


## Próximas etapas

Ao seguir este tutorial, você conectou o [!DNL Event Hubs] conta para Experience Platform. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento em nuvem para o Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).

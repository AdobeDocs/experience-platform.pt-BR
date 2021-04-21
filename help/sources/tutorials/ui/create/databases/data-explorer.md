---
keywords: Experience Platform, home, tópicos populares, Data Explorer do Azure, explorador de dados do azure, explorador de dados, Data Explorer
solution: Experience Platform
title: Criar uma conexão de origem de Data Explorer do Azure na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Azure Data Explorer usando a interface do usuário do Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Data Explorer] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Azure Data Explorer] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Azure Data Explorer] (a seguir chamado &quot;[!DNL Data Explorer]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Data Explorer], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar sua conta [!DNL Data Explorer] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O endpoint do servidor [!DNL Data Explorer]. |
| `database` | O nome do banco de dados [!DNL Data Explorer]. |
| `tenant` | A ID de locatário exclusiva usada para se conectar ao banco de dados [!DNL Data Explorer]. |
| `servicePrincipalId` | A ID da entidade de serviço exclusiva usada para se conectar ao banco de dados [!DNL Data Explorer]. |
| `servicePrincipalKey` | A chave principal de serviço exclusiva usada para se conectar ao banco de dados [!DNL Data Explorer]. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Conecte sua conta [!DNL Azure Data Explorer]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Data Explorer] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes nas quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Azure Data Explorer]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector do Data Explorer.

![catálogo](../../../../images/tutorials/create/data-explorer/catalog.png)

A página **[!UICONTROL Connect to Azure Data Explorer]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Data Explorer]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Data Explorer] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/data-explorer/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Data Explorer]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).

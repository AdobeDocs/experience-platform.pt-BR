---
keywords: Experience Platform, home, tópicos populares, Azure Data Lake Storage Gen2, ADLS Gen2, adls gen2, conector adls
solution: Experience Platform
title: Criar uma conexão de origem Gen2 do Armazenamento do Azure Data Lake na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem Gen2 do Armazenamento do Azure Data Lake usando a interface do usuário do Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Data Lake Storage Gen2] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para autenticar um conector de origem [!DNL Azure Data Lake Storage Gen2] (a seguir chamado &quot;[!DNL ADLS Gen2]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão ADLS Gen2 válida, poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Obter credenciais necessárias

Para autenticar seu conector de origem [!DNL ADLS Gen2], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O endpoint para [!DNL ADLS Gen2]. |
| `servicePrincipalId` | A ID de cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações do locatário que contêm seu aplicativo. |

Para obter mais informações sobre esses valores, consulte [this [!DNL ADLS Gen2] document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Conecte sua conta [!DNL ADLS Gen2]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL ADLS Gen2] para se conectar a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Azure Data Lake Gen2]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

A caixa de diálogo **[!UICONTROL Connect to Azure Data Lake Gen2]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New Account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL ADLS Gen2]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL ADLS Gen2] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL ADLS Gen2]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento de nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md).

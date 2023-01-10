---
keywords: Experience Platform, home, tópicos populares, Azure Data Lake Storage Gen2, ADLS Gen2, adls gen2, conector adls
solution: Experience Platform
title: Criar uma conexão de origem Gen2 do Armazenamento do Azure Data Lake na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem Gen2 do Armazenamento do Azure Data Lake usando a interface do usuário do Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Crie um [!DNL Azure Data Lake Storage Gen2] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para a autenticação de um [!DNL Azure Data Lake Storage Gen2] (a seguir designado por &quot;[!DNL ADLS Gen2]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se já tiver uma conexão ADLS Gen2 válida, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Obter credenciais necessárias

Para autenticar seu [!DNL ADLS Gen2] conector de origem, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O terminal para [!DNL ADLS Gen2]. |
| `servicePrincipalId` | A ID de cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações do locatário que contêm seu aplicativo. |

Para obter mais informações sobre esses valores, consulte [this [!DNL ADLS Gen2] documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Conecte seu [!DNL ADLS Gen2] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL ADLS Gen2] conta à qual se conectar [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Azure Data Lake Gen2]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

O **[!UICONTROL Conecte-se ao Azure Data Lake Gen2]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL ADLS Gen2] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL ADLS Gen2] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL ADLS Gen2] conta. Agora você pode continuar para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento na nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md).

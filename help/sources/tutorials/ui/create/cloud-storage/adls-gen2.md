---
keywords: Experience Platform;página inicial;tópicos populares;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls connector
solution: Experience Platform
title: Criar uma Conexão Source Gen2 do Armazenamento Azure Data Lake na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem Gen2 do Armazenamento Azure Data Lake usando a interface do usuário do Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Data Lake Storage Gen2] na interface

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para autenticar um conector de origem [!DNL Azure Data Lake Storage Gen2] (a seguir denominado &quot;[!DNL ADLS Gen2]&quot;) usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão ADLS Gen2 válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para autenticar o conector de origem do [!DNL ADLS Gen2], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O ponto de extremidade para [!DNL ADLS Gen2]. |
| `servicePrincipalId` | A ID do cliente do aplicativo. |
| `servicePrincipalKey` | A chave do aplicativo. |
| `tenant` | As informações de locatário que contêm seu aplicativo. |

Para obter mais informações sobre esses valores, consulte [este [!DNL ADLS Gen2] documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Conectar sua conta do [!DNL ADLS Gen2]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL ADLS Gen2] e conectar-se ao [!DNL Experience Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Azure Data Lake Gen2]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

A caixa de diálogo **[!UICONTROL Conectar-se ao Azure Data Lake Gen2]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL ADLS Gen2]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL ADLS Gen2] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL ADLS Gen2]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento na nuvem para o  [!DNL Experience Platform]](../../dataflow/batch/cloud-storage.md).

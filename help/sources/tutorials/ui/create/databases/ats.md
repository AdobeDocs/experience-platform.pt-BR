---
keywords: Experience Platform;home;popular topics;Azure Table Storage;azure table storage;ats;ATS
solution: Experience Platform
title: Criar um conector de origem do Armazenamento de Tabela do Azure na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem do Armazenamento de Tabela do Azure (a seguir denominado "ATS") usando a interface de usuário da Plataforma.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---


# Criar um conector [!DNL Azure Table Storage] de origem na interface do usuário

>[!NOTE]
>
>O [!DNL Azure Table Storage] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Azure Table Storage] (a seguir denominado &quot;ATS&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão ATS válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta ATS em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma string de conexão para se conectar à sua [!DNL Azure Table Storage] instância. A cadeia de conexão para conexão com a instância ATS. O padrão da string de conexão para ATS é `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obter mais informações sobre a introdução, consulte [ [!DNL Azure Table Storage] este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Conectar sua [!DNL Azure Table Storage] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular a conta ATS à [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de Dados, selecione **[!UICONTROL Armazenamento]** de Tabela do Azure. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector ATS.

![catálogo](../../../../images/tutorials/create/ats/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento]** de tabela do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais ATS. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/ats/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta ATS à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/ats/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta ATS. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/databases.md)os dados para o
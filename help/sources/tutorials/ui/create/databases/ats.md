---
keywords: Experience Platform, home, tópicos populares, Armazenamento de tabela do Azure, armazenamento de tabela do azure, ats, ATS
solution: Experience Platform
title: Criar uma Conexão de Origem de Armazenamento de Tabela do Azure na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Armazenamento de Tabela do Azure usando a interface do usuário do Adobe Experience Platform.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Azure Table Storage] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Azure Table Storage] (a seguir denominado &quot;ATS&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão ATS válida, ignore o restante deste documento e prossiga para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar sua conta ATS em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | Uma string de conexão para se conectar à instância [!DNL Azure Table Storage]. A string de conexão a ser conectada à instância ATS. O padrão da string de conexão para ATS é `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Conecte sua conta [!DNL Azure Table Storage]

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular sua conta ATS a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos de Dados]**, selecione **[!UICONTROL Armazenamento de Tabela do Azure]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector ATS.

![catálogo](../../../../images/tutorials/create/ats/catalog.png)

A página **[!UICONTROL Conectar-se ao Armazenamento de Tabela do Azure]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais ATS. Quando terminar, selecione **[!UICONTROL Connect]** e deixe algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/ats/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta ATS à qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/ats/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta ATS. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).

---
keywords: Experience Platform, home, tópicos populares, Salesforce, salesforce
solution: Experience Platform
title: Criar uma conexão de origem do Salesforce na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Salesforce usando a interface do usuário do Adobe Experience Platform.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Salesforce] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de CRM de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Salesforce] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida [!DNL Salesforce], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/crm.md).

### Obter credenciais necessárias

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL da instância de origem [!DNL Salesforce]. |
| `username` | O nome de usuário da conta de usuário [!DNL Salesforce]. |
| `password` | A senha da conta de usuário [!DNL Salesforce]. |
| `securityToken` | O token de segurança para a conta de usuário [!DNL Salesforce]. |

Para obter mais informações sobre a introdução, consulte [este documento do Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## Conecte sua conta [!DNL Salesforce]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Salesforce] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Salesforce]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector do Salesforce.

![catálogo](../../../../images/tutorials/create/salesforce/catalog.png)

A página **[!UICONTROL Connect to Salesforce]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Salesforce]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Salesforce] com a qual deseja se conectar e selecione **[!UICONTROL Next]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/salesforce/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Salesforce]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/crm.md).

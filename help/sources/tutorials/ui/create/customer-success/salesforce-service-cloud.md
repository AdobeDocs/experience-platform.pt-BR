---
keywords: Experience Platform, home, tópicos populares, Salesforce Service Cloud, salesforce service cloud
solution: Experience Platform
title: Criar uma conexão de origem da nuvem do Salesforce Service na interface do usuário
topic: visão geral
type: Tutorial
description: Saiba como criar uma conexão de origem do Salesforce Service Cloud usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a0b016e8adc519bc79701f9fd850b6ddf7d46127
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Salesforce Service Cloud] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Salesforce Service Cloud] (a seguir chamado &quot;SSC&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão SSC válida, poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/customer-success.md)

### Obter credenciais necessárias

Para acessar sua conta SSC em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da conta de usuário. |
| `password` | A senha da conta de usuário. |
| `securityToken` | O token de segurança da conta do usuário. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Salesforce Service Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Conecte sua conta [!DNL Salesforce Service Cloud]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta do SSC a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Customer Success]**, selecione **[!UICONTROL Salesforce Service Cloud]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector SSC.

![catálogo](../../../../images/tutorials/create/ssc/catalog.png)

A página **[!UICONTROL Connect to Salesforce Service Cloud]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do SSC. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta SSC à qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do SSC. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de Sucesso do cliente para [!DNL Platform]](../../dataflow/customer-success.md).
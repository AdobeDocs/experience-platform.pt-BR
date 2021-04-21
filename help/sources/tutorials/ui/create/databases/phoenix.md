---
keywords: Experience Platform, home, tópicos populares, Phoenix, phonix
solution: Experience Platform
title: Criar uma conexão de origem Phoenix na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem Phoenix usando a interface do usuário do Adobe Experience Platform.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Criar uma conexão de origem [!DNL Phoenix] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Phoenix] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Phoenix] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Phoenix], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md)

### Obter credenciais necessárias

Para acessar sua conta [!DNL Phoenix] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do servidor [!DNL Phoenix]. |
| `port` | A porta TCP que o servidor [!DNL Phoenix] usa para detectar as conexões do cliente. Se você se conectar a [!DNL Azure HDInsights], especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao servidor [!DNL Phoenix]. Especifique /hbasephonix0 se estiver usando o cluster [!DNL Azure HDInsights]. |
| `username` | O nome de usuário usado para acessar o servidor [!DNL Phoenix]. |
| `password` | A senha que corresponde ao usuário. |
| `enableSsl` | Um botão que especifica se as conexões com o servidor são criptografadas usando SSL. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Phoenix] document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Conecte sua conta [!DNL Phoenix]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Phoenix] para se conectar a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Phoenix]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar uma nova conta [!DNL Phoenix].

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

A página **[!UICONTROL Connect to Phoenix]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Phoenix]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Phoenix] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Phoenix]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).

---
keywords: Experience Platform, home, tópicos populares, mysql, MySQL
solution: Experience Platform
title: Criar uma conexão de origem MySQL na interface do usuário
topic: visão geral
type: Tutorial
description: Saiba como criar uma conexão de origem MySQL usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 8851e11e956b393e56714d4d48870b7f68947c18
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL MySQL] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar uma conexão de origem [!DNL MySQL] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL MySQL], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar sua conta [!DNL MySQL] em [!DNL Platform], você deve fornecer o seguinte valor:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão [!DNL MySQL] associada à sua conta. O padrão da string de conexão [!DNL MySQL] é: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Você pode saber mais sobre cadeias de conexão e como obtê-las lendo o [[!DNL MySQL] document](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Conecte sua conta [!DNL MySQL]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL MySQL] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL MySQL]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL MySQL].

![](../../../../images/tutorials/create/my-sql/catalog.png)

A página **[!UICONTROL Connect to MySQL]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL MySQL]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/my-sql/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL MySQL] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do MySQL . Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
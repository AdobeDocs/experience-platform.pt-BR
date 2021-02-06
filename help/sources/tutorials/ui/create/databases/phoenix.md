---
keywords: Experience Platform;casa;tópicos populares;Phoenix;phonix;home;popular topics;Phoenix;phonix
solution: Experience Platform
title: Criar uma conexão de origem Phoenix na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem Phoenix usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# Criar uma conexão de origem [!DNL Phoenix] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Phoenix] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de origem [!DNL Phoenix] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Phoenix], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md)

### Reunir credenciais obrigatórias

Para acessar sua conta [!DNL Phoenix] em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou nome do host do servidor [!DNL Phoenix]. |
| `port` | A porta TCP que o servidor [!DNL Phoenix] usa para escutar as conexões do cliente. Se você se conectar a [!DNL Azure HDInsights], especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao servidor [!DNL Phoenix]. Especifique /hbasephonix0 se estiver usando o cluster [!DNL Azure HDInsights]. |
| `username` | O nome de usuário que você usa para acessar o servidor [!DNL Phoenix]. |
| `password` | A senha que corresponde ao usuário. |
| `enableSsl` | Uma alternância que especifica se as conexões com o servidor são criptografadas usando SSL. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Conectar sua conta [!DNL Phoenix]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Phoenix] para se conectar a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos de Dados]**, selecione **[!UICONTROL Phoenix]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar uma nova conta [!DNL Phoenix].

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

A página **[!UICONTROL Conectar-se a Phoenix]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Phoenix]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Phoenix] com a qual você deseja se conectar e selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Phoenix]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
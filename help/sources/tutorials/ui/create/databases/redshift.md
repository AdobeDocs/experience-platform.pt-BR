---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Amazon Redshift na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Criar um conector [!DNL Amazon Redshift] de origem na interface do usuário

>As seleções de menu [!NOTE]
>O [!DNL Amazon Redshift] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Amazon Redshift] (a seguir denominado &quot;[!DNL Redshift]&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Redshift] básica, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua [!DNL Redshift] conta em [!DNL Platform], forneça os seguintes valores:

| **Credencial** | **Descrição** |
| -------------- | --------------- |
| `server` | O servidor associado à sua [!DNL Redshift] conta. |
| `username` | O nome de usuário associado à sua [!DNL Redshift] conta. |
| `password` | A senha associada à sua [!DNL Redshift] conta. |
| `database` | O [!DNL Redshift] banco de dados que você está acessando. |

Para obter mais informações sobre a introdução, consulte [este documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)Redshift.

## Conectar sua [!DNL Redshift] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua [!DNL Redshift] conta [!DNL Platform].

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL Amazon Redshift]** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão básica de entrada, selecione Origem **[!UICONTROL do]** Connect.

![](../../../../images/tutorials/create/redshift/catalog.png)

A página *[!UICONTROL Conectar-se ao Amazon Redshift]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Redshift] credenciais à conexão básica. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![](../../../../images/tutorials/create/redshift/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Redshift] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/redshift/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua [!DNL Redshift] conta. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Platform](../../dataflow/databases.md).
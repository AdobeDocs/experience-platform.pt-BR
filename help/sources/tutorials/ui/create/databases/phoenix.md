---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem Phoenix na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Criar um conector [!DNL Phoenix] de origem na interface do usuário

>[!NOTE]
> O [!DNL Phoenix] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL Phoenix] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Phoenix] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md)

### Reunir credenciais obrigatórias

Para acessar sua [!DNL Phoenix] conta em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do [!DNL Phoenix] servidor. |
| `port` | A porta TCP que o [!DNL Phoenix] servidor usa para escutar as conexões do cliente. Se você se conectar a [!DNL Azure HDInsights], especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao [!DNL Phoenix] servidor. Especifique /hbasephonix0 se estiver usando o [!DNL Azure HDInsights] cluster. |
| `username` | O nome de usuário que você usa para acessar o [!DNL Phoenix] servidor. |
| `password` | A senha que corresponde ao usuário. |
| `enableSsl` | Uma alternância que especifica se as conexões com o servidor são criptografadas usando SSL. |

Para obter mais informações sobre como começar, consulte [este documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

## Conecte sua conta Phoenix

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova [!DNL Phoenix] conta à qual se conectar [!DNL Platform].

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes para as quais você pode criar uma conta de entrada, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL Phoenix]** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de entrada, selecione Origem **[!UICONTROL do]** Connect.

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

A página *[!UICONTROL Conectar-se a Phoenix]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas [!DNL Phoenix] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Phoenix] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL Phoenix] conta. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Platform](../../dataflow/databases.md).
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Google Big Query na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Criar um conector [!DNL Google Big Query] de origem na interface do usuário

>[!NOTE]
> O [!DNL Google BigQuery] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Google Big Query] (a seguir denominado &quot;GBQ&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica GBQ, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta GBQ em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | A ID do projeto padrão para o [!DNL BigQuery] query. |
| `clientID` | O valor da ID usado para gerar o token de atualização. |
| `clientSecret` | O valor secreto usado para gerar o token de atualização. |
| `refreshToken` | O token de atualização obtido do [!DNL Google] usado para autorizar o acesso ao [!DNL BigQuery]. |

Para obter mais informações sobre esses valores, consulte [este documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)GBQ.

## Conecte sua conta GBQ

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular a sua conta GBQ à [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL Google Big Query]** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de base de entrada, selecione **[!UICONTROL Adicionar dados]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

A página *[!UICONTROL Conectar-se ao Google Big Query]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais de GBQ à conexão básica. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GBQ com a qual deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta GBQ. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).
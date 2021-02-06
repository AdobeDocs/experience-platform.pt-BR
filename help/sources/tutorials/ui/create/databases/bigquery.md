---
keywords: Experience Platform;home;popular tópicos;Google Big Query;google big query;GBQ;gbq;;home;popular topics;Google Big ;GBQ;gbq
solution: Experience Platform
title: Criar uma conexão de fonte do Google Big Query na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão fonte do Google Big Query usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# Criar uma conexão de origem [!DNL Google Big Query] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Google BigQuery] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Google Big Query] (a seguir denominado &quot;BigQuery&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão BigQuery válida, poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta BigQuery em [!DNL Platform], você deve fornecer os seguintes valores de autenticação OAuth 2.0:

| Credencial | Descrição |
| ---------- | ----------- |
| `project` | A ID do projeto padrão [!DNL BigQuery] para o query. |
| `clientID` | O valor da ID usado para gerar o token de atualização. |
| `clientSecret` | O valor secreto usado para gerar o token de atualização. |
| `refreshToken` | O token de atualização obtido de [!DNL Google] usado para autorizar o acesso a [!DNL BigQuery]. |

Para obter mais informações sobre esses valores, consulte [este documento BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Conecte sua conta do Google BigQuery

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta BigQuery a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos de Dados]**, selecione **[!UICONTROL Google Big Query]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector BigQuery.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

A página **[!UICONTROL Conectar-se ao Google Big Query]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do BigQuery. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta BigQuery com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Next]** para continuar.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta GBQ. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
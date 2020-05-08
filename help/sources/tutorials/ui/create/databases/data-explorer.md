---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Azure Data Explorer na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 1fb07723aedcf6dfd49765c10342b70b0a7d24f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Criar um conector de origem do Azure Data Explorer na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Azure Data Explorer (a seguir denominado &quot;Data Explorer&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida com o Data Explorer, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta do Data Explorer na Plataforma, forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O terminal do servidor do Data Explorer. |
| `database` | O nome do banco de dados do Data Explorer. |
| `tenant` | A ID de locatário exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `servicePrincipalId` | A ID de principal de serviço exclusiva usada para conectar-se ao banco de dados do Data Explorer. |
| `servicePrincipalKey` | A chave principal de serviço exclusiva usada para conectar-se ao banco de dados do Data Explorer. |

Para obter mais informações sobre como começar, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)do Data Explorer.

## Conectar sua conta do Azure Data Explorer

Depois de coletar as credenciais necessárias, você pode seguir as etapas abaixo para criar uma nova conta do Data Explorer para se conectar à Plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *[!UICONTROL Catálogo]* exibe várias fontes para as quais você pode criar uma conta de entrada, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de Dados, selecione **[!UICONTROL Azure Data Explorer]** e clique **no ícone + (+)** para criar um novo conector do Data Explorer.

![catálogo](../../../../images/tutorials/create/data-explorer/catalog.png)

A página *[!UICONTROL Conectar-se ao Azure Data Explorer]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do Data Explorer. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do Data Explorer à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/data-explorer/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Data Explorer. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).
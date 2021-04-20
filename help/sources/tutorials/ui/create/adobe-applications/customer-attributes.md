---
keywords: Experience Platform, home, tópicos populares, atributos do cliente
solution: Experience Platform
title: Criar uma conexão de fonte de atributos do cliente na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem na interface do usuário para coletar dados de perfil de atributos do cliente no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---


# Criar uma conexão de origem de Atributos do cliente na interface do usuário

Este tutorial fornece etapas para criar uma conexão de origem na interface do usuário para coletar dados de perfil de Atributos do cliente no Adobe Experience Platform. Para obter mais informações sobre Atributos do cliente, consulte a [Visão geral dos Atributos do cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>No momento, as funcionalidades de desativação, ativação e exclusão de fluxos de dados não são compatíveis com a fonte de atributos do cliente.

## Criar uma conexão de origem

Na interface do usuário da plataforma, selecione **[!UICONTROL Sources]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conexão.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Adobe applications], selecione **[!UICONTROL Customer Attributes]** e selecione **[!UICONTROL Add data]**.

>[!NOTE]
>
>Se você já tiver estabelecido uma conexão de origem para os dados de perfil dos Atributos do cliente, a opção para se conectar à fonte será desativada.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

A tela [!UICONTROL Add data] lista todas as fontes de dados disponíveis para Atributos do cliente. Para criar uma nova conexão, selecione uma fonte de dados na lista e selecione **[!UICONTROL Next]**.

>[!NOTE]
>
>Somente um conjunto de dados pode ser selecionado por conexão de origem dos Atributos do cliente.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

A etapa [!UICONTROL Dataflow detail] é exibida, permitindo nomear e fornecer uma breve descrição para o novo fluxo de dados.

Durante esse processo, também é possível ativar [!UICONTROL Partial ingestion] e [!UICONTROL Error diagnostics]. [!UICONTROL Partial ingestion] O fornece a capacidade de assimilar dados contendo erros, até um determinado limite que pode ser definido, enquanto  [!UICONTROL Error diagnostics] fornece detalhes sobre dados incorretos que são armazenados em lote separadamente. Para obter mais informações, consulte a [visão geral da ingestão parcial de lote](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

A etapa [!UICONTROL Review] é exibida, permitindo que você revise o novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Connection]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas dentro desse arquivo de origem.
* **[!UICONTROL Assign dataset & map fields]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Próximas etapas

Depois que a conexão é criada, um esquema de público-alvo e um conjunto de dados são criados automaticamente para conter os dados recebidos. Quando a assimilação inicial for concluída, os dados de perfil dos atributos do cliente poderão ser usados pelos serviços downstream da plataforma, como [!DNL Real-time Customer Profile] e [!DNL Segmentation Service]. Consulte os seguintes documentos para obter mais detalhes:

* [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
* [[!DNL Segmentation Service] visão geral](../../../../../segmentation/home.md)

---
keywords: Experience Platform;página inicial;tópicos populares;atributos do cliente
solution: Experience Platform
title: Criar uma conexão do Source de atributos do cliente na interface
type: Tutorial
description: Saiba como criar uma conexão de origem na interface do usuário para trazer dados de perfil de atributos do cliente para a Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Criar uma conexão de origem de atributos do cliente na interface

Este tutorial fornece etapas para criar uma conexão de origem na interface do usuário a fim de trazer os dados de perfil dos Atributos do cliente para a Adobe Experience Platform. Para obter mais informações sobre os Atributos do cliente, consulte a [visão geral dos Atributos do cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=pt-BR).

>[!IMPORTANT]
>
>No momento, a fonte de atributos do cliente não é compatível com a ativação ou desativação de fluxos de dados.

## Criar uma conexão de origem

>[!NOTE]
>
>Se você já tiver estabelecido uma conexão de origem para os dados de perfil dos Atributos do cliente, a opção para se conectar com a origem será desativada.

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conexão.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL aplicativos do Adobe], selecione **[!UICONTROL Atributos do cliente]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Selecionar fonte de dados de atributos do cliente

A tela [!UICONTROL Adicionar dados] lista todas as fontes de dados disponíveis para os Atributos do cliente. Somente um conjunto de dados pode ser selecionado por conexão de origem de Atributos do cliente.

>[!NOTE]
>
>Grupos de campos, esquemas e conjuntos de dados são criados prontos para uso como parte do provisionamento de fluxo. Eles permanecerão como estão e você terá que excluí-los manualmente, se necessário.

A evolução do esquema não é aceita pela fonte de atributos do cliente. Se a entrada do esquema de uma fonte de dados de atributos do cliente for alterada, ela se tornará incompatível com o Experience Platform. Como solução alternativa, você pode excluir um fluxo de dados de atributos do cliente existente, juntamente com seu conjunto de dados associado, esquema e grupo de campos e, em seguida, criar um novo com o esquema e a fonte de dados atualizados.

>[!IMPORTANT]
>
>Embora seja possível excluir um fluxo de dados de atributos do cliente, o conjunto de dados correspondente permanecerá mesmo após a exclusão do fluxo de dados. Consulte o guia em [excluindo um conjunto de dados](../../../../../catalog/datasets/user-guide.md) para obter etapas sobre como excluir um conjunto de dados manualmente.

Para criar uma nova conexão, selecione uma fonte de dados na lista e selecione **[!UICONTROL Avançar]**.

![adicionar-dados](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Fornecer detalhes do fluxo de dados

A etapa [!UICONTROL Detalhes do fluxo de dados] é exibida, permitindo que você forneça um nome e uma breve descrição para o fluxo de dados. Durante esse processo, você também pode definir configurações para [!UICONTROL Diagnóstico de erro], [!UICONTROL Assimilação parcial] e [!UICONTROL Alertas].

O [!UICONTROL Diagnóstico de erro] habilita a geração de mensagens de erro detalhadas para todos os registros incorretos que ocorrem no fluxo de dados, enquanto a [!UICONTROL Assimilação parcial] permite assimilar dados que contêm erros, até um determinado limite definido manualmente. Consulte a [visão geral da assimilação parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de fontes usando a interface](../../alerts.md).

Quando terminar de fornecer detalhes ao seu fluxo de dados, selecione **[!UICONTROL Avançar]**.

![detalhes do fluxo de dados](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Revisar fluxo de dados

A etapa [!UICONTROL Revisão] é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir campos de conjunto de dados e mapa]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados pertence.

![avaliação](../../../../images/tutorials/create/customer-attributes/review.png)

## Próximas etapas

Depois que a conexão é criada, um esquema de público-alvo e um conjunto de dados são criados automaticamente para conter os dados recebidos. Quando a assimilação inicial for concluída, os dados do perfil de atributos do cliente poderão ser usados pelos serviços downstream da Experience Platform, como o [!DNL Real-Time Customer Profile] e o [!DNL Segmentation Service]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Visão geral do [!DNL Segmentation Service]](../../../../../segmentation/home.md)

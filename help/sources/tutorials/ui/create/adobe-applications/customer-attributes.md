---
keywords: Experience Platform;página inicial;tópicos populares;atributos do cliente
solution: Experience Platform
title: Criar uma conexão de origem de atributos do cliente na interface
type: Tutorial
description: Saiba como criar uma conexão de origem na interface do usuário para trazer dados de perfil de atributos do cliente para a Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# Criar uma conexão de origem de atributos do cliente na interface

Este tutorial fornece etapas para criar uma conexão de origem na interface do usuário a fim de trazer os dados de perfil dos Atributos do cliente para a Adobe Experience Platform. Para obter mais informações sobre os atributos do cliente, consulte [Visão geral dos atributos do cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=pt-BR).

>[!IMPORTANT]
>
>No momento, a fonte de atributos do cliente não é compatível com a ativação ou desativação de fluxos de dados.

## Criar uma conexão de origem

>[!NOTE]
>
>Se você já tiver estabelecido uma conexão de origem para os dados de perfil dos Atributos do cliente, a opção para se conectar com a origem será desativada.

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conexão.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL aplicativos Adobe] categoria, selecione **[!UICONTROL Atributos do cliente]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Selecionar fonte de dados de atributos do cliente

A variável [!UICONTROL Adicionar dados] A tela lista todas as fontes de dados disponíveis para os Atributos do cliente. Somente um conjunto de dados pode ser selecionado por conexão de origem de Atributos do cliente.

>[!NOTE]
>
>Grupos de campos, esquemas e conjuntos de dados são criados prontos para uso como parte do provisionamento de fluxo. Eles permanecerão como estão e você terá que excluí-los manualmente, se necessário.

A evolução do esquema não é aceita pela fonte de atributos do cliente. Se a entrada do esquema de uma fonte de dados de atributos do cliente for alterada, ela se tornará incompatível com a Platform. Como solução alternativa, você pode excluir um fluxo de dados de atributos do cliente existente, juntamente com seu conjunto de dados associado, esquema e grupo de campos e, em seguida, criar um novo com o esquema e a fonte de dados atualizados.

>[!IMPORTANT]
>
>Embora seja possível excluir um fluxo de dados de atributos do cliente, o conjunto de dados correspondente permanecerá mesmo após a exclusão do fluxo de dados. Consulte o guia sobre [exclusão de um conjunto de dados](../../../../../catalog/datasets/user-guide.md) para obter etapas sobre como excluir manualmente um conjunto de dados.

Para criar uma nova conexão, selecione uma fonte de dados na lista e selecione **[!UICONTROL Próxima]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Fornecer detalhes do fluxo de dados

A variável [!UICONTROL Detalhes do fluxo de dados] é exibida, permitindo que você forneça um nome e uma breve descrição para o fluxo de dados. Durante esse processo, você também pode definir configurações para [!UICONTROL Diagnóstico de erro], [!UICONTROL Assimilação parcial], e [!UICONTROL Alertas].

[!UICONTROL Diagnóstico de erro] permite a geração de mensagens de erro detalhadas para qualquer registro incorreto que ocorra em seu fluxo de dados, enquanto [!UICONTROL Assimilação parcial] O permite assimilar dados que contêm erros, até um determinado limite definido manualmente. Consulte a [visão geral da assimilação parcial de lotes](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de origens usando a interface do usuário](../../alerts.md).

Quando terminar de fornecer detalhes ao seu fluxo de dados, selecione **[!UICONTROL Próxima]**.

![detalhes do fluxo de dados](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Revisar fluxo de dados

A variável [!UICONTROL Revisão] é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

![revisão](../../../../images/tutorials/create/customer-attributes/review.png)

## Próximas etapas

Depois que a conexão é criada, um esquema de público-alvo e um conjunto de dados são criados automaticamente para conter os dados recebidos. Quando a assimilação inicial for concluída, os dados do perfil de atributos do cliente poderão ser usados pelos serviços downstream da plataforma, como [!DNL Real-Time Customer Profile] e [!DNL Segmentation Service]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do [!DNL Real-Time Customer Profile]](../../../../../profile/home.md)
* [Visão geral do [!DNL Segmentation Service]](../../../../../segmentation/home.md)

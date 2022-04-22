---
keywords: Experience Platform, home, tópicos populares, atributos do cliente
solution: Experience Platform
title: Criar uma conexão de fonte de atributos do cliente na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem na interface do usuário para trazer os dados de perfil dos atributos do cliente para o Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: b1b820c93ff1731b797f2b5e3ace7d2d6995b98b
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# Criar uma conexão de origem de Atributos do cliente na interface do usuário

Este tutorial fornece etapas para criar uma conexão de origem na interface do usuário para trazer os dados de perfil dos Atributos do cliente para o Adobe Experience Platform. Para obter mais informações sobre atributos do cliente, consulte [Visão geral dos atributos do cliente](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=pt-BR).

>[!IMPORTANT]
>
>Atualmente, a fonte de atributos do cliente não oferece suporte à ativação ou desativação de fluxos de dados.

## Criar uma conexão de origem

>[!NOTE]
>
>Se você já tiver estabelecido uma conexão de origem para os dados de perfil dos Atributos do cliente, a opção para se conectar à fonte será desativada.

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conexão.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Aplicativos Adobe] categoria , selecione **[!UICONTROL Atributos do cliente]** e depois selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Selecionar fonte de dados dos atributos do cliente

O [!UICONTROL Adicionar dados] lista todas as fontes de dados disponíveis para Atributos do cliente. Somente um conjunto de dados pode ser selecionado por conexão de origem dos Atributos do cliente.

>[!NOTE]
>
>Grupos de campos, esquemas e conjuntos de dados são criados prontos para uso como parte do provisionamento de fluxo. Elas permanecerão como estão e você terá que excluí-las manualmente, se necessário.

A evolução do esquema não é suportada pela fonte de atributos do cliente. Se a entrada de esquema de uma fonte de dados dos atributos do cliente for alterada, ela se tornará incompatível com a Platform. Como solução alternativa, você pode excluir um fluxo de dados de atributos do cliente existente, juntamente com seu conjunto de dados, esquema e grupo de campos associados e, em seguida, criar um novo com o esquema atualizado e a fonte de dados.

>[!IMPORTANT]
>
>Embora seja possível excluir um fluxo de dados de atributos do cliente, o conjunto de dados correspondente permanecerá mesmo após a exclusão do fluxo de dados. Consulte o guia sobre [exclusão de um conjunto de dados](../../../../../catalog/datasets/user-guide.md) para obter etapas sobre como excluir manualmente um conjunto de dados.

Para criar uma nova conexão, selecione uma fonte de dados na lista e selecione **[!UICONTROL Próximo]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Fornecer detalhes do fluxo de dados

O [!UICONTROL Detalhes do fluxo de dados] é exibida, permitindo que você forneça um nome e uma breve descrição para o fluxo de dados. Durante esse processo, também é possível definir as configurações para [!UICONTROL Diagnóstico de erros], [!UICONTROL Ingestão parcial]e [!UICONTROL Alertas].

[!UICONTROL Diagnóstico de erros] permite a geração detalhada de mensagens de erro para qualquer registro incorreto que ocorra no seu fluxo de dados, enquanto [!UICONTROL Ingestão parcial] O permite assimilar dados contendo erros, até um determinado limite definido manualmente. Consulte a [visão geral da ingestão parcial de lote](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

Você pode habilitar alertas para receber notificações sobre o status do seu fluxo de dados. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de origens usando a interface do usuário](../../alerts.md).

Quando terminar de fornecer detalhes do fluxo de dados, selecione **[!UICONTROL Próximo]**.

![detalhe do fluxo de dados](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Revisar o fluxo de dados

O [!UICONTROL Revisão] é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e o número de colunas dentro desse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

![revisão](../../../../images/tutorials/create/customer-attributes/review.png)

## Próximas etapas

Depois que a conexão é criada, um esquema de público-alvo e um conjunto de dados são criados automaticamente para conter os dados recebidos. Quando a assimilação inicial for concluída, os dados de perfil dos atributos do cliente poderão ser usados por serviços downstream da plataforma, como [!DNL Real-time Customer Profile] e [!DNL Segmentation Service]. Consulte os seguintes documentos para obter mais detalhes:

* [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
* [[!DNL Segmentation Service] visão geral](../../../../../segmentation/home.md)

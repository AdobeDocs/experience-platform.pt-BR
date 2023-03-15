---
keywords: Experience Platform;página inicial;tópicos populares;Conector de origem do Audience Manager;Audience Manager;conector do audience manager
title: Criar uma conexão de origem do Adobe Audience Manager na interface
description: Este tutorial percorre as etapas para criar uma conexão de origem para que o Adobe Audience Manager traga dados do Evento de experiência do consumidor para a Platform usando a interface do usuário.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Criar uma conexão de origem do Adobe Audience Manager na interface

Este tutorial percorre as etapas para criar um conector de origem para o Adobe Audience Manager trazer dados do evento de experiência do consumidor para a Platform usando a interface do usuário.

## Criar uma conexão de origem com o Adobe Audience Manager

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Aplicativo Adobe], selecione **[!UICONTROL Adobe Audience Manager]** e selecione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

### Selecionar características e segmentos

>[!NOTE]
>
>Não é possível assimilar dados regionais da origem do Audience Manager para o Experience Platform. Se você tiver casos de uso do Analytics que exigem dados regionais, use o [Conector de origem do Analytics](../adobe-applications/analytics.md).

A variável [!UICONTROL Selecionar características e segmentos] é exibida, fornecendo uma interface interativa para explorar e selecionar suas características, segmentos e dados.

* O painel esquerdo da interface contém o [!UICONTROL Selecionar características e segmentos] opções, bem como um diretório hierárquico de todos os segmentos disponíveis.
* A metade direita da interface permite interagir com segmentos selecionados e escolher os dados específicos que deseja usar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar pelos segmentos disponíveis, selecione a pasta que deseja acessar na [!UICONTROL Todos os segmentos] painel. Selecionar uma pasta permite percorrer a hierarquia de uma pasta e fornece uma lista de segmentos para filtrar.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Depois de identificar e selecionar os segmentos que deseja usar, um novo painel aparecerá à direita, exibindo a lista de itens selecionados. Você pode continuar a acessar pastas diferentes e selecionar segmentos diferentes para sua conexão. Selecionar mais segmentos atualiza o painel à direita.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Como alternativa, você pode selecionar a variável **[!UICONTROL Selecionar todos os segmentos]** e **[!UICONTROL Selecionar todas as características]** caixas. Selecionar todos os segmentos levará os segmentos de Audience Manager para a Platform, enquanto selecionar todas as características ativa todas as características originais do Audience Manager.

>[!WARNING]
>
>A assimilação de populações consideráveis de segmentos de Audience Manager tem um impacto direto na contagem total de perfis ao enviar pela primeira vez um segmento de Audience Manager para a Platform usando a origem de Audience Manager. Isso significa que selecionar todos os segmentos pode levar a uma contagem de perfis que excede seu direito de uso de licença. Revise seu [permissão de uso de licença](../../../../../dashboards/guides/license-usage.md) antes de prosseguir.

Quando terminar, selecione **[!UICONTROL Próxima]**

![todos os segmentos](../../../../images/tutorials/create/aam/all-segments.png)

A variável [!UICONTROL Revisão] será exibida, permitindo que você revise as características e os segmentos selecionados antes de eles serem conectados à Platform. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Dados selecionados]**: mostra o número de segmentos selecionados e características ativadas.

![revisão](../../../../images/tutorials/create/aam/review.png)

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

## Próximas etapas

Enquanto um fluxo de dados de Audience Manager estiver ativo, os dados recebidos serão assimilados automaticamente nos Perfis de clientes em tempo real. Agora você pode utilizar esses dados recebidos e criar segmentos de público-alvo usando o Serviço de segmentação de plataforma. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do serviço de segmentação](../../../../../segmentation/home.md)

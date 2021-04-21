---
keywords: Experience Platform, home, tópicos populares, conector de origem do Audience Manager, Audience Manager, conector do audience manager
solution: Experience Platform
title: Criar uma conexão de origem do Adobe Audience Manager na interface do usuário
topic-legacy: overview
type: Tutorial
description: Este tutorial o orienta pelas etapas para criar conectores de origem para o Adobe Audience Manager, para trazer dados do Evento de experiência do consumidor para a Plataforma usando a interface do usuário.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Criar uma conexão de origem do Adobe Audience Manager na interface do usuário

Este tutorial o orienta pelas etapas para criar um conector de origem para o Adobe Audience Manager trazer dados do Evento de experiência do consumidor para a Plataforma usando a interface do usuário.

## Criar uma conexão de origem com o Adobe Audience Manager

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conta.

Na categoria [!UICONTROL Adobe applications], selecione **[!UICONTROL Adobe Audience Manager]** e selecione **[!UICONTROL Configure]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

A etapa [!UICONTROL Select traits and segments] é exibida, fornecendo uma interface interativa para explorar e selecionar suas características, segmentos e dados.

* O painel esquerdo da interface contém as opções [!UICONTROL Select traits and segments] , bem como um diretório hierárquico de todos os segmentos disponíveis para você.
* A metade direita da interface permite interagir com segmentos selecionados e coletar dados específicos que deseja usar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar pelos segmentos disponíveis, selecione a pasta que deseja acessar no painel [!UICONTROL All Segments]. Selecionar uma pasta permite atravessar a hierarquia de uma pasta e fornece uma lista de segmentos para filtrar.

![pasta de segmentos](../../../../images/tutorials/create/aam/segment-folder.png)

Depois de identificar e selecionar os segmentos que deseja usar, um novo painel é exibido à direita, exibindo a lista de itens selecionados. Você pode continuar a acessar pastas diferentes e selecionar segmentos diferentes para sua conexão. Selecionar mais segmentos atualiza o painel à direita.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Como alternativa, você pode selecionar as caixas **[!UICONTROL Select all segments]** e **[!UICONTROL Select all traits]**. A seleção de todos os segmentos trará segmentos Audience Manager para a Plataforma, enquanto a seleção de todas as características ativa todas as características próprias a partir do Audience Manager.

Quando terminar, selecione **[!UICONTROL Next]**

![todos os segmentos](../../../../images/tutorials/create/aam/all-segments.png)

A etapa [!UICONTROL Review] é exibida, permitindo que você revise as características e segmentos selecionados antes que eles sejam conectados à Plataforma. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Connection]**: Mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Selected data]**: Mostra o número de segmentos selecionados e características ativadas.

![revisão](../../../../images/tutorials/create/aam/review.png)

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Finish]** e aguarde algum tempo para que o fluxo de dados seja criado.

## Próximas etapas

Enquanto um fluxo de dados do Audience Manager está ativo, os dados recebidos são assimilados automaticamente em Perfis do cliente em tempo real. Agora você pode utilizar esses dados recebidos e criar segmentos de público-alvo usando o Serviço de segmentação da plataforma. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do serviço de segmentação](../../../../../segmentation/home.md)

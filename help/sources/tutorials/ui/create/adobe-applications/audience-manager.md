---
keywords: Experience Platform, home, tópicos populares, conector de origem do Audience Manager, Audience Manager, conector do audience manager
title: Criar uma conexão de origem do Adobe Audience Manager na interface do usuário
description: Este tutorial o orienta pelas etapas para criar uma conexão de origem para o Adobe Audience Manager trazer dados do Evento de experiência do consumidor para a Plataforma usando a interface do usuário.
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 90a917ea2b623079f26c67b776dd46b62531c7da
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Criar uma conexão de origem do Adobe Audience Manager na interface do usuário

Este tutorial o orienta pelas etapas para criar um conector de origem para o Adobe Audience Manager trazer dados do Evento de experiência do consumidor para a Plataforma usando a interface do usuário.

## Criar uma conexão de origem com o Adobe Audience Manager

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL Aplicativo Adobe], selecione **[!UICONTROL Adobe Audience Manager]** e depois selecione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

### Selecionar características e segmentos

>[!NOTE]
>
>Não é possível assimilar dados regionais da fonte Audience Manager para o Experience Platform. Se você tiver casos de uso do Analytics que exigem dados regionais, use a variável [Conector de origem do Analytics](../adobe-applications/analytics.md).

O [!UICONTROL Selecionar características e segmentos] será exibida, fornecendo uma interface interativa para explorar e selecionar suas características, segmentos e dados.

* O painel esquerdo da interface contém a variável [!UICONTROL Selecionar características e segmentos] , bem como um diretório hierárquico de todos os segmentos disponíveis para você.
* A metade direita da interface permite interagir com segmentos selecionados e coletar dados específicos que deseja usar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar pelos segmentos disponíveis, selecione a pasta que deseja acessar do [!UICONTROL Todos os segmentos] painel. Selecionar uma pasta permite atravessar a hierarquia de uma pasta e fornece uma lista de segmentos para filtrar.

![pasta de segmentos](../../../../images/tutorials/create/aam/segment-folder.png)

Depois de identificar e selecionar os segmentos que deseja usar, um novo painel é exibido à direita, exibindo a lista de itens selecionados. Você pode continuar a acessar pastas diferentes e selecionar segmentos diferentes para sua conexão. Selecionar mais segmentos atualiza o painel à direita.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Como alternativa, você pode selecionar a variável **[!UICONTROL Selecionar todos os segmentos]** e **[!UICONTROL Selecionar todas as características]** caixas. A seleção de todos os segmentos trará segmentos Audience Manager para a Plataforma, enquanto a seleção de todas as características ativa todas as características próprias da Audience Manager.

Depois de concluir, selecione **[!UICONTROL Próximo]**

![todos os segmentos](../../../../images/tutorials/create/aam/all-segments.png)

O [!UICONTROL Revisão] é exibida, permitindo que você analise suas características e segmentos selecionados antes que eles sejam conectados à Platform. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Dados selecionados]**: Mostra o número de segmentos selecionados e características ativadas.

![revisão](../../../../images/tutorials/create/aam/review.png)

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

## Próximas etapas

Enquanto um fluxo de dados do Audience Manager está ativo, os dados recebidos são assimilados automaticamente em Perfis do cliente em tempo real. Agora você pode utilizar esses dados recebidos e criar segmentos de público-alvo usando o Serviço de segmentação da plataforma. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do serviço de segmentação](../../../../../segmentation/home.md)

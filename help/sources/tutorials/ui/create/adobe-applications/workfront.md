---
keywords: Experience Platform; home; tópicos populares;
title: (Beta) Criar uma conexão de origem do Adobe Workfront na interface do usuário
description: Este tutorial fornece etapas para criar uma conexão de origem do Adobe Workfront para trazer seus dados do Workfront para o Adobe Experience Platform usando a interface do usuário.
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# (Beta) Criar uma conexão de origem do Adobe Workfront na interface do usuário

>[!NOTE]
>
>A fonte do Adobe Workfront está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar uma conexão de origem do Adobe Workfront para trazer seus dados do Workfront para o Adobe Experience Platform usando a interface do usuário.

## Introdução

>[!IMPORTANT]
>
>Você deve estar configurado como administrador no Adobe Admin Console para acessar a fonte do Workfront.

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil do cliente em tempo real](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Criar uma conexão de origem do Workfront na interface do usuário

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes que podem ser usadas para criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Também é possível usar a barra de pesquisa para restringir as fontes exibidas.

Em **[!UICONTROL Aplicativos Adobe]** categoria , selecione **[!UICONTROL Adobe Workfront]** e depois selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes com a fonte do Adobe Workfront é realçado.](../../../../images/tutorials/create/workfront/catalog.png)

## Selecionar dados

O [!UICONTROL Selecionar dados] será exibida. Aqui, você deve fornecer valores para o subdomínio e o Datalane do Workfront. O subdomínio Workfront é o mesmo URL usado para acessar a instância do Workfront, por exemplo `https://acme.workfront.com/`, enquanto seu DataList representa o ambiente do front-end que você deseja usar.

Depois de adicionar o subdomínio e o painel de dados, selecione **[!UICONTROL Próximo]**.

![A página de dados selecionada com valores de espaço reservado para subdomínio e painel de dados.](../../../../images/tutorials/create/workfront/select-data.png)

## Fornecer detalhes do fluxo de dados

A etapa de detalhes do fluxo de dados permite fornecer um nome e uma descrição opcional para o fluxo de dados. Durante essa etapa, você também pode assinar alertas para receber notificações sobre o status do fluxo de dados. Para obter mais informações sobre alertas, visite o tutorial em [inscrever-se em alertas na interface do usuário de fontes](../../alerts.md).

Depois de fornecer os detalhes do fluxo de dados e definir as configurações de alerta desejadas, selecione **[!UICONTROL Próximo]**.

![A página de detalhes do fluxo de dados com informações sobre o nome do fluxo de dados, descrição e notificações de alerta](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Revisão

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas dentro desse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![A página de revisão que resume informações de conexão.](../../../../images/tutorials/create/workfront/review.png)

## Apêndice

As seções a seguir fornecem informações adicionais sobre a fonte do Workfront.

### Alterar esquema de evento do Workfront

Os dados do Workfront na Platform são representados como dados de registro de séries de tempo, em que cada linha nos dados tem um carimbo de data e hora que é exibido quando o evento ocorreu e os atributos relacionados a ele.

Durante a configuração, um esquema chamado Workfront Change Events from Flow é criado.

| Campo Esquema | Descrição |
| --- | --- |
| `timestamp` | A hora em que o evento selecionado ocorreu. O carimbo de data e hora é representado no fuso horário GTM. |
| `_workfront.objectType` | O tipo de objeto. Os valores disponíveis podem incluir `project`, `task`, `portfolio`e outros, dependendo do objeto que foi alterado ou criado. |
| `_workfront.objectID` | A ID que corresponde ao tipo de objeto. |
| `_workfront.created` | Este valor está definido como `1` se o evento representar uma criação de objeto. |
| `_workfront.deleted` | Este valor está definido como `1` se o objeto for excluído. |
| `_worfkront.updated` | Este valor está definido como `1` se o objeto for atualizado. |
| `_workfront.completed` | Este valor está definido como `1` se o objeto estiver marcado como concluído. |
| `_workfront.parentObjectType` | (Opcional) O tipo de objeto que corresponde ao pai do objeto. |
| `_workfront.parentID` | A ID do objeto pai. |
| `_workfront.customData` | Um mapa de todos os campos e valores de formulários personalizados preenchidos durante o evento. |

>[!IMPORTANT]
>
>Somente os atributos que foram alterados ou criados como parte de um evento são preenchidos. Por exemplo, se você alterar apenas o nome do objeto, os únicos campos que serão preenchidos serão:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Próximas etapas

Ao seguir este tutorial, você criou um fluxo de dados para trazer seus dados do Workfront para o Experience Platform. Agora você pode usar serviços como [Serviço de query](../../../../../query-service/home.md) para executar análises adicionais sobre seus dados. Para obter mais informações sobre o Workfront, leia a [Visão geral do Workfront](../../../../connectors/adobe-applications/workfront.md).

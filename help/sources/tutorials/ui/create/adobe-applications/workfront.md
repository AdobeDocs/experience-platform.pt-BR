---
keywords: Experience Platform;página inicial;tópicos populares;
title: (Beta) Criar uma conexão de origem do Adobe Workfront na interface
description: Este tutorial fornece etapas para criar uma conexão de origem do Adobe Workfront para trazer seus dados do Workfront para o Adobe Experience Platform usando a interface do usuário.
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# (Beta) Criar uma conexão de origem do Adobe Workfront na interface

>[!NOTE]
>
>A fonte do Adobe Workfront está na versão beta. Consulte a [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para criar uma conexão de origem do Adobe Workfront para trazer seus dados do Workfront para o Adobe Experience Platform usando a interface do usuário.

## Introdução

>[!IMPORTANT]
>
>Você deve estar configurado como administrador no Adobe Admin Console para acessar a origem do Workfront.

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Perfil do cliente em tempo real](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

## Criar uma conexão de origem do Workfront na interface

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] A tela exibe uma variedade de fontes que podem ser usadas para criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Você também pode usar a barra de pesquisa para restringir as fontes exibidas.

No **[!UICONTROL aplicativos Adobe]** categoria, selecione **[!UICONTROL Adobe Workfront]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com a origem do Adobe Workfront realçada.](../../../../images/tutorials/create/workfront/catalog.png)

## Selecionar dados

A variável [!UICONTROL Selecionar dados] é exibida. Aqui, você deve fornecer valores para o subdomínio do Workfront e o datalane. O subdomínio do Workfront é o mesmo URL usado para acessar a instância do Workfront, por exemplo `https://acme.workfront.com/`, enquanto seu datalane representa o ambiente do workfront que você deseja usar.

Depois de adicionar o subdomínio e o datalane, selecione **[!UICONTROL Próxima]**.

![A página Selecionar dados com valores de espaço reservado para subdomínio e datalane.](../../../../images/tutorials/create/workfront/select-data.png)

## Fornecer detalhes do fluxo de dados

A etapa de detalhes do fluxo de dados permite fornecer um nome e uma descrição opcional para o fluxo de dados. Durante essa etapa, você também pode assinar alertas para receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o tutorial em [assinatura de alertas na interface de origens](../../alerts.md).

Depois de fornecer os detalhes do fluxo de dados e definir as configurações de alerta desejadas, selecione **[!UICONTROL Próxima]**.

![A página de detalhes do fluxo de dados com informações sobre nome do fluxo de dados, descrição e notificações de alerta](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Consulte a seção

A variável **[!UICONTROL Revisão]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.

Depois de revisar o fluxo de dados, selecione **[!UICONTROL Concluir]** e aguarde algum tempo para criar o fluxo de dados.

![A página de revisão que resume as informações de conexão.](../../../../images/tutorials/create/workfront/review.png)

## Apêndice

As seções a seguir fornecem informações adicionais sobre a origem do Workfront.

### Esquema do evento de alteração do Workfront

Os dados do Workfront na Platform são representados como dados de registro de série temporal, em que cada linha nos dados tem um carimbo de data e hora que exibe quando o evento ocorreu e os atributos relacionados a esse evento.

Durante a configuração, um esquema chamado Workfront Change Events from Flow é criado.

| Campo de esquema | Descrição |
| --- | --- |
| `timestamp` | A hora em que o evento selecionado ocorreu. O carimbo de data e hora é representado no fuso horário GTM. |
| `_workfront.objectType` | O tipo de objeto. Os valores disponíveis podem incluir `project`, `task`, `portfolio`e outros, dependendo do objeto que foi alterado ou criado. |
| `_workfront.objectID` | A ID que corresponde ao tipo de objeto. |
| `_workfront.created` | Esse valor é definido como `1` se o evento representar uma criação de objeto. |
| `_workfront.deleted` | Esse valor é definido como `1` se o objeto for excluído. |
| `_worfkront.updated` | Esse valor é definido como `1` se o objeto for atualizado. |
| `_workfront.completed` | Esse valor é definido como `1` se o objeto estiver marcado como concluído. |
| `_workfront.parentObjectType` | (Opcional) O tipo de objeto que corresponde ao pai do objeto. |
| `_workfront.parentID` | A ID do objeto pai. |
| `_workfront.customData` | Um mapa de todos os campos e valores de formulário personalizados preenchidos durante o evento. |

>[!IMPORTANT]
>
>Somente os atributos que foram alterados ou criados como parte de um evento são preenchidos. Por exemplo, se você alterar apenas o nome do objeto, os únicos campos que serão preenchidos serão:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Próximas etapas

Ao seguir este tutorial, você agora criou um fluxo de dados para trazer seus dados do Workfront para o Experience Platform. Agora você pode usar serviços como [Serviço de consulta](../../../../../query-service/home.md) para executar uma análise mais detalhada dos dados. Para obter mais informações sobre o Workfront, leia a [Visão geral do Workfront](../../../../connectors/adobe-applications/workfront.md).

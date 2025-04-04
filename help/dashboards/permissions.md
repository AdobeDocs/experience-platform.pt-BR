---
solution: Experience Platform
title: Como obter e conceder permissões de acesso aos painéis do Experience Platform
type: Documentation
description: Conceda aos usuários a capacidade de exibir, editar e atualizar painéis do Experience Platform usando o Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 6%

---

# Permissões de acesso para painéis

Para conceder aos usuários a capacidade de exibir, editar e atualizar painéis, primeiro você deve habilitar permissões. No Adobe Experience Platform, o controle de acesso é fornecido por meio da [Adobe Admin Console](https://adminconsole.adobe.com/). Os usuários são vinculados a permissões e sandboxes por meio de perfis de produto no [!DNL Admin Console].

Este documento fornece um resumo das permissões disponíveis para painéis, incluindo os recursos aos quais eles dão acesso e as funções de usuário que eles habilitam. Para obter informações detalhadas sobre como obter e atribuir permissões de acesso, comece lendo a [visão geral do controle de acesso](../access-control/home.md).

## Pré-requisitos

Para configurar o controle de acesso para [!DNL Experience Platform], você deve ter privilégios de administrador para uma organização que tenha uma integração de produto [!DNL Experience Platform]. Consulte o artigo da Central de ajuda da Adobe em [funções administrativas](https://helpx.adobe.com/br/enterprise/using/admin-roles.html) para obter mais informações.

## Permissões de painel disponíveis {#available-permissions}

O serviço [!DNL Dashboards] fornece três permissões que, quando combinadas, fornecem acesso total aos painéis [!UICONTROL Perfis], [!UICONTROL Segmentos], [!UICONTROL Destinos] e [!UICONTROL Uso de Licenças] dentro do Adobe Experience Platform. Essas permissões são:

| Permissão | Descrição |
|---|---|
| **Gerenciar Painéis Padrão** | Esta permissão é uma **permissão global de leitura e gravação**. Permite [criar widgets personalizados](./customize/custom-widgets.md) e [editar o esquema de widget](./customize/edit-schema.md) por meio da [!UICONTROL Biblioteca de widgets]. |
| **Exibir Painéis Padrão** | Isso fornece a funcionalidade **somente leitura** para os painéis [!UICONTROL Perfis], [!UICONTROL Destinos] e [!UICONTROL Segmentos] e permite o acesso a eles por meio da navegação à esquerda da Experience Platform. Ele também adiciona [!UICONTROL Painéis] à navegação à esquerda e acesso à guia de inventário e integrações do [!UICONTROL Painéis]. |
| **Exibir Painel de Uso de Licenças** | Esta permissão permite aos usuários **somente leitura** acesso ao [painel de uso de licença](./guides/license-usage.md) na interface do usuário do Experience Platform. |

Há cinco permissões não incluídas na categoria [!DNL Dashboard] que podem ser necessárias, dependendo de suas necessidades. A tabela a seguir descreve os locais de categoria na Admin Console:

>[!IMPORTANT]
>
>As permissões **[!DNL Manage Standard Dashboards]** e **[!DNL View Standard Dashboards]** **exigem** uma permissão &quot;exibir&quot; ou &quot;gerenciar&quot; da categoria [!DNL Profile Management] ou [!DNL Destinations] na Admin Console para ativar as seções relevantes na interface do usuário do Experience Platform.

| Permissão | Local da categoria do Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matriz de controle de acesso

A matriz de controle de acesso a seguir fornece um detalhamento de quais permissões são necessárias e qual função elas fornecem em relação ao acesso aos diferentes recursos do painel. As permissões são listadas na linha horizontal superior e o espaço de trabalho da interface do usuário do Experience Platform é listado na coluna à esquerda.

|   | [!UICONTROL Exibir Painel Padrão] OU [!UICONTROL Gerenciar Painel Padrão] | [!UICONTROL Exibir Perfis],<br/>[!UICONTROL Exibir Segmentos],<br/> [!UICONTROL Exibir Destinos] | [!UICONTROL Gerenciar consultas] e [!UICONTROL Gerenciar sandboxes] | [!UICONTROL Exibir Painel de Uso de Licenças] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] na navegação à esquerda. | N/D | **É NECESSÁRIA uma permissão &quot;Exibir&quot; ou &quot;Gerenciar&quot;** para cada respectivo painel. | N/D | N/D |
| [!DNL Dashboards] na navegação à esquerda. | ATIVADO | **É NECESSÁRIO PELO MENOS**. | N/D | N/D |
| [!DNL Dashboards] [!DNL Inventory] <br/>(a guia procurar) | ATIVADO | N/D | N/D | N/D |
| Guia <br/> do [!DNL Dashboards] [!DNL Integrations] (usada para instalar o Power BI) | ATIVADO | **É NECESSÁRIO PELO MENOS** | N/D | N/D |
| Fluxo de trabalho e botão Instalar do Power BI | ATIVADO | N/D | **NECESSÁRIO** | N/D |
| Painéis de [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations].<br/>A capacidade de editar esquemas de widget e adicionar novos atributos para personalização de widget | **Gerenciar-painel-padrão NECESSÁRIO** | **OBRIGATÓRIO (para cada respectivo painel)** | N/D | N/D |
| [!DNL License Usage Dashboard] | N/D | N/D | N/D | ATIVADO |

{style="table-layout:auto"}

## Adicionar permissões ao perfil de produto

Use as informações fornecidas acima para adicionar as permissões apropriadas ao perfil do produto. Consulte a documentação para obter instruções completas sobre [como adicionar permissões por meio da interface de controle de acesso](../access-control/ui/permissions.md).

Para obter descrições das permissões, consulte a seção [permissões disponíveis](#available-permissions), apresentada anteriormente neste documento.

>[!NOTE]
>
>Não é necessário ativar todas as permissões para todos os usuários. Dependendo da estrutura de sua organização, talvez você queira criar perfis de produto separados para determinados usuários e conceder acesso limitado (como somente leitura). Consulte a documentação sobre gerenciamento de usuários para um perfil de produto para saber [como atribuir permissões para usuários específicos](../access-control/ui/users.md).

Após adicionar as permissões de acesso necessárias, os usuários em sua organização podem começar a exibir painéis na interface do usuário do Experience Platform e executar outras ações com base nas permissões atribuídas.

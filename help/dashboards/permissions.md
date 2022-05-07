---
solution: Experience Platform
title: Como obter e conceder permissões de acesso a painéis do Experience Platform
type: Documentation
description: Conceda aos usuários a capacidade de visualizar, editar e atualizar painéis do Experience Platform usando o Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: 052e365c6127961363b7b5333cb0f4f82ab5479a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 7%

---

# Permissões de acesso para painéis

Para conceder aos usuários a capacidade de exibir, editar e atualizar painéis, primeiro você deve ativar permissões. No Adobe Experience Platform, o controle de acesso é fornecido por meio da variável [Adobe Admin Console](https://adminconsole.adobe.com/). Os usuários são vinculados a permissões e sandboxes por meio de perfis de produtos na [!DNL Admin Console].

Este documento fornece um resumo das permissões disponíveis para painéis, incluindo os recursos aos quais eles dão acesso e as funções de usuário que habilitam. Para obter informações detalhadas sobre obter e atribuir permissões de acesso, comece lendo o [visão geral do controle de acesso](../access-control/home.md).

## Pré-requisitos

Para configurar o controle de acesso para [!DNL Experience Platform], você deve ter privilégios de administrador para uma organização que tenha um [!DNL Experience Platform] integração do produto. Consulte o artigo da Adobe Help Center em [funções administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.html) para obter mais informações.

## Permissões disponíveis no painel {#available-permissions}

O [!DNL Dashboards] fornece três permissões que, quando combinadas, fornecem acesso total ao [!UICONTROL Perfis], [!UICONTROL Segmentos], [!UICONTROL Destinos]e [!UICONTROL Uso de licença] painéis no Adobe Experience Platform. Essas permissões são:

| Permissão | Descrição |
|---|---|
| **Gerenciar painéis padrão** | Essa permissão é uma **permissão global de leitura e gravação**. Permite [criar widgets personalizados](./customize/custom-widgets.md) e [editar o esquema de widget](./customize/edit-schema.md) através da [!UICONTROL Biblioteca de widgets]. |
| **Exibir painéis padrão** | Isso fornece **somente leitura** para [!UICONTROL Perfis], [!UICONTROL Destinos]e [!UICONTROL Segmentos] painéis e permite acesso a eles por meio da navegação à esquerda da plataforma. Ele também acrescenta: [!UICONTROL Painéis] à esquerda e ao acesso à [!UICONTROL Painéis] guia inventário e integrações. |
| **Exibir painel de uso de licença** | Essa permissão permite que os usuários **somente leitura** acesso a [o painel de uso da licença](./guides/license-usage.md) na interface do usuário do Experience Platform. |

Há cinco permissões não incluídas no [!DNL Dashboard] categoria que é potencialmente necessária, dependendo de suas necessidades. A tabela a seguir descreve os locais de categoria na Admin Console:

>[!IMPORTANT]
>
>Ambos os **[!DNL Manage Standard Dashboards]** e **[!DNL View Standard Dashboards]** permissões **exigir** uma permissão &quot;exibir&quot; ou &quot;gerenciar&quot; no [!DNL Profile Management] ou [!DNL Destinations] na Admin Console para ativar as seções relevantes na interface do usuário da plataforma.

| Permissão | Localização da categoria Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matriz de controle de acesso

A matriz de controle de acesso a seguir fornece um detalhamento de quais permissões são necessárias e qual função elas oferecem em relação ao acesso aos diferentes recursos do painel. As permissões são listadas na linha horizontal superior e o espaço de trabalho da interface do usuário da plataforma é listado ao longo da coluna esquerda.

|  | [!UICONTROL Exibir painel padrão] OU [!UICONTROL Gerenciar painel padrão] | [!UICONTROL Exibir perfis],<br/>[!UICONTROL Exibir segmentos],<br/> [!UICONTROL Exibir destinos] | [!UICONTROL Gerenciar Consultas] &amp; [!UICONTROL Gerenciar sandboxes] | [!UICONTROL Exibir painel de uso de licença] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] no painel de navegação esquerdo. | N/D | **É NECESSÁRIA uma permissão &quot;Exibir&quot; ou &quot;Gerenciar&quot;** para cada painel respectivo. | N/D | N/D |
| [!DNL Dashboards] no painel de navegação esquerdo. | ATIVADO | **Pelo menos um OBRIGATÓRIO**. | N/D | N/D |
| [!DNL Dashboards] [!DNL Inventory] <br/>(a guia browse ) | ATIVADO | N/D | N/D | N/D |
| [!DNL Dashboards] [!DNL Integrations] guia <br/>(usado para instalar o Power BI) | ATIVADO | **Pelo menos um OBRIGATÓRIO** | N/D | N/D |
| Botão Instalar e fluxo de trabalho do Power BI | ATIVADO | N/D | **OBRIGATÓRIO** | N/D |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] painéis.<br/>A capacidade de editar esquemas de widget e adicionar novos atributos para personalização de widgets | **É NECESSÁRIO Gerenciar painel padrão** | **OBRIGATÓRIO (para cada painel respectivo)** | N/D | N/D |
| [!DNL License Usage Dashboard] | N/D | N/D | N/D | ATIVADO |

{style=&quot;table-layout:auto&quot;}

## Adicionar permissões ao perfil do produto

Use as informações fornecidas acima para adicionar as permissões apropriadas ao seu perfil de produto. Consulte a documentação para obter instruções completas sobre [como adicionar permissões por meio da interface do usuário de controle de acesso](../access-control/ui/permissions.md).

Para obter descrições das permissões, consulte o [permissões disponíveis](#available-permissions) anteriormente neste documento.

>[!NOTE]
>
>Não é necessário habilitar todas as permissões para todos os usuários. Dependendo da estrutura de sua organização, talvez você queira criar perfis de produto separados para determinados usuários e conceder acesso limitado (como somente leitura). Consulte a documentação sobre como gerenciar usuários para obter um perfil de produto para saber mais [como atribuir permissões para usuários específicos](../access-control/ui/users.md).

Depois de ter adicionado as permissões de acesso necessárias, os usuários em sua organização podem começar a visualizar painéis na interface do usuário do Experience Platform e executar outras ações com base nas permissões atribuídas.

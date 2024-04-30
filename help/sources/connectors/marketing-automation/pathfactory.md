---
title: Visão geral da origem do PathFactory
description: Saiba como conectar o PathFactory ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Beta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# [!DNL PathFactory]

>[!NOTE]
>
>A variável [!DNL PathFactory] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

[[!DNL PathFactory]](https://www.pathfactory.com/) O oferece uma plataforma baseada em nuvem que ajuda as empresas a gerenciar jornadas de conteúdo e impulsionar o engajamento por meio de insights inteligentes de conteúdo. Este guia detalha como é possível integrar dados do PathFactory ao Experience Platform, utilizando conectores do PathFactory para assimilação de dados ideal.

Você pode assimilar dados de [[!DNL PathFactory]](https://www.pathfactory.com/) usando três fontes principais:

* **[!DNL Visitors]**: assimile dados de clientes e contatos como registros para entender melhor seu público-alvo.
* **[!DNL Sessions]**: eventos de série temporal que rastreiam atividades de sessão de usuário individual na sua plataforma.
* **[!DNL Page Views]**: eventos de série temporal que fornecem insights sobre quais páginas estão sendo exibidas, ajudando você a analisar o desempenho do conteúdo.

Leia o documento abaixo para obter informações sobre como configurar seus [!DNL PathFactory] conta de origem.

## LISTA DE PERMISSÕES de endereço IP {#ip-allow-list}

Pode ser necessário adicionar uma lista de endereços IP a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes de começar a integração [[!DNL PathFactory]](https://www.pathfactory.com/) conectores com o Experience Platform, verifique se os seguintes pré-requisitos estão sendo atendidos:

* **A [Conta PathFactory]**.
   * Contato [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) se você ainda não tiver uma conta válida.
* **Uma assinatura ativa** a qualquer [!DNL PathFactory] produto.
* **Nome de usuário, senha e domínio**.
   * Essas credenciais são necessárias para acessar o [!DNL PathFactory] conta e seus dados.
* **Token de acesso** e **Endpoints de API**.
   * São necessários para a conexão com o [!DNL PathFactory] APIs.

### Como obter credenciais e tokens de acesso {#gather-credentials}

Para conectar [!DNL PathFactory] para o Experience Platform, você deve fornecer as seguintes credenciais:

| Credencial | Descrição | Endpoint |
| --- | --- | --- |
| Nome de usuário | Seu [!DNL PathFactory] usuário da conta. | Não aplicável |
| Senha | Seu [!DNL PathFactory] senha da conta. | Não aplicável |
| Domínio | O domínio associado à [!DNL PathFactory] conta. | Não aplicável |
| Token de acesso | Um token exclusivo usado para autenticação da API. | Não aplicável |
| Endpoint de visitantes | O endpoint da API para dados do visitante. | `/api/public/v3/data_lake_apis/visitors.json` |
| Endpoint de sessões | O endpoint da API para dados de sessão. | `/api/public/v3/data_lake_apis/sessions.json` |
| Ponto de extremidade de exibições de página | O terminal da API para dados de exibição de página. | `/api/public/v3/data_lake_apis/page_views.json` |

Para obter instruções detalhadas sobre como obter nome de usuário, senha, domínio e token de acesso, visite o [[!DNL PathFactory] Centro de suporte](https://support.pathfactory.com/categories/adobe/). Esse recurso fornece guias abrangentes sobre como recuperar e gerenciar suas credenciais.

### Configurar permissões no Experience Platform

Você deve ter ambos **[!UICONTROL Exibir fontes]** e **[!UICONTROL Gerenciar fontes]** permissões habilitadas para sua conta para conectar seu [!DNL PathFactory] conta para Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia a [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

## Conectar [!DNL PathFactory] para a Platform {#pathfactory-connect}

A documentação abaixo fornece informações sobre como se conectar [!DNL PathFactory] para a Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL PathFactory] dados para a Platform usando APIs](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Conecte seu [!DNL PathFactory] conta para Experience Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Criar um fluxo de dados para uma conexão de origem usando a interface](../../tutorials/ui/dataflow/marketing-automation.md).

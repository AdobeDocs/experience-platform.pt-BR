---
title: Visão geral do PathFactory Source
description: Saiba como conectar o PathFactory ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2024-04-30T00:00:00Z
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 3%

---

# [!DNL PathFactory]

[[!DNL PathFactory]](https://www.pathfactory.com/) oferece uma plataforma baseada em nuvem que ajuda as empresas a gerenciar jornadas de conteúdo e impulsionar o engajamento por meio de insights de conteúdo inteligentes. Este guia detalha como é possível integrar dados do PathFactory ao Experience Platform, utilizando conectores do PathFactory para assimilação de dados ideal.

Você pode assimilar dados de [[!DNL PathFactory]](https://www.pathfactory.com/) usando três fontes primárias:

* **[!DNL Visitors]**: Assimilar dados de clientes e contatos como registros para entender melhor seu público-alvo.
* **[!DNL Sessions]**: eventos de série temporal que rastreiam atividades de sessão de usuário individual na sua plataforma.
* **[!DNL Page Views]**: eventos de série temporal que fornecem insights sobre quais páginas estão sendo exibidas, ajudando você a analisar o desempenho do conteúdo.

Leia o documento abaixo para obter informações sobre como configurar sua conta de origem do [!DNL PathFactory].

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-allow-list}

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes de começar a integrar os conectores do [[!DNL PathFactory]](https://www.pathfactory.com/) ao Experience Platform, verifique se você atende aos seguintes pré-requisitos:

* **Uma [conta PathFactory]**.
   * Contate [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) se você ainda não tiver uma conta válida.
* **Uma assinatura ativa** para qualquer produto [!DNL PathFactory].
* **Nome de usuário, senha e domínio**.
   * Essas credenciais são necessárias para acessar a conta do [!DNL PathFactory] e seus dados.
* **Token de Acesso** e **Pontos de Extremidade de API**.
   * Eles são necessários para a conexão com APIs [!DNL PathFactory].

### Como obter credenciais e tokens de acesso {#gather-credentials}

Para conectar [!DNL PathFactory] ao Experience Platform, você deve fornecer as seguintes credenciais:

| Credencial | Descrição | Endpoint |
| --- | --- | --- |
| Nome de usuário | Seu nome de usuário da conta [!DNL PathFactory]. | Não aplicável |
| Senha | A senha da sua conta [!DNL PathFactory]. | Não aplicável |
| Domínio | O domínio associado à sua conta [!DNL PathFactory]. | Não aplicável |
| Token de acesso | Um token exclusivo usado para autenticação da API. | Não aplicável |
| Endpoint de visitantes | O endpoint da API para dados do visitante. | `/api/public/v3/data_lake_apis/visitors.json` |
| Endpoint de sessões | O endpoint da API para dados de sessão. | `/api/public/v3/data_lake_apis/sessions.json` |
| Ponto de extremidade de exibições de página | O terminal da API para dados de exibição de página. | `/api/public/v3/data_lake_apis/page_views.json` |

Para obter instruções detalhadas sobre como obter seu nome de usuário, senha, domínio e token de acesso, visite o [[!DNL PathFactory] Centro de Suporte](https://support.pathfactory.com/categories/adobe/). Esse recurso fornece guias abrangentes sobre como recuperar e gerenciar suas credenciais.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL View Sources]** e **[!UICONTROL Manage Sources]** habilitadas para sua conta para conectar sua conta do [!DNL PathFactory] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

## Conectar [!DNL PathFactory] ao Experience Platform {#pathfactory-connect}

A documentação abaixo fornece informações sobre como conectar o [!DNL PathFactory] ao Experience Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL PathFactory] dados para a Experience Platform usando APIs](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Conecte sua conta [!DNL PathFactory] à Experience Platform usando a interface](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Criar um fluxo de dados para uma conexão de origem usando a interface](../../tutorials/ui/dataflow/marketing-automation.md).

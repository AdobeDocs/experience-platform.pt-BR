---
title: Visão geral do Google Ads Source
description: Saiba como conectar o Google Ads ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# [!DNL Google Ads] origem

>[!NOTE]
>
>A origem [!DNL Google Ads] está na versão beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema de publicidade de terceiros. O suporte para provedores de publicidade inclui [!DNL Google Ads].

## Pré-requisitos {#prerequisites}

### LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Google Ads] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

### Coletar credenciais necessárias

Você deve fornecer os valores apropriados para as credenciais a seguir para conectar com êxito sua conta do [!DNL Google Ads] à Experience Platform.

| Credencial | Descrição |
| --- | --- |
| `clientCustomerId` | A ID do cliente é o número da conta que corresponde à conta do cliente [!DNL Google Ads] que você deseja gerenciar com a API [!DNL Google Ads]. Esta ID segue o modelo de `123-456-7890`. |
| `loginCustomerId` | A ID do cliente de logon é o número da conta que corresponde à sua conta de gerente do [!DNL Google Ads] e é usada para buscar dados de relatório de um cliente operacional específico. Para obter mais informações sobre como fazer logon na ID do cliente, leia a [[!DNL Google Ads] documentação da API](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | O token do desenvolvedor permite acessar a API [!DNL Google Ads]. Você pode usar o mesmo token de desenvolvedor para fazer solicitações em todas as suas contas do [!DNL Google Ads]. Recupere seu token de desenvolvedor [fazendo logon em sua conta de gerente](https://ads.google.com/home/tools/manager-accounts/) e navegando até a página [!DNL API Center]. |
| `refreshToken` | O token de atualização faz parte da autenticação [!DNL OAuth2]. Esse token permite gerar novamente os tokens de acesso após a expiração. |
| `clientId` | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação [!DNL OAuth2]. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Google]. |
| `clientSecret` | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação [!DNL OAuth2]. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Google]. |
| `googleAdsApiVersion` | A versão da API atual com suporte por [!DNL Google Ads]. Enquanto a última versão é `v18`, a última versão com suporte no Experience Platform é `v17`. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Google Ads] é: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. Esse valor é necessário se você estiver conectando sua conta do [!DNL Google Ads] usando a API do [!DNL Flow Service]. |

## Conectar [!DNL Google Ads] ao Experience Platform

A documentação abaixo fornece informações sobre como conectar o [!DNL Google Ads] ao Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

* [Criar uma conexão básica do Google Ads usando a API de serviço de fluxo](../../tutorials/api/create/advertising/ads.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de publicidade usando a API do serviço de fluxo](../../tutorials/api/collect/advertising.md)

### Uso da interface

* [Criar uma conexão de origem do Google Ads na interface](../../tutorials/ui/create/advertising/ads.md)
* [Criar um fluxo de dados para uma conexão de origem de anúncio na interface](../../tutorials/ui/dataflow/advertising.md)

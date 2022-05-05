---
keywords: Experience Platform, home, tópicos populares, salesforce marketing cloud, Marketing Cloud Salesforce, automação de marketing
solution: Experience Platform
title: Visão geral da fonte de Marketing Cloud do Salesforce
topic-legacy: overview
description: Saiba como conectar o Salesforce Marketing Cloud ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# (Beta) [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>O [!DNL Salesforce Marketing Cloud] A fonte está em beta. Consulte a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

[!DNL Experience Platform] O oferece suporte para assimilar dados de sistemas de automação de marketing de terceiros. O suporte para provedores de automação de marketing inclui [!DNL Salesforce Marketing Cloud].

## Pré-requisitos

Antes de se conectar [!DNL Salesforce Marketing Cloud] de origem para plataforma, você deve garantir que: **escopos de permissão** são provisionadas para sua [!DNL Salesforce Marketing Cloud] ID do cliente e combinação de segredo do cliente:

* `campaign_read`
* `list_and_subscribers_read`

Você pode solicitar escopos fazendo uma chamada para a variável `v2/userinfo` do [!DNL Salesforce Marketing Cloud] API. Consulte a [[!DNL Salesforce Marketing Cloud] Documento de escopos de permissão de integração de API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) para obter orientação sobre como solicitar e comparar escopos.

Para obter mais informações sobre escopos, incluindo uma lista de suas permissões e comportamentos relacionados, consulte [[!DNL Salesforce Marketing Cloud] Documento da API REST](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Connect [!DNL Salesforce Marketing Cloud] para Plataforma usando APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Salesforce Marketing Cloud] para Plataforma usando APIs:

* [Criar uma conexão base de Marketing Cloud do Salesforce usando a API do Serviço de Fluxo](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorar tabelas de dados usando a API do Serviço de fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de automação de marketing usando a API do Serviço de fluxo](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] para Plataforma usando a interface do usuário

A documentação abaixo fornece informações sobre como se conectar [!DNL Salesforce Marketing Cloud] para Plataforma usando a interface do usuário:

* [Criar uma conexão de origem do Marketing Cloud do Salesforce na interface do usuário](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Criar um fluxo de dados para uma conexão de origem da automação de marketing na interface do usuário](../../tutorials/ui/dataflow/marketing-automation.md)

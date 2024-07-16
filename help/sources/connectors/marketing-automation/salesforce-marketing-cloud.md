---
solution: Experience Platform
title: Visão geral do Salesforce Marketing Cloud Source
description: Saiba como conectar o Salesforce Marketing Cloud ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: bc37d41d0f7b0ff0cf4d52242f41467f2891d613
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de sistemas de automação de marketing de terceiros. O suporte para provedores de automação de marketing inclui [!DNL Salesforce Marketing Cloud].

## Pré-requisitos

Antes de poder conectar sua origem [!DNL Salesforce Marketing Cloud] à Platform, você deve garantir que os **escopos de permissão** a seguir sejam provisionados para sua combinação de ID de cliente e segredo de cliente [!DNL Salesforce Marketing Cloud]:

* `campaign_read`
* `list_and_subscribers_read`

Você pode solicitar escopos fazendo uma chamada para o recurso `v2/userinfo` da API [!DNL Salesforce Marketing Cloud]. Consulte o [[!DNL Salesforce Marketing Cloud] documento Escopos de Permissão de Integração de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obter orientação sobre como solicitar e comparar escopos.

Para obter mais informações sobre escopos, incluindo uma lista de suas permissões e comportamentos relacionados, consulte este [[!DNL Salesforce Marketing Cloud] documento sobre API REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não tem suporte da integração de origem [!DNL Salesforce Marketing Cloud].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Conectar [!DNL Salesforce Marketing Cloud] à plataforma usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce Marketing Cloud] à Platform usando APIs:

* [Criar uma conexão básica de Marketing Cloud do Salesforce usando a API do Serviço de fluxo](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de automação de marketing usando a API do Serviço de fluxo](../../tutorials/api/collect/marketing-automation.md)

## Conectar [!DNL Salesforce Marketing Cloud] à Plataforma usando a interface

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce Marketing Cloud] à Platform usando a interface do usuário:

* [Criar uma conexão de origem do Marketing Cloud do Salesforce na interface](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Criar um fluxo de dados para uma conexão de origem de automação de marketing na interface](../../tutorials/ui/dataflow/marketing-automation.md)

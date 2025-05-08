---
solution: Experience Platform
title: Visão geral do Salesforce Marketing Cloud Source
description: Saiba como conectar o Salesforce Marketing Cloud ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>A origem [!DNL Salesforce Marketing Cloud] será substituída em janeiro de 2026. Uma nova fonte será lançada ainda este ano como alternativa. Depois que a nova origem for lançada, você deverá planejar migrar para a nova origem criando novas conexões de conta e fluxos de dados antes do final de janeiro de 2026.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilação de dados de sistemas de automação de marketing de terceiros. O suporte para provedores de automação de marketing inclui [!DNL Salesforce Marketing Cloud].

## Pré-requisitos

Antes de poder conectar sua origem [!DNL Salesforce Marketing Cloud] à Experience Platform, você deve garantir que os **escopos de permissão** a seguir sejam provisionados para sua combinação de ID de cliente e segredo de cliente [!DNL Salesforce Marketing Cloud]:

* `campaign_read`
* `list_and_subscribers_read`

Você pode solicitar escopos fazendo uma chamada para o recurso `v2/userinfo` da API [!DNL Salesforce Marketing Cloud]. Consulte o [[!DNL Salesforce Marketing Cloud] documento Escopos de Permissão de Integração de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obter orientação sobre como solicitar e comparar escopos.

Para obter mais informações sobre escopos, incluindo uma lista de suas permissões e comportamentos relacionados, consulte este [[!DNL Salesforce Marketing Cloud] documento sobre API REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não tem suporte da integração de origem [!DNL Salesforce Marketing Cloud].

## INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

>[!WARNING]
>
>Incluir na lista de permissões Se você não adicionar os endereços IP necessários ao arquivo, a conta do [!DNL Salesforce Marketing Cloud] não será conectada ao Experience Platform.

## Conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando APIs:

* [Criar uma conexão básica do Salesforce Marketing Cloud usando a API do Serviço de fluxo](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de automação de marketing usando a API do Serviço de fluxo](../../tutorials/api/collect/marketing-automation.md)

## Conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando a interface

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando a interface do usuário:

* [Criar uma conexão de origem do Salesforce Marketing Cloud na interface](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Criar um fluxo de dados para uma conexão de origem de automação de marketing na interface](../../tutorials/ui/dataflow/marketing-automation.md)

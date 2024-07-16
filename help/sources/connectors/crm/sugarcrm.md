---
title: Visão geral do SugarCRM Source
description: Saiba como conectar o SugarCRM ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# [!DNL SugarCRM]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um aplicativo CRM de terceiros. O suporte para provedores de CRM inclui [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) é um sistema de gerenciamento de relacionamento com o cliente (CRM). A funcionalidade de [!DNL SugarCRM] inclui automação da força de vendas, campanhas de marketing, suporte ao cliente, colaboração, CRM móvel, CRM social e relatórios.

A fonte [!DNL SugarCRM] permite assimilar dados de contas, contatos e eventos dos seguintes pontos de extremidade de API:

* [Contas](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contatos](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Eventos](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

O [!DNL SugarCRM] usa tokens de portador como um mecanismo de autenticação para se comunicar com as APIs de Conta e Contato do [!DNL SugarCRM] e a API de Eventos do [!DNL SugarCRM].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos

Antes de criar uma conexão de origem [!DNL SugarCRM], primeiro verifique se você tem o seguinte:

* Uma conta [!DNL SugarMarket]. Você deve entrar em contato com o gerente de conta do [!DNL SugarCRM] para obter uma conta válida do [!DNL SugarMarket], caso ainda não tenha uma.

* Um nome de usuário e conta da API exclusivos, separados de qualquer conta de usuário associada ao processo de marketing ou vendas. Essa combinação exclusiva de nome de usuário e conta deve ter permissões de acesso à API. Para obter mais informações sobre o processo de configuração de uma conta, visite a documentação [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro).

## Conectar [!DNL SugarCRM Accounts & Contacts] à plataforma

* [Crie uma conexão de origem para trazer [!DNL SugarCRM Accounts & Contacts] dados para a Plataforma usando APIs](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Crie uma conexão de origem para trazer [!DNL SugarCRM Accounts & Contacts] dados para a Platform usando a interface de usuário](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)


## Conectar [!DNL SugarCRM Events] à plataforma

* [Crie uma conexão de origem para trazer [!DNL SugarCRM Events] dados para a Plataforma usando APIs](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Crie uma conexão de origem para trazer [!DNL SugarCRM Events] dados para a Platform usando a interface de usuário](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Criar um fluxo de dados para uma conexão de origem do CRM na interface](../../tutorials/ui/dataflow/crm.md)

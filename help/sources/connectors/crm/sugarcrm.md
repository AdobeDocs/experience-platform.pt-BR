---
title: Visão geral da origem do SugarCRM
description: Saiba como conectar o SugarCRM ao Adobe Experience Platform usando APIs ou a interface do usuário.
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# (Beta) [!DNL SugarCRM]

>[!NOTE]
>
>A variável [!DNL SugarCRM] a fonte está na versão beta. Consulte a [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um aplicativo CRM de terceiros. O suporte para provedores de CRM inclui [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) O é um sistema de CRM (relacionamento com o cliente). [!DNL SugarCRM]A funcionalidade da inclui automação da força de vendas, campanhas de marketing, suporte ao cliente, colaboração, CRM móvel, CRM social e relatórios.

A variável [!DNL SugarCRM] O source permite assimilar dados de contas, contatos e eventos dos seguintes endpoints de API:

* [Contas](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contatos](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Eventos](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] O usa tokens de portador como um mecanismo de autenticação para se comunicar com a [!DNL SugarCRM] APIs de conta e contato e a variável [!DNL SugarCRM] API de eventos.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos

Antes de criar um [!DNL SugarCRM] conexão de origem, você deve primeiro garantir que tenha o seguinte:

* A [!DNL SugarMarket] conta. Você deve entrar em contato com [!DNL SugarCRM] gerente de conta para obter uma conta válida [!DNL SugarMarket] conta caso ainda não tenha uma.

* Um nome de usuário e conta da API exclusivos, separados de qualquer conta de usuário associada ao processo de marketing ou vendas. Essa combinação exclusiva de nome de usuário e conta deve ter permissões de acesso à API. Para obter mais informações sobre o processo de configuração de uma conta, visite o [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) documentação.

## Conectar [!DNL SugarCRM Accounts & Contacts] para a Platform

* [Crie uma conexão de origem para trazer [!DNL SugarCRM Accounts & Contacts] dados para a Platform usando APIs](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Crie uma conexão de origem para trazer [!DNL SugarCRM Accounts & Contacts] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)


## Conectar [!DNL SugarCRM Events] para a Platform

* [Crie uma conexão de origem para trazer [!DNL SugarCRM Events] dados para a Platform usando APIs](../../tutorials/api/create/crm/sugarcrm-events.md).
* [Crie uma conexão de origem para trazer [!DNL SugarCRM Events] dados para a Platform usando a interface do usuário](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Criar um fluxo de dados para uma conexão de origem do CRM na interface](../../tutorials/ui/dataflow/crm.md)

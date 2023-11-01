---
title: Visão geral do Conector de origem do Zendesk
description: Saiba como conectar o Zendesk ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# [!DNL Zendesk]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um aplicativo de sucesso de clientes de terceiros. O suporte para provedores de sucesso do cliente inclui [!DNL Zendesk].

Esta Adobe Experience Platform [origens](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=pt-BR) utiliza o [API do Zendesk Search > Exportar resultados da pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) que retorna informações dos usuários para o Experience Platform do Zendesk para processamento adicional.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Autentique seu [!DNL Zendesk] account

[!DNL Zendesk] O usa tokens de portador como um mecanismo de autenticação para se comunicar com a [!DNL Zendesk] API.

Esta seção descreve as etapas de pré-requisito a serem concluídas para autenticar seu [!DNL Zendesk] conta.

* A primeira etapa na autenticação do [!DNL Zendesk] conta é para garantir que você tenha [!DNL Zendesk] conta de suporte. Se você ainda não tiver um, consulte o [[!DNL Zendesk] página de registro](https://www.zendesk.com/register/) para registrar e criar sua conta do Zendesk.
* Depois de se registrar com êxito, navegue até o [[!DNL Zendesk] site](https://www.zendesk.com/login/) e forneça seu **subdomínio**.
* Em seguida, selecione **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Por fim, recupere o token da API no **[!DNL API token]** seção.

![Token de API do Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulte a [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) para obter informações sobre como recuperar o subdomínio. Para obter informações sobre como gerar o token da API, consulte a [[!DNL Zendesk] guia sobre a geração de um novo token de API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

A documentação abaixo fornece informações sobre como se conectar [!DNL Zendesk] para a Platform usando APIs ou a interface do usuário:

## Conectar [!DNL Zendesk] para a Platform usando APIs

* [Criar uma conexão de origem e um fluxo de dados para [!DNL Zendesk] uso da API do Serviço de fluxo](../../tutorials/api/create/customer-success/zendesk.md)

## Conectar [!DNL Zendesk] para a Platform usando a interface

* [Criar um [!DNL Zendesk ]conexão de origem na interface](../../tutorials/ui/create/customer-success/zendesk.md)
* [Criar um fluxo de dados para uma conexão de origem de sucesso do cliente na interface](../../tutorials/ui/dataflow/customer-success.md)

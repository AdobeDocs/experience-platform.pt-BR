---
title: Visão geral do Zendesk Source Connector
description: Saiba como conectar o Zendesk ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 8%

---

# [!DNL Zendesk]

A Adobe Experience Platform permite a assimilação de dados de fontes externas, além de permitir estruturar, rotular e aprimorar os dados recebidos por meio dos serviços da Experience Platform. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

A Experience Platform oferece suporte para assimilação de dados de um aplicativo de sucesso de clientes de terceiros. O suporte para provedores de sucesso do cliente inclui [!DNL Zendesk].

Estas [fontes](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=pt-BR) do Adobe Experience Platform usam a [API do Zendesk Search > Exportar Resultados da Pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) que retorna informações dos usuários para o Experience Platform do Zendesk para processamento adicional.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

## Autentique sua conta do [!DNL Zendesk]

[!DNL Zendesk] usa tokens de portador como um mecanismo de autenticação para se comunicar com a API [!DNL Zendesk].

Esta seção descreve as etapas de pré-requisito a serem concluídas para autenticar sua conta do [!DNL Zendesk].

* A primeira etapa na autenticação da conta do [!DNL Zendesk] é verificar se você tem uma conta de suporte do [!DNL Zendesk]. Se você ainda não tiver uma, veja a [[!DNL Zendesk] página de registro](https://www.zendesk.com/register/) para registrar e criar sua conta do Zendesk.
* Depois de se registrar com êxito, navegue até o [[!DNL Zendesk] site](https://www.zendesk.com/login/) e forneça seu **subdomínio**.
* Em seguida, selecione **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Finalmente, recupere seu token de API da seção **[!DNL API token]**.

![Token de API do Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulte o [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) para obter informações sobre como recuperar o subdomínio. Para obter informações sobre como gerar o token da API, consulte o [[!DNL Zendesk] manual sobre como gerar um novo token de API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

A documentação abaixo fornece informações sobre como conectar o [!DNL Zendesk] ao Experience Platform usando APIs ou a interface do usuário:

## Conectar o [!DNL Zendesk] ao Experience Platform usando APIs

* [Criar uma conexão de origem e um fluxo de dados para  [!DNL Zendesk] usando a API de Serviço de Fluxo](../../tutorials/api/create/customer-success/zendesk.md)

## Conectar o [!DNL Zendesk] ao Experience Platform usando a interface

* [Criar uma conexão de origem  [!DNL Zendesk ] na interface](../../tutorials/ui/create/customer-success/zendesk.md)
* [Criar um fluxo de dados para uma conexão de origem de sucesso do cliente na interface](../../tutorials/ui/dataflow/customer-success.md)

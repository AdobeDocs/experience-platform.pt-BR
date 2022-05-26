---
keywords: Experience Platform, home, tópicos populares, Zendesk, zendesk
solution: Experience Platform
title: Visão geral do conector de origem do Zendesk
description: Saiba como conectar o Zendesk ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (Beta) [!DNL Zendesk]

>[!NOTE]
>
>O [!DNL Zendesk] A fonte está em beta. Consulte a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de um aplicativo de terceiros com sucesso do cliente. O suporte para provedores de sucesso do cliente inclui [!DNL Zendesk].

Este Adobe Experience Platform [fontes](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en) utiliza o [API de pesquisa do Zendesk > Exportar resultados de pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) que retorna informações dos usuários ao Experience Platform do Zendesk para processamento adicional.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Autentique seu [!DNL Zendesk] account

[!DNL Zendesk] O usa os tokens do portador como um mecanismo de autenticação para se comunicar com o [!DNL Zendesk] API.

Esta seção descreve as etapas de pré-requisito a serem concluídas para autenticar seu [!DNL Zendesk] conta.

* A primeira etapa para autenticar seu [!DNL Zendesk] para garantir que você [!DNL Zendesk] conta de suporte. Se você não tiver um já visualize o [[!DNL Zendesk]página de registro](https://www.zendesk.com/register/) para registrar e criar sua conta do Zendesk.
* Depois de se registrar com êxito, navegue até o [[!DNL Zendesk] site](https://www.zendesk.com/login/) e **subdomínio**.
* Em seguida, selecione **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Por fim, recupere o token de API do **[!DNL API token]** seção.

![Token de API do Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulte a [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) para obter informações sobre como recuperar o subdomínio. Para obter informações sobre a geração do token de API, consulte o [[!DNL Zendesk] guia sobre como gerar um novo token de API](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

A documentação abaixo fornece informações sobre como se conectar [!DNL Zendesk] para Plataforma usando APIs ou a interface do usuário:

## Connect [!DNL Zendesk] para Plataforma usando APIs

* [Criar uma conexão de origem e um fluxo de dados para [!DNL Zendesk] usando a API do Serviço de Fluxo](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] para Plataforma usando a interface do usuário

* [Crie um [!DNL Zendesk ]conexão de origem na interface do usuário](../../tutorials/ui/create/customer-success/zendesk.md)
* [Criar um fluxo de dados para uma conexão de origem de sucesso do cliente na interface do usuário](../../tutorials/ui/dataflow/customer-success.md)

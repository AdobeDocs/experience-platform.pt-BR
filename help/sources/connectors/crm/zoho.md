---
keywords: Experience Platform;página inicial;tópicos populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Visão geral do Conector Zoho CRM Source
description: Saiba como conectar o Zoho CRM ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!WARNING]
>
>A origem [!DNL Zoho CRM] será substituída no final de junho de 2025.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

A Experience Platform oferece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Zoho CRM].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Recuperar suas credenciais de autenticação para [!DNL Zoho CRM]

Antes de trazer dados de sua conta do [!DNL Zoho CRM] para a Experience Platform, você deve primeiro recuperar suas credenciais para autenticar sua fonte do [!DNL Zoho CRM]. Siga as etapas abaixo para recuperar a ID do cliente, o segredo do cliente, o token de acesso e o token de atualização.

### Registre seu aplicativo

A primeira etapa na recuperação das credenciais de autenticação é registrar o aplicativo usando o [[!DNL Zoho CRM] console do desenvolvedor](https://accounts.zoho.com/). Para registrar seu aplicativo, você deve selecionar o tipo de cliente em: Java Script, baseado na Web, móvel, aplicativos móveis que não são de navegador ou cliente próprio. Em seguida, forneça valores para o nome do seu aplicativo, a URL da sua página da Web e um URI de redirecionamento autorizado que [!DNL Zoho CRM] pode usar para redirecioná-lo com um token de concessão.

Um registro bem-sucedido retorna a ID do cliente e o segredo do cliente.

### Criar uma solicitação de autorização

Em seguida, você deve criar uma [solicitação de autorização](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) usando um aplicativo baseado na Web ou um autocliente. A solicitação de autorização retorna o token de concessão, que, por sua vez, permite recuperar o token de acesso.

Ao criar uma solicitação de autorização, você deve preencher valores para **escopos** e **tipos de acesso**. Consulte este [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) para obter mais informações sobre escopos, enquanto seu **tipo de acesso** deve sempre ser definido como `offline`.

### Gerar seus tokens de acesso e atualização

Depois de recuperar o token de concessão, você poderá gerar os [tokens de acesso e atualização](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) fazendo uma solicitação POST para `{ACCOUNTS_URL}/oauth/v2/token` enquanto fornece a ID do cliente, o segredo do cliente, o token de concessão e o URI de redirecionamento. Durante esta etapa, você também deve incluir `grant_type` como parâmetro e definir o valor como `"authorization_code"`.

Uma solicitação bem-sucedida retorna os tokens de acesso e atualização, que podem ser usados para autenticação.

Para obter etapas detalhadas sobre como adquirir suas credenciais, consulte o [[!DNL Zoho CRM] guia de autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conectar [!DNL Zoho CRM] a [!DNL Experience Platform] usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Zoho CRM] ao Experience Platform usando APIs ou a interface do usuário:

- [Criar uma conexão base  [!DNL Zoho CRM]  usando a API de Serviço de Fluxo](../../tutorials/api/create/crm/zoho.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Zoho CRM] a [!DNL Experience Platform] usando a interface

- [Criar uma conexão de origem  [!DNL Zoho CRM]  na interface](../../tutorials/ui/create/crm/zoho.md)
- [Criar um fluxo de dados para uma conexão de origem do CRM na interface](../../tutorials/ui/dataflow/crm.md)

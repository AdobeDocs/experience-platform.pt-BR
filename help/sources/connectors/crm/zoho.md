---
keywords: Experience Platform;página inicial;tópicos populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Visão geral do Conector de origem do Zoho CRM
description: Saiba como conectar o Zoho CRM ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando o [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de um sistema CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Zoho CRM].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Recuperar suas credenciais de autenticação para [!DNL Zoho CRM]

Antes que você possa trazer os dados de seu [!DNL Zoho CRM] para a Platform, você deve primeiro recuperar suas credenciais para autenticar sua [!DNL Zoho CRM] origem. Siga as etapas abaixo para recuperar a ID do cliente, o segredo do cliente, o token de acesso e o token de atualização.

### Registre seu aplicativo

A primeira etapa na recuperação de credenciais de autenticação é registrar o aplicativo usando o [[!DNL Zoho CRM] console do desenvolvedor](https://accounts.zoho.com/). Para registrar seu aplicativo, você deve selecionar o tipo de cliente em: Java Script, baseado na Web, móvel, aplicativos móveis que não são de navegador ou cliente próprio. Em seguida, forneça valores para o nome do aplicativo, o URL da página da Web e um URI de redirecionamento autorizado que [!DNL Zoho CRM] O pode então usar o para redirecioná-lo com um token de concessão.

Um registro bem-sucedido retorna a ID do cliente e o segredo do cliente.

### Criar uma solicitação de autorização

Em seguida, você deve criar um [solicitação de autorização](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) usando um aplicativo baseado na web ou um autocliente. A solicitação de autorização retorna o token de concessão, que, por sua vez, permite recuperar o token de acesso.

Ao criar uma solicitação de autorização, você deve preencher valores para ambos **escopos** e **tipo de acesso**. Consulte esta [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) para obter mais informações sobre escopos, enquanto as **tipo de acesso** deve ser sempre definido como `offline`.

### Gerar seus tokens de acesso e atualização

Depois de recuperar o token de concessão, você poderá gerar [tokens de acesso e atualização](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) fazendo uma solicitação POST para `{ACCOUNTS_URL}/oauth/v2/token` ao fornecer sua ID do cliente, segredo do cliente, token de concessão e URI de redirecionamento. Durante essa etapa, você também deve incluir `grant_type` como parâmetro e defina o valor como `"authorization_code"`.

Uma solicitação bem-sucedida retorna os tokens de acesso e atualização, que podem ser usados para autenticação.

Para obter etapas detalhadas sobre como adquirir suas credenciais, consulte [[!DNL Zoho CRM] guia de autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conectar [!DNL Zoho CRM] para [!DNL Platform] uso de APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Zoho CRM] para a Platform usando APIs ou a interface do usuário:

- [Criar um [!DNL Zoho CRM] conexão básica usando a API de serviço de fluxo](../../tutorials/api/create/crm/zoho.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Criar um fluxo de dados para uma origem de CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Zoho CRM] para [!DNL Platform] uso da interface

- [Criar um [!DNL Zoho CRM] conexão de origem na interface](../../tutorials/ui/create/crm/zoho.md)
- [Criar um fluxo de dados para uma conexão de origem do CRM na interface](../../tutorials/ui/dataflow/crm.md)

---
keywords: Experience Platform, home, tópicos populares, Zoho CRM, zoho crm, Zoho, zoho
solution: Experience Platform
title: Visão geral do conector de origem do Zoho CRM
topic-legacy: overview
description: Saiba como conectar o Zoho CRM ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform oferece suporte para assimilar dados de um sistema de CRM de terceiros. O suporte para provedores de CRM inclui [!DNL Zoho CRM].

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Recupere suas credenciais de autenticação para [!DNL Zoho CRM]

Antes de trazer os dados do [!DNL Zoho CRM] para a Platform, primeiro você deve recuperar suas credenciais para autenticar seu [!DNL Zoho CRM] fonte. Siga as etapas abaixo para recuperar a ID do cliente, o segredo do cliente, o token de acesso e o token de atualização.

### Registre seu aplicativo

A primeira etapa na recuperação de suas credenciais de autenticação é registrar seu aplicativo usando o [[!DNL Zoho CRM] console do desenvolvedor](https://accounts.zoho.com/). Para registrar seu aplicativo, você deve selecionar seu tipo de cliente em: Java Script, aplicativos móveis com base na Web, sem navegador ou clientes próprios. Em seguida, forneça valores para o nome do seu aplicativo, o URL da sua página da Web e um URI de redirecionamento autorizado que [!DNL Zoho CRM] pode usar para redirecionar você com um token de concessão.

Um registro bem-sucedido retorna a ID do cliente e o segredo do cliente.

### Criar uma solicitação de autorização

Em seguida, você deve criar um [pedido de autorização](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) usando um aplicativo baseado na web ou um autocliente. A solicitação de autorização retorna o token de concessão, que, por sua vez, permite recuperar o token de acesso.

Ao criar uma solicitação de autorização, você deve preencher os valores para **escopos** e **tipo de acesso**. Consulte esta [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) para obter mais informações sobre escopos, enquanto seus **tipo de acesso** deve ser sempre definido como `offline`.

### Gere seus tokens de acesso e atualização

Depois de recuperar o token de concessão, você poderá gerar [acessar e atualizar tokens](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) fazendo uma solicitação de POST para `{ACCOUNTS_URL}/oauth/v2/token` ao fornecer a ID do cliente, o segredo do cliente, o token de concessão e o URI de redirecionamento. Durante essa etapa, você também deve incluir `grant_type` como parâmetro e defina o valor como `"authorization_code"`.

Uma solicitação bem-sucedida retorna os tokens de acesso e atualização, que você pode usar para autenticar.

Para obter etapas detalhadas sobre como adquirir suas credenciais, consulte [[!DNL Zoho CRM] guia de autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connect [!DNL Zoho CRM] para [!DNL Platform] uso de APIs

A documentação abaixo fornece informações sobre como se conectar [!DNL Zoho CRM] para Plataforma usando APIs ou a interface do usuário:

- [Crie um [!DNL Zoho CRM] conexão básica usando a API do Serviço de Fluxo](../../tutorials/api/create/crm/zoho.md)
- [Explorar tabelas de dados usando a API do Serviço de fluxo](../../tutorials/api/explore/tabular.md)
- [Crie um fluxo de dados para uma fonte CRM usando a API do Serviço de Fluxo](../../tutorials/api/collect/crm.md)

## Connect [!DNL Zoho CRM] para [!DNL Platform] uso da interface do usuário

- [Crie um [!DNL Zoho CRM] conexão de origem na interface do usuário](../../tutorials/ui/create/crm/zoho.md)
- [Criar um fluxo de dados para uma conexão de origem do CRM na interface do usuário](../../tutorials/ui/dataflow/crm.md)

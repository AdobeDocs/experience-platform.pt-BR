---
title: Visão geral do Salesforce Marketing Cloud Source
description: Saiba como conectar o Salesforce Marketing Cloud ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>A origem [!DNL Salesforce Marketing Cloud] será substituída em janeiro de 2026. Uma nova fonte será lançada ainda este ano como alternativa. Depois que a nova origem for lançada, você deverá planejar migrar para a nova origem criando novas conexões de conta e fluxos de dados antes do final de janeiro de 2026.

O [!DNL Salesforce Marketing Cloud] capacita você a gerenciar e automatizar a participação do cliente em e-mails, dispositivos móveis, redes sociais e anúncios, tudo em uma única plataforma. Com ferramentas como o Email Studio, o Jornada Builder e o Audience Builder, você pode criar campanhas personalizadas e jornadas do cliente personalizadas para seu público-alvo.

Você pode usar a fonte [!DNL Salesforce Marketing Cloud] para conectar sua conta e trazer seus dados para a Adobe Experience Platform.

## Pré-requisitos

Antes de poder conectar sua origem [!DNL Salesforce Marketing Cloud] à Experience Platform, você deve garantir que os **escopos de permissão** a seguir sejam provisionados para sua combinação de ID de cliente e segredo de cliente [!DNL Salesforce Marketing Cloud]:

* `campaign_read`
* `list_and_subscribers_read`

Você pode solicitar escopos fazendo uma chamada para o recurso `v2/userinfo` da API [!DNL Salesforce Marketing Cloud]. Consulte o [[!DNL Salesforce Marketing Cloud] documento Escopos de Permissão de Integração de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obter orientação sobre como solicitar e comparar escopos.

Para obter mais informações sobre escopos, incluindo uma lista de suas permissões e comportamentos relacionados, consulte este [[!DNL Salesforce Marketing Cloud] documento sobre API REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>No momento, a assimilação de objetos personalizados não tem suporte da integração de origem [!DNL Salesforce Marketing Cloud].

### INCLUIR NA LISTA DE PERMISSÕES endereço IP

Você deve adicionar endereços IP específicos da sua região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

>[!WARNING]
>
>Incluir na lista de permissões Se você não adicionar os endereços IP necessários ao arquivo, a conta do [!DNL Salesforce Marketing Cloud] não será conectada ao Experience Platform.

### Autenticar para o Experience Platform no Azure {#azure}

Você deve fornecer valores para as credenciais a seguir para conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform em [!DNL Azure].

| Credencial | Descrição |
| --- | --- |
| Host | O servidor host do aplicativo. Esse geralmente é o seu subdomínio. **Observação:** ao inserir seu valor `host`, você precisa especificar o `{subdomain}.rest.marketingcloudapis.com`. Por exemplo, se a URL do host for `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, você deve inserir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` como valor do host. |
| ID de cliente | A ID do cliente associada ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| Segredo do cliente | O segredo do cliente associado ao aplicativo [!DNL Salesforce Marketing Cloud]. |
| ID de especificação da conexão | A **especificação de conexão** fornece as propriedades do conector de uma fonte de dados. Isso inclui detalhes como especificações de autenticação e requisitos para criar conexões de **base** e **origem**. Para [!DNL Salesforce Marketing Cloud], a ID de especificação da conexão é: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Observação:** esta credencial só é necessária durante a conexão via APIs. |

### Autenticar para o Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../landing/multi-cloud.md).

Você deve fornecer valores para as credenciais a seguir para conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform no AWS.

| Credencial | Descrição |
| --- | --- |
| Subdomínio | A parte exclusiva da URL da instância [!DNL Salesforce Marketing Cloud], usada para construir pontos de extremidade de API. |
| ID de cliente | Um identificador público do aplicativo, gerado ao criar um pacote instalado no [!DNL Salesforce Marketing Cloud] |
| Segredo do cliente | Uma chave confidencial associada à ID do cliente, também gerada no pacote instalado. |
| ID de especificação da conexão | A **especificação de conexão** fornece as propriedades do conector de uma fonte de dados. Isso inclui detalhes como especificações de autenticação e requisitos para criar conexões de **base** e **origem**. Para [!DNL Salesforce Marketing Cloud], a ID de especificação da conexão é: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Observação:** esta credencial só é necessária durante a conexão via APIs. |

Para obter mais informações, leia a [[!DNL Salesforce] documentação sobre o token de acesso para integrações de servidor para servidor](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando APIs

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando APIs:

* [Conectar  [!DNL Salesforce Marketing Cloud]  ao Experience Platform usando a API de Serviço de Fluxo](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
* [Criar um fluxo de dados para uma fonte de automação de marketing usando a API do Serviço de fluxo](../../tutorials/api/collect/marketing-automation.md)

## Conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando a interface

A documentação abaixo fornece informações sobre como conectar o [!DNL Salesforce Marketing Cloud] ao Experience Platform usando a interface do usuário:

* [Conectar [!DNL Salesforce Marketing Cloud] ao Experience Platform na interface](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Criar um fluxo de dados para uma conexão de origem de automação de marketing na interface](../../tutorials/ui/dataflow/marketing-automation.md)

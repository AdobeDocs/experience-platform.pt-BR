---
title: Visão geral do Salesforce Service Cloud Source Connector
description: Saiba como conectar a Salesforce Service Cloud ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# [!DNL Salesforce Service Cloud]

A [!DNL Salesforce Service Cloud] é uma plataforma de sucesso de clientes projetada para automatizar fluxos de trabalho de serviços e simplificar a comunicação entre as empresas e seus clientes. Ele consolida solicitações de vários canais, como email, telefone, mídia social e bate-papo em tempo real, em um console de agente unificado. Isso permite que as equipes de suporte gerenciem os &quot;casos&quot; com uma visão de 360 graus do histórico do cliente, garantindo que as respostas sejam personalizadas e eficientes, independentemente de como o cliente entre em contato.

Você pode usar o conector de origem [!DNL Salesforce Service Cloud] em Fontes do Adobe Experience Platform para conectar sua conta [!DNL Salesforce Service Cloud] e trazer seus dados para uso nos Serviços da Experience Platform.

Leia este documento para saber como você pode configurar sua conta do [!DNL Salesforce Service Cloud] e conectá-la à Experience Platform.

## Pré-requisitos {#prerequisites}

Leia esta seção para obter a configuração de pré-requisitos que você deve concluir para poder se conectar com êxito ao Experience Platform.

### INCLUO NA LISTA DE PERMISSÕES de endereços IP {#allowlist}

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

### Coletar credenciais necessárias {#credentials}

Você deve fornecer valores para as credenciais a seguir para conectar sua conta do [!DNL Salesforce Service Cloud] usando a Credencial do Cliente OAuth2.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | A URL da instância de origem [!DNL Salesforce Service Cloud]. |
| ID de cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce Service Cloud]. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce Service Cloud]. |
| Versão da API | A versão da API REST da instância [!DNL Salesforce Service Cloud] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce Service Cloud], leia o [[!DNL Salesforce Service Cloud] guia sobre Fluxos de Autorização do OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Conectar o [!DNL Salesforce Service Cloud] ao Experience Platform usando APIs

- [Criar uma conexão básica do Salesforce Service Cloud usando a API do Serviço de fluxo](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [Explorar tabelas de dados usando a API de Serviço de Fluxo](../../tutorials/api/explore/tabular.md)
- [Crie um fluxo de dados para uma fonte de sucesso do cliente usando a API do serviço de fluxo](../../tutorials/api/collect/customer-success.md)

## Conectar o [!DNL Salesforce Service Cloud] ao Experience Platform usando a interface

- [Criar uma conexão de origem do Salesforce Service Cloud na interface](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [Criar fluxo de dados para uma conexão de origem de sucesso do cliente na interface](../../tutorials/ui/dataflow/customer-success.md)

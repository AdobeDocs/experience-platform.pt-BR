---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Processamento de solicitação de privacidade no Perfil do cliente em tempo real
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Processamento de solicitação de privacidade no Perfil do cliente em tempo real

A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado pelas regulamentações de privacidade, como o Regulamento Geral de Proteção de Dados (RGPD) e o Ato de Privacidade do Consumidor da Califórnia (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para o Perfil de cliente em tempo real.

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes serviços de Experience Platform antes de ler este guia:

* [Privacy Service](home.md): Gerencia solicitações de clientes para acessar, opt out da venda ou excluir seus dados pessoais nos aplicativos da Adobe Experience Cloud.
* [Serviço](../identity-service/home.md)de identidade: Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [Perfil](../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

O Serviço de identidade do Adobe Experience Platform faz a ponte entre os dados de identidade do cliente nos sistemas e dispositivos. O Serviço de identidade usa namespaces **de** identidade para fornecer contexto aos valores de identidade relacionando-os ao seu sistema de origem. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma ID da Advertising Cloud da Adobe (&quot;AdCloud&quot;) ou uma ID da Adobe Target (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidas globalmente (padrão) e definidas pelo usuário (personalizadas). namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizadas para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade no Experience Platform, consulte a visão geral [da namespace de](../identity-service/namespaces.md)identidade.

## Enviando solicitações {#submit}

>[!NOTE]
>
>Esta seção aborda como criar solicitações de privacidade para o armazenamento de dados do Perfil. É altamente recomendável que você reveja a documentação da API [do](../privacy-service/api/getting-started.md) Privacy Service ou da interface do usuário [do](../privacy-service/ui/overview.md) Privacy Service para obter etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

A seção a seguir descreve como fazer solicitações de privacidade para o Perfil do cliente em tempo real e o Data Lake usando a API do Privacy Service ou a interface do usuário.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer `userIDs` um fornecido deve usar um arquivo específico `namespace` e `type` dependendo do armazenamento de dados ao qual se aplicam. As IDs do repositório de Perfis devem usar &quot;padrão&quot; ou &quot;personalizado&quot; para o seu `type` valor e uma namespace [de](#namespaces) identidade válida reconhecida pelo Serviço de identidade para o seu `namespace` valor.


Além disso, a `include` matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações para o Data Lake, a matriz deve incluir o valor &quot;ProfileService&quot;.

A solicitação a seguir cria um novo trabalho de privacidade para o Perfil de cliente em tempo real, usando a namespace de identidade &quot;Email&quot; padrão. Ele também inclui o valor do produto para o Perfil no `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Uso da interface

Ao criar solicitações de trabalho na interface do usuário, selecione **AEP Data Lake** e/ou **Perfil** em _Products_ para processar jobs para dados armazenados no Data Lake ou no Perfil Real-time Customer, respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Excluir processamento de solicitação

Quando o Experience Platform recebe uma solicitação de exclusão do Privacy Service, a Platform envia uma confirmação para o Privacy Service que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são removidos do Data Lake ou do repositório de Perfis em sete dias. Durante esse período de sete dias, os dados são excluídos por software e, portanto, não podem ser acessados por nenhum serviço da Platform.

Em versões futuras, a Platform enviará a confirmação ao Privacy Service depois que os dados forem fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no Experience Platform. É recomendável que você continue lendo a documentação fornecida em todo este guia para aprofundar sua compreensão sobre como gerenciar dados de identidade e criar trabalhos de privacidade.

Para obter informações sobre como processar solicitações de privacidade para recursos Platform não usados pelo Perfil, consulte o documento sobre processamento de solicitações de [privacidade no Data Lake](../catalog/privacy.md).
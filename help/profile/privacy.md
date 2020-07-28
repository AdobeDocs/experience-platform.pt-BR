---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Processamento de solicitação de privacidade no Perfil do cliente em tempo real
topic: overview
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---


# Processamento de solicitação de privacidade em [!DNL Real-time Customer Profile]

O Adobe Experience Platform [!DNL Privacy Service] processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado por regulamentos de privacidade, como o Regulamento Geral de Proteção de Dados (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Real-time Customer Profile].

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes [!DNL Experience Platform] serviços antes de ler este guia:

* [!DNL Privacy Service](home.md): Gerencia solicitações de clientes para acessar, opt out da venda ou excluir seus dados pessoais em aplicativos Adobe Experience Cloud.
* [!DNL Identity Service](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [!DNL Real-time Customer Profile](../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

O Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente nos sistemas e dispositivos. [!DNL Identity Service] usa namespaces **de** identidade para fornecer contexto aos valores de identidade relacionando-os ao seu sistema de origem. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma ID da Adobe Advertising Cloud (&quot;AdCloud&quot;) ou uma ID da Adobe Target (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidas globalmente (padrão) e definidas pelo usuário (personalizadas). namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizadas para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a visão geral [da namespace de](../identity-service/namespaces.md)identidade.

## Enviando solicitações {#submit}

>[!NOTE]
>
>Esta seção aborda como criar solicitações de privacidade para o armazenamento de [!DNL Profile] dados. É altamente recomendável que você reveja a documentação da API [do](../privacy-service/api/getting-started.md) Privacy Service ou da interface do usuário [do](../privacy-service/ui/overview.md) Privacy Service para obter etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

A seção a seguir descreve como fazer solicitações de privacidade para [!DNL Real-time Customer Profile] e o [!DNL Data Lake] uso da [!DNL Privacy Service] API ou da interface do usuário.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer `userIDs` um fornecido deve usar um arquivo específico `namespace` e `type` dependendo do armazenamento de dados ao qual se aplicam. As IDs da [!DNL Profile] loja devem usar &quot;padrão&quot; ou &quot;personalizado&quot; para o `type` valor, e uma namespace [de](#namespaces) identidade válida reconhecida pelo [!DNL Identity Service] `namespace` valor.


Além disso, a `include` matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações para o [!DNL Data Lake], a matriz deve incluir o valor &quot;ProfileService&quot;.

A solicitação a seguir cria um novo trabalho de privacidade para ambos [!DNL Real-time Customer Profile], usando a namespace de identidade &quot;Email&quot; padrão. Também inclui o valor do produto para [!DNL Profile] na `include` matriz:

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

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Perfil]** em _[!UICONTROL Products]_para processar jobs para dados armazenados no[!DNL Data Lake]ou[!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Excluir processamento de solicitação

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia uma confirmação para [!DNL Privacy Service] que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são removidos da loja [!DNL Data Lake] ou da [!DNL Profile] loja dentro de sete dias. Durante esse período de sete dias, os dados são apagados em modo suave e, portanto, não podem ser acessados por nenhum [!DNL Platform] serviço.

Em versões futuras, [!DNL Platform] enviará uma confirmação para [!DNL Privacy Service] depois que os dados tiverem sido fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Experience Platform]. É recomendável que você continue lendo a documentação fornecida em todo este guia para aprofundar sua compreensão sobre como gerenciar dados de identidade e criar trabalhos de privacidade.

Para obter informações sobre como processar solicitações de privacidade para [!DNL Platform] recursos não usados pelo, consulte o documento sobre processamento de solicitações de [!DNL Profile]privacidade no Data Lake [](../catalog/privacy.md).
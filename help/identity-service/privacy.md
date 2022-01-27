---
keywords: Experience Platform, home, tópicos populares
title: Processamento de solicitação de privacidade no Serviço de identidade
description: A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido por várias regulamentações de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade do Serviço de identidade.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: f0fa8d77e6184314056f8e70205a9b42409d09d5
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# Processamento de solicitação de privacidade em [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] processa solicitações de acesso, recusa de venda ou exclusão de seus dados pessoais pelo cliente, conforme definido pelas regulamentações de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade de [!DNL Identity Service] no Adobe Experience Platform.

>[!NOTE]
>
>Este guia só aborda como fazer solicitações de privacidade para o armazenamento de dados de identidade no Experience Platform. Se você também planeja fazer solicitações de privacidade para o Platform Data Lake ou [!DNL Real-time Customer Profile], consulte o guia em [processamento de solicitação de privacidade no Data Lake](../catalog/privacy.md) e ao guia sobre [processamento de solicitação de privacidade para Perfil](../profile/privacy.md) além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos Adobe Experience Cloud, consulte o [Documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introdução

É recomendável que você tenha uma compreensão funcional do seguinte [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gerencia solicitações de clientes para acessar, recusar a venda ou excluir seus dados pessoais nos aplicativos Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [[!DNL Real-time Customer Profile]](home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente em todos os sistemas e dispositivos. [!DNL Identity Service] uses **namespaces de identidade** fornecer contexto aos valores de identidade, relacionando-os com o seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizados). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte o [visão geral do namespace de identidade](../identity-service/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Identity Service] usando o [!DNL Privacy Service] API ou interface do usuário. Antes de ler essas seções, é altamente recomendável revisar a seção [API Privacy Service](../privacy-service/api/getting-started.md) ou [Interface do usuário do Privacy Service](../privacy-service/ui/overview.md) documentação para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados do usuário nas cargas de solicitação.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer ID fornecida em `userIDs` deve usar um `namespace` e `type`. Um [namespace de identidade](#namespaces) reconhecido por [!DNL Identity Service] devem ser previstas `namespace` , enquanto a variável `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

Além disso, a variável `include` a matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados em que a solicitação está sendo feita. Ao fazer solicitações para [!DNL Identity], a matriz deve incluir o valor `Identity`.

A solicitação a seguir cria um novo trabalho de privacidade sob o GDPR para os dados de um único cliente na [!DNL Identity] armazenar. Dois valores de identidade são fornecidos para o cliente na variável `userIDs` Array; uma usando a norma `Email` namespace de identidade e outro usando um `ECID` namespace, Também inclui o valor do produto para [!DNL Identity] (`Identity`) na `include` array:

>[!TIP]
>
>Ao excluir um namespace personalizado usando a API, você deve especificar o símbolo de identidade como namespace, em vez do nome de exibição.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### Uso da interface do usuário

>[!TIP]
>
>Ao excluir um namespace personalizado usando a interface do usuário, você deve especificar o símbolo de identidade como namespace, em vez do nome de exibição. Além disso, não é possível excluir namespaces personalizados na interface do usuário para sandboxes de não produção.

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL Identidade]** under **[!UICONTROL Produtos]** para processar tarefas para dados armazenados em [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Excluir processamento de solicitação

When [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia confirmação para [!DNL Privacy Service] que a solicitação foi recebida e os dados afetados foram marcados para exclusão. A exclusão da identidade individual é baseada no namespace e/ou no valor de ID fornecidos. Além disso, a exclusão ocorre para todas as sandboxes associadas a uma determinada Organização IMS.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Identity Service]. Para obter informações sobre o processamento de solicitações de privacidade de outras [!DNL Experience Cloud] aplicativos, consulte o documento em [[!DNL Privacy Service] and [!DNL Experience Cloud] aplicativos](../privacy-service/experience-cloud-apps.md).

---
keywords: Experience Platform;página inicial;tópicos populares
title: Processamento de solicitação de privacidade no serviço de identidade
description: O Adobe Experience Platform Privacy Service processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido por várias regulamentações de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade do Serviço de identidade.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 0%

---

# Processamento de solicitação de privacidade em [!DNL Identity Service]

O Adobe Experience Platform [!DNL Privacy Service] processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido pelos regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e o [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Identity Service] no Adobe Experience Platform.

>[!NOTE]
>
>Este guia aborda apenas como fazer solicitações de privacidade para o armazenamento de dados de identidade no Experience Platform. Se você também planeja fazer solicitações de privacidade para o data lake da Platform ou o [!DNL Real-Time Customer Profile], consulte o manual sobre [processamento de solicitações de privacidade no data lake](../catalog/privacy.md) e o manual sobre [processamento de solicitação de privacidade para o Perfil](../profile/privacy.md), além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos da Adobe Experience Cloud, consulte a [documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes serviços do [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): gerencia solicitações de clientes para acesso, cancelamento de venda ou exclusão de dados pessoais nos aplicativos da Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente, unindo as identidades em dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Compreensão dos namespaces de identidade {#namespaces}

O Adobe Experience Platform [!DNL Identity Service] une dados de identidade do cliente entre sistemas e dispositivos. [!DNL Identity Service] usa **namespaces de identidade** para fornecer contexto aos valores de identidade, relacionando-os ao seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizado). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a [visão geral sobre namespaces de identidade](../identity-service/features/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Identity Service] usando a API ou a interface do usuário [!DNL Privacy Service]. Antes de ler estas seções, é altamente recomendável que você consulte a documentação da [API de Privacy Service](../privacy-service/api/getting-started.md) ou da [Interface do usuário de Privacy Service](../privacy-service/ui/overview.md) para ver as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados do usuário nas cargas de solicitação.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer ID fornecida em `userIDs` deve usar um `namespace` e `type` específicos. Um [namespace de identidade](#namespaces) válido e reconhecido por [!DNL Identity Service] deve ser fornecido para o valor `namespace`, enquanto `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

Além disso, a matriz `include` da carga da solicitação deve incluir os valores de produto para os diferentes armazenamentos de dados para os quais a solicitação está sendo feita. Ao fazer solicitações para [!DNL Identity], a matriz deve incluir o valor `Identity`.

A solicitação a seguir cria um novo trabalho de privacidade no GDPR para os dados de um único cliente no armazenamento [!DNL Identity]. Dois valores de identidade são fornecidos para o cliente na matriz `userIDs`: um usando o namespace de identidade `Email` padrão e o outro usando um namespace `ECID`. Ele também inclui o valor do produto para [!DNL Identity] (`Identity`) na matriz `include`:

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

### Uso da interface

>[!TIP]
>
>Ao excluir um namespace personalizado usando a interface do usuário, você deve especificar o símbolo de identidade como namespace, em vez do nome de exibição. Além disso, não é possível excluir namespaces personalizados na interface do usuário para sandboxes de não produção.

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL Identidade]** em **[!UICONTROL Produtos]** para processar trabalhos para dados armazenados em [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Processamento de solicitação de exclusão

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia uma confirmação para [!DNL Privacy Service] de que a solicitação foi recebida e de que os dados afetados foram marcados para exclusão. A exclusão da identidade individual baseia-se no namespace e/ou valor de ID fornecido. Além disso, a exclusão ocorre para todas as sandboxes associadas a uma determinada organização.

Se você também incluiu o Perfil de Cliente em Tempo Real (`ProfileService`) e o data lake (`aepDataLake`) como produtos em sua solicitação de privacidade do Serviço de Identidade (`identity`), diferentes conjuntos de dados relacionados à identidade serão removidos do sistema em momentos potencialmente diferentes:

| Produtos incluídos | Efeitos |
| --- | --- |
| Somente `identity` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. O perfil construído a partir desse gráfico de identidade ainda permanece, mas não será atualizado à medida que novos dados são assimilados, pois as associações de identidade agora são removidas. Os dados associados ao perfil também permanecem no data lake. |
| `identity` e `ProfileService` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. Os dados associados ao perfil permanecem no data lake. |
| `identity` e `aepDataLake` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. O perfil construído a partir desse gráfico de identidade ainda permanece, mas não será atualizado à medida que novos dados são assimilados, pois as associações de identidade agora são removidas.<br><br>Quando o produto do data lake responder que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por nenhum serviço [!DNL Platform]. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |
| `identity`, `ProfileService` e `aepDataLake` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida.<br><br>Quando o produto do data lake responder que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por nenhum serviço [!DNL Platform]. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |

Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o rastreamento de status de trabalho.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Identity Service]. Para obter informações sobre como processar solicitações de privacidade para outros aplicativos do [!DNL Experience Cloud], consulte o documento em [[!DNL Privacy Service] e [!DNL Experience Cloud] aplicativos](../privacy-service/experience-cloud-apps.md).

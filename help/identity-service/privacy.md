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

# Processamento de solicitação de privacidade no [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] O processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Identity Service] no Adobe Experience Platform.

>[!NOTE]
>
>Este guia aborda apenas como fazer solicitações de privacidade para o armazenamento de dados de identidade no Experience Platform. Se você também planeja fazer solicitações de privacidade para o data lake ou [!DNL Real-Time Customer Profile], consulte o guia sobre [processamento de solicitação de privacidade no data lake](../catalog/privacy.md) e ao guia sobre [processamento de solicitação de privacidade para o Perfil](../profile/privacy.md) além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos da Adobe Experience Cloud, consulte o [Documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introdução

Recomenda-se que você tenha uma compreensão funcional do seguinte [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): gerencia as solicitações do cliente para acessar, cancelar a venda ou excluir seus dados pessoais nos aplicativos da Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): soluciona o desafio fundamental apresentado pela fragmentação dos dados de experiência do cliente, unindo identidades em dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

Adobe Experience Platform [!DNL Identity Service] conecta os dados de identidade do cliente entre sistemas e dispositivos. [!DNL Identity Service] usos **namespaces de identidade** para contextualizar os valores de identidade, relacionando-os com o seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizado). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade no [!DNL Experience Platform], consulte o [visão geral do namespace de identidade](../identity-service/features/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Identity Service] usando o [!DNL Privacy Service] API ou interface. Antes de ler essas seções, é altamente recomendável que você analise a [API PRIVACY SERVICE](../privacy-service/api/getting-started.md) ou [IU DO PRIVACY SERVICE](../privacy-service/ui/overview.md) documentação para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados do usuário nas cargas de solicitação.

### Uso da API

Ao criar solicitações de trabalho na API, as IDs fornecidas em `userIDs` deve usar um `namespace` e `type`. Um válido [namespace de identidade](#namespaces) reconhecido por [!DNL Identity Service] deve ser previsto para o `namespace` valor, enquanto a variável `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

Além disso, a `include` A matriz da carga da solicitação deve incluir os valores de produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações para [!DNL Identity], a matriz deve incluir o valor `Identity`.

A solicitação a seguir cria um novo processo de privacidade no GDPR para os dados de um único cliente na [!DNL Identity] armazenamento. Dois valores de identidade são fornecidos para o cliente na variável `userIDs` matriz; uma usando o padrão `Email` namespace de identidade e o outro usando um `ECID` também inclui o valor do produto para [!DNL Identity] (`Identity`) no `include` matriz:

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

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL Identidade]** em **[!UICONTROL Produtos]** para processar trabalhos de dados armazenados no [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Processamento de solicitação de exclusão

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia confirmação para [!DNL Privacy Service] que a solicitação foi recebida e que os dados afetados foram marcados para exclusão. A exclusão da identidade individual baseia-se no namespace e/ou valor de ID fornecido. Além disso, a exclusão ocorre para todas as sandboxes associadas a uma determinada organização.

Se você também incluiu o Perfil de cliente em tempo real (`ProfileService`) e o data lake (`aepDataLake`) como produtos em sua solicitação de privacidade do Serviço de identidade (`identity`), diferentes conjuntos de dados relacionados à identidade são removidos do sistema em momentos potencialmente diferentes:

| Produtos incluídos | Efeitos |
| --- | --- |
| `identity` somente | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. O perfil construído a partir desse gráfico de identidade ainda permanece, mas não será atualizado à medida que novos dados são assimilados, pois as associações de identidade agora são removidas. Os dados associados ao perfil também permanecem no data lake. |
| `identity` e `ProfileService` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. Os dados associados ao perfil permanecem no data lake. |
| `identity` e `aepDataLake` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. O perfil construído a partir desse gráfico de identidade ainda permanece, mas não será atualizado à medida que novos dados são assimilados, pois as associações de identidade agora são removidas.<br><br>Quando o produto do data lake responde que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |
| `identity`, `ProfileService`, e `aepDataLake` | A identidade fornecida é excluída assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida.<br><br>Quando o produto do data lake responde que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |

Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o rastreamento de status de tarefas.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Identity Service]. Para obter informações sobre o processamento de solicitações de privacidade de outros [!DNL Experience Cloud] aplicativos, consulte o documento sobre [[!DNL Privacy Service] e [!DNL Experience Cloud] aplicativos](../privacy-service/experience-cloud-apps.md).

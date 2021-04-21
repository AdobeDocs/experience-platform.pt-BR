---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Processamento de solicitação de privacidade no perfil do cliente em tempo real
topic-legacy: overview
type: Documentation
description: A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido por várias regulamentações de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade do Perfil do cliente em tempo real.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Processamento de solicitação de privacidade em [!DNL Real-time Customer Profile]

O Adobe Experience Platform [!DNL Privacy Service] processa as solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Real-time Customer Profile].

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes serviços [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](home.md): Gerencia solicitações de clientes para acessar, recusar a venda ou excluir seus dados pessoais nos aplicativos Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

O Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente e dos dispositivos. [!DNL Identity Service] O usa  **namespaces de** identidade para fornecer contexto aos valores de identidade ao relacioná-los ao seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizados). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a [visão geral do namespace de identidade](../identity-service/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Real-time Customer Profile] usando a API ou a interface do usuário [!DNL Privacy Service]. Antes de ler essas seções, é altamente recomendável revisar a documentação [Privacy Service API](../privacy-service/api/getting-started.md) ou [Privacy Service UI](../privacy-service/ui/overview.md) para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

>[!IMPORTANT]
>
>O Privacy Service só pode processar dados [!DNL Profile] usando uma política de mesclagem que não executa a compilação de identidade. Se estiver usando a interface do usuário para confirmar se suas solicitações de privacidade estão sendo processadas, verifique se você está usando uma política com &quot;[!DNL None]&quot; como seu tipo [!UICONTROL ID stitching]. Em outras palavras, não é possível usar uma política de mesclagem em que [!UICONTROL ID stitching] está definido como &quot;[!UICONTROL Private graph]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Também é importante observar que o tempo que uma solicitação de privacidade pode levar para ser concluída não pode ser garantido. Se ocorrerem alterações nos seus dados [!DNL Profile] enquanto uma solicitação ainda estiver em processamento, se esses registros forem processados também não poderá ser garantido.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer ID fornecida em `userIDs` deve usar um `namespace` e `type` específicos. Um [namespace de identidade](#namespaces) válido reconhecido por [!DNL Identity Service] deve ser fornecido para o valor `namespace`, enquanto `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

>[!NOTE]
>
>Talvez seja necessário fornecer mais de uma ID para cada cliente, dependendo do gráfico de identidade e de como os fragmentos de perfil são distribuídos nos conjuntos de dados da plataforma. Consulte a próxima seção [fragmentos de perfil](#fragments) para obter mais informações.

Além disso, a matriz `include` da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados em que a solicitação está sendo feita. Ao fazer solicitações para [!DNL Data Lake], a matriz deve incluir o valor &quot;ProfileService&quot;.

A solicitação a seguir cria um novo trabalho de privacidade para os dados de um único cliente no armazenamento [!DNL Profile]. Dois valores de identidade são fornecidos para o cliente na matriz `userIDs`; um usando o namespace de identidade padrão `Email` e o outro usando um namespace personalizado `Customer_ID`. Também inclui o valor do produto para [!DNL Profile] (`ProfileService`) na matriz `include`:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Uso da interface do usuário

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Profile]** em **[!UICONTROL Products]** para processar tarefas para dados armazenados no [!DNL Data Lake] ou [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Fragmentos de perfil em solicitações de privacidade {#fragments}

No armazenamento de dados [!DNL Profile], os dados pessoais de um cliente individual geralmente serão compostos de vários fragmentos de perfil, que estão associados à pessoa por meio do gráfico de identidade. Ao fazer solicitações de privacidade para o armazenamento [!DNL Profile], é importante observar que as solicitações são processadas somente no nível do fragmento de perfil, em vez do perfil inteiro.

Por exemplo, considere uma situação em que você está armazenando dados de atributos do cliente em três conjuntos de dados separados, que usam identificadores diferentes para associar esses dados a clientes individuais:

| Nome do conjunto de dados | Campo de identidade primária | Atributos armazenados |
| --- | --- | --- |
| Conjunto de dados 1 | `customer_id` | `address` |
| Conjunto de dados 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de dados 3 | `email_id` | `mlScore` |

Um dos conjuntos de dados usa `customer_id` como seu identificador principal, enquanto os outros dois usam `email_id`. Se você enviasse uma solicitação de privacidade (acesso ou exclusão) usando apenas `email_id` como o valor da ID do usuário, somente os atributos `firstName`, `lastName` e `mlScore` seriam processados, enquanto `address` não seria afetado.

Para garantir que suas solicitações de privacidade processem todos os atributos relevantes do cliente, você deve fornecer os principais valores de identidade para todos os conjuntos de dados aplicáveis, onde esses atributos podem ser armazenados (até no máximo nove IDs por cliente). Consulte a seção sobre campos de identidade nas [noções básicas da composição do schema](../xdm/schema/composition.md#identity) para obter mais informações sobre campos comumente marcados como identidades.

>[!NOTE]
>
>Se você estiver usando [sandboxes](../sandboxes/home.md) diferentes para armazenar seus dados [!DNL Profile], deverá fazer uma solicitação de privacidade separada para cada sandbox, indicando o nome da sandbox apropriado no cabeçalho `x-sandbox-name`.

## Excluir processamento de solicitação

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia a confirmação para [!DNL Privacy Service] de que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são removidos do armazenamento [!DNL Data Lake] ou [!DNL Profile] após a conclusão do trabalho de privacidade. Enquanto o trabalho de exclusão ainda está sendo processado, os dados são excluídos automaticamente e, portanto, não podem ser acessados por nenhum serviço [!DNL Platform]. Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o rastreamento dos status do trabalho.

>[!IMPORTANT]
>
>Embora uma solicitação de exclusão bem-sucedida remova os dados de atributo coletados para um cliente (ou conjunto de clientes), a solicitação não remove as associações estabelecidas no gráfico de identidade.
>
>Por exemplo, uma solicitação de exclusão que usa os `email_id` e `customer_id` do cliente remove todos os dados de atributos armazenados nessas IDs. No entanto, quaisquer dados que sejam assimilados posteriormente sob o mesmo `customer_id` ainda serão associados ao `email_id` apropriado, pois a associação ainda existe.

Em versões futuras, [!DNL Platform] enviará confirmação para [!DNL Privacy Service] depois que os dados forem fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade em [!DNL Experience Platform]. É recomendável continuar lendo a documentação fornecida neste guia para aprofundar sua compreensão de como gerenciar dados de identidade e criar tarefas de privacidade.

Para obter informações sobre o processamento de solicitações de privacidade para recursos [!DNL Platform] não usados por [!DNL Profile], consulte o documento sobre o processamento de [solicitação de privacidade no Data Lake](../catalog/privacy.md).

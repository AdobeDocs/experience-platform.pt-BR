---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Processamento de solicitação de privacidade no Perfil do cliente em tempo real
topic: overview
type: Documentation
description: A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado por várias regulamentações de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para o Perfil de cliente em tempo real.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# Processamento de solicitação de privacidade em [!DNL Real-time Customer Profile]

A Adobe Experience Platform [!DNL Privacy Service] processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado por regulamentos de privacidade, como o Regulamento Geral de Proteção de Dados (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Real-time Customer Profile].

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes serviços [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](home.md): Gerencia solicitações de clientes para acessar, opt out da venda ou excluir seus dados pessoais em aplicativos Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

A Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente e entre sistemas e dispositivos. [!DNL Identity Service] usa  **namespaces de** identidade para fornecer contexto aos valores de identidade relacionando-os ao seu sistema de origem. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidas globalmente (padrão) e definidas pelo usuário (personalizadas). Namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizadas para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a [visão geral da namespace de identidade](../identity-service/namespaces.md).

## Enviando solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Real-time Customer Profile] usando a API ou a interface do usuário [!DNL Privacy Service]. Antes de ler essas seções, é altamente recomendável revisar a documentação da [API do Privacy Service](../privacy-service/api/getting-started.md) ou [interface do usuário do Privacy Service](../privacy-service/ui/overview.md) para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário submetidos nas cargas de solicitação.

>[!IMPORTANT]
>
>O Privacy Service só pode processar [!DNL Profile] dados usando uma política de mesclagem que não executa identificação. Se você estiver usando a interface do usuário para confirmar se suas solicitações de privacidade estão sendo processadas, certifique-se de estar usando uma política com &quot;[!DNL None]&quot; como o tipo [!UICONTROL identificação]. Em outras palavras, não é possível usar uma política de mesclagem em que [!UICONTROL a identificação] está definida como &quot;[!UICONTROL Gráfico privado]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Também é importante observar que o tempo que uma solicitação de privacidade pode levar para ser concluída não pode ser garantido. Se ocorrerem alterações nos seus dados [!DNL Profile] enquanto uma solicitação ainda estiver sendo processada, o processamento desses registros também não poderá ser garantido.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer ID fornecida em `userIDs` deve usar um `namespace` e `type` específicos. Uma namespace de identidade [válida](#namespaces) reconhecida por [!DNL Identity Service] deve ser fornecida para o valor `namespace`, enquanto `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizadas, respectivamente).

>[!NOTE]
>
>Talvez seja necessário fornecer mais de uma ID para cada cliente, dependendo do gráfico de identidade e de como os fragmentos do perfil são distribuídos nos conjuntos de dados da plataforma. Consulte a próxima seção [fragmentos de perfil](#fragments) para obter mais informações.

Além disso, a matriz `include` da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações para [!DNL Data Lake], a matriz deve incluir o valor &quot;ProfileService&quot;.

A solicitação a seguir cria um novo trabalho de privacidade para os dados de um único cliente na loja [!DNL Profile]. Dois valores de identidade são fornecidos para o cliente na matriz `userIDs`; um usando a namespace de identidade padrão `Email` e o outro usando uma namespace personalizada `Customer_ID`. Também inclui o valor do produto para [!DNL Profile] (`ProfileService`) na matriz `include`:

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

### Uso da interface

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Perfil]** em **[!UICONTROL Products]** para processar tarefas para dados armazenados em [!DNL Data Lake] ou [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Fragmentos de perfil em solicitações de privacidade {#fragments}

No armazenamento de dados [!DNL Profile], os dados pessoais de um cliente individual serão muitas vezes compostos de vários fragmentos de perfil, que são associados à pessoa por meio do gráfico de identidade. Ao fazer solicitações de privacidade para a loja [!DNL Profile], é importante observar que as solicitações são processadas somente no nível do fragmento do perfil, em vez do perfil inteiro.

Por exemplo, considere uma situação em que você está armazenando dados de atributos do cliente em três conjuntos de dados separados, que usam identificadores diferentes para associar esses dados a clientes individuais:

| Nome do conjunto de dados | Campo de identidade principal | Atributos armazenados |
| --- | --- | --- |
| Conjunto de dados 1 | `customer_id` | `address` |
| Conjunto de dados 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de dados 3 | `email_id` | `mlScore` |

Um dos conjuntos de dados usa `customer_id` como seu identificador principal, enquanto os outros dois usam `email_id`. Se você enviasse uma solicitação de privacidade (acesso ou exclusão) usando apenas `email_id` como valor da ID do usuário, somente os atributos `firstName`, `lastName` e `mlScore` seriam processados, enquanto `address` não seriam afetados.

Para garantir que suas solicitações de privacidade processem todos os atributos relevantes do cliente, forneça os valores de identidade principais para todos os conjuntos de dados aplicáveis nos quais esses atributos possam ser armazenados (até no máximo nove IDs por cliente). Consulte a seção sobre campos de identidade nas [noções básicas de composição de schemas](../xdm/schema/composition.md#identity) para obter mais informações sobre campos que são comumente marcados como identidades.

>[!NOTE]
>
>Se você estiver usando [caixas de proteção](../sandboxes/home.md) diferentes para armazenar seus dados [!DNL Profile], é necessário fazer uma solicitação de privacidade separada para cada caixa de proteção, indicando o nome apropriado da caixa de proteção no cabeçalho `x-sandbox-name`.

## Excluir processamento de solicitação

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia a confirmação para [!DNL Privacy Service] de que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são removidos do armazenamento [!DNL Data Lake] ou [!DNL Profile] depois que o trabalho de privacidade for concluído. Enquanto o trabalho de exclusão ainda está sendo processado, os dados são excluídos por software e, portanto, não podem ser acessados por nenhum serviço [!DNL Platform]. Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre os status do trabalho de rastreamento.

>[!IMPORTANT]
>
>Enquanto uma solicitação de exclusão bem-sucedida remove os dados de atributo coletados para um cliente (ou conjunto de clientes), a solicitação não remove as associações estabelecidas no gráfico de identidade.
>
>Por exemplo, uma solicitação de exclusão que usa `email_id` e `customer_id` de um cliente remove todos os dados de atributos armazenados nessas IDs. No entanto, todos os dados que forem ingeridos posteriormente sob o mesmo `customer_id` ainda serão associados ao `email_id` apropriado, já que a associação ainda existe.

Em versões futuras, [!DNL Platform] enviará a confirmação para [!DNL Privacy Service] depois que os dados tiverem sido fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade em [!DNL Experience Platform]. É recomendável que você continue lendo a documentação fornecida em todo este guia para aprofundar sua compreensão sobre como gerenciar dados de identidade e criar trabalhos de privacidade.

Para obter informações sobre como processar solicitações de privacidade para recursos [!DNL Platform] não usados por [!DNL Profile], consulte o documento no processamento de [solicitação de privacidade no Data Lake](../catalog/privacy.md).
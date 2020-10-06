---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Processamento de solicitação de privacidade no Perfil do cliente em tempo real
topic: overview
translation-type: tm+mt
source-git-commit: f7abccb677294e1595fb35c27e03c30eb968082a
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---


# Processamento de solicitação de privacidade em [!DNL Real-time Customer Profile]

A Adobe Experience Platform [!DNL Privacy Service] processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado por regulamentos de privacidade, como o Regulamento Geral de Proteção de Dados (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Real-time Customer Profile].

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes [!DNL Experience Platform] serviços antes de ler este guia:

* [[!DNL Privacy Service]](home.md): Gerencia solicitações de clientes para acessar, opt out da venda ou excluir seus dados pessoais em aplicativos Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [[!DNL Perfil do cliente em tempo real]](../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

A Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente nos sistemas e dispositivos. [!DNL Identity Service] usa namespaces **de** identidade para fornecer contexto aos valores de identidade relacionando-os ao seu sistema de origem. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidas globalmente (padrão) e definidas pelo usuário (personalizadas). Namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizadas para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a visão geral [da namespace de](../identity-service/namespaces.md)identidade.

## Enviando solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Real-time Customer Profile] usar a [!DNL Privacy Service] API ou a interface do usuário. Antes de ler essas seções, é altamente recomendável revisar a documentação da API [do](../privacy-service/api/getting-started.md) Privacy Service ou da interface do usuário [do](../privacy-service/ui/overview.md) Privacy Service para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

>[!IMPORTANT]
>
>O Privacy Service só pode processar [!DNL Profile] dados usando uma política de mesclagem que não executa identificação. Se você estiver usando a interface do usuário para confirmar se suas solicitações de privacidade estão sendo processadas, verifique se você está usando uma política com &quot;[!DNL None]&quot; como o tipo de identificação [!UICONTROL da ID] . Em outras palavras, não é possível usar uma política de mesclagem em que a sutura [!UICONTROL de] ID está definida como &quot;Gráficoprivado&quot;.
>
>![](./images/privacy/no-id-stitch.png)

### Uso da API

Ao criar solicitações de trabalho na API, quaisquer IDs fornecidas dentro `userIDs` devem usar um `namespace` e `type`específicos. Uma namespace [de](#namespaces) identidade válida reconhecida pelo [!DNL Identity Service] deve ser fornecida para o `namespace` valor, enquanto o `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizadas, respectivamente).

>[!NOTE]
>
>Talvez seja necessário fornecer mais de uma ID para cada cliente, dependendo do gráfico de identidade e de como os fragmentos do perfil são distribuídos nos conjuntos de dados da plataforma. Consulte os fragmentos [do](#fragments) perfil da próxima seção para obter mais informações.

Além disso, a `include` matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações para o [!DNL Data Lake], a matriz deve incluir o valor &quot;ProfileService&quot;.

A solicitação a seguir cria uma nova tarefa de privacidade para os dados de um único cliente na [!DNL Profile] loja. Dois valores de identidade são fornecidos para o cliente no `userIDs` storage; um usando a namespace de `Email` identidade padrão e o outro usando uma `Customer_ID` namespace personalizada. Também inclui o valor do produto para [!DNL Profile] (`ProfileService`) na `include` matriz:

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

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Perfil]** em **[!UICONTROL Products]** para processar jobs para dados armazenados no [!DNL Data Lake] ou [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Fragmentos de perfil em solicitações de privacidade {#fragments}

No armazenamento de [!DNL Profile] dados, os dados pessoais de um cliente individual geralmente são compostos de vários fragmentos de perfil, que são associados à pessoa por meio do gráfico de identidade. Ao fazer solicitações de privacidade para a [!DNL Profile] loja, é importante observar que as solicitações são processadas somente no nível do fragmento do perfil, em vez do perfil inteiro.

Por exemplo, considere uma situação em que você está armazenando dados de atributos do cliente em três conjuntos de dados separados, que usam identificadores diferentes para associar esses dados a clientes individuais:

| Nome do conjunto de dados | Campo de identidade principal | Atributos armazenados |
| --- | --- | --- |
| Conjunto de dados 1 | `customer_id` | `address` |
| Conjunto de dados 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de dados 3 | `email_id` | `mlScore` |

Um dos conjuntos de dados usa `customer_id` como seu identificador principal, enquanto os outros dois usam `email_id`. Se você enviasse uma solicitação de privacidade (acesso ou exclusão) usando apenas `email_id` como valor da ID do usuário, somente os atributos `firstName`, `lastName`e `mlScore` seriam processados, enquanto não `address` seriam afetados.

Para garantir que suas solicitações de privacidade processem todos os atributos relevantes do cliente, forneça os valores de identidade principais para todos os conjuntos de dados aplicáveis nos quais esses atributos possam ser armazenados (até no máximo nove IDs por cliente). Consulte a seção sobre campos de identidade nas [noções básicas da composição](../xdm/schema/composition.md#identity) do schema para obter mais informações sobre campos que são comumente marcados como identidades.

>[!NOTE]
>
>Se você estiver usando [caixas de proteção](../sandboxes/home.md) diferentes para armazenar seus [!DNL Profile] dados, deverá fazer uma solicitação de privacidade separada para cada caixa de proteção, indicando o nome apropriado da caixa de proteção no `x-sandbox-name` cabeçalho.

## Excluir processamento de solicitação

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia uma confirmação para [!DNL Privacy Service] que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são removidos do repositório [!DNL Data Lake] ou da [!DNL Profile] loja após a conclusão do trabalho de privacidade. Enquanto o trabalho de exclusão ainda estiver sendo processado, os dados serão excluídos automaticamente e, portanto, não poderão ser acessados por nenhum [!DNL Platform] serviço. Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o status do job de rastreamento.

>[!IMPORTANT]
>
>Enquanto uma solicitação de exclusão bem-sucedida remove os dados de atributo coletados para um cliente (ou conjunto de clientes), a solicitação não remove as associações estabelecidas no gráfico de identidade.
>
>Por exemplo, uma solicitação de exclusão que usa um cliente `email_id` e `customer_id` remove todos os dados de atributo armazenados nessas IDs. No entanto, quaisquer dados posteriormente assimilados ao abrigo do mesmo `customer_id` serão ainda associados aos dados adequados `email_id`, uma vez que a associação ainda existe.

Em versões futuras, [!DNL Platform] enviará uma confirmação para [!DNL Privacy Service] depois que os dados tiverem sido fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Experience Platform]. É recomendável que você continue lendo a documentação fornecida em todo este guia para aprofundar sua compreensão sobre como gerenciar dados de identidade e criar trabalhos de privacidade.

Para obter informações sobre como processar solicitações de privacidade para [!DNL Platform] recursos não usados pelo, consulte o documento sobre processamento de solicitações de [!DNL Profile]privacidade no Data Lake [](../catalog/privacy.md).
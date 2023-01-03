---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Processamento de solicitação de privacidade no perfil do cliente em tempo real
type: Documentation
description: A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido por várias regulamentações de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade do Perfil do cliente em tempo real.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# Processamento de solicitação de privacidade em [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] processa solicitações de acesso, recusa de venda ou exclusão de seus dados pessoais pelo cliente, conforme definido pelas regulamentações de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade de [!DNL Real-Time Customer Profile] no Adobe Experience Platform.

>[!NOTE]
>
>Este guia só aborda como fazer solicitações de privacidade para o armazenamento de dados do perfil no Experience Platform. Se também planeja fazer solicitações de privacidade para o lago de dados da Plataforma, consulte o guia sobre [processamento de solicitação de privacidade no data lake](../catalog/privacy.md) além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos Adobe Experience Cloud, consulte o [Documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introdução

É recomendável que você tenha uma compreensão funcional do seguinte [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gerencia solicitações de clientes para acessar, recusar a venda ou excluir seus dados pessoais nos aplicativos Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente em todos os sistemas e dispositivos. [!DNL Identity Service] uses **namespaces de identidade** fornecer contexto aos valores de identidade, relacionando-os com o seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizados). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte o [visão geral do namespace de identidade](../identity-service/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Real-Time Customer Profile] usando o [!DNL Privacy Service] API ou interface do usuário. Antes de ler essas seções, é altamente recomendável revisar a seção [API Privacy Service](../privacy-service/api/getting-started.md) ou [Interface do usuário do Privacy Service](../privacy-service/ui/overview.md) documentação para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

>[!IMPORTANT]
>
>O Privacy Service só pode processar [!DNL Profile] dados que usam uma política de mesclagem que não executa a identificação. Consulte a seção sobre [limitações da política de mesclagem](#merge-policy-limitations) para obter mais informações.
>
>Também é importante observar que o tempo que uma solicitação de privacidade pode levar para ser concluída não pode ser garantido. Se ocorrerem alterações no [!DNL Profile] dados enquanto uma solicitação ainda está sendo processada, não é possível garantir se esses registros são processados ou não.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer ID fornecida em `userIDs` deve usar um `namespace` e `type`. Um [namespace de identidade](#namespaces) reconhecido por [!DNL Identity Service] devem ser previstas `namespace` , enquanto a variável `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

>[!NOTE]
>
>Talvez seja necessário fornecer mais de uma ID para cada cliente, dependendo do gráfico de identidade e de como os fragmentos de perfil são distribuídos nos conjuntos de dados da plataforma. Consulte a próxima seção [fragmentos de perfil](#fragments) para obter mais informações.

Além disso, a variável `include` a matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados em que a solicitação está sendo feita. Para excluir os dados de perfil associados a uma identidade, a matriz deve incluir o valor `ProfileService`. Para excluir as associações de gráficos de identidade do cliente, a matriz deve incluir o valor `identity`.

>[!NOTE]
>
>Consulte a seção sobre [solicitações de perfil e solicitações de identidade](#profile-v-identity) mais adiante neste documento para obter informações mais detalhadas sobre os efeitos da utilização de `ProfileService` e `identity` no `include` matriz.

A solicitação a seguir cria um novo trabalho de privacidade para os dados de um único cliente na [!DNL Profile] armazenar. Dois valores de identidade são fornecidos para o cliente na variável `userIDs` Array; uma usando a norma `Email` namespace de identidade e outro usando um `Customer_ID` namespace. Também inclui o valor do produto para [!DNL Profile] (`ProfileService`) na `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>A plataforma processa solicitações de privacidade em todas as [sandboxes](../sandboxes/home.md) pertencente à sua organização. Como resultado, qualquer `x-sandbox-name` o cabeçalho incluído na solicitação é ignorado pelo sistema.

### Uso da interface do usuário

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Perfil]** under **[!UICONTROL Produtos]** para processar trabalhos de dados armazenados no lago de dados ou [!DNL Real-Time Customer Profile], respectivamente.

![Uma solicitação de trabalho de acesso que está sendo criada na interface do usuário, com a opção Perfil selecionada em Produtos](./images/privacy/product-value.png)

## Fragmentos de perfil em solicitações de privacidade {#fragments}

No [!DNL Profile] armazenamento de dados, os dados pessoais de um cliente individual geralmente serão compostos de vários fragmentos de perfil, que estão associados à pessoa por meio do gráfico de identidade. Ao fazer solicitações de privacidade para a [!DNL Profile] , é importante observar que as solicitações são processadas somente no nível do fragmento de perfil, em vez do perfil inteiro.

Por exemplo, considere uma situação em que você está armazenando dados de atributos do cliente em três conjuntos de dados separados, que usam identificadores diferentes para associar esses dados a clientes individuais:

| Nome do conjunto de dados | Campo de identidade primária | Atributos armazenados |
| --- | --- | --- |
| Conjunto de dados 1 | `customer_id` | `address` |
| Conjunto de dados 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de dados 3 | `email_id` | `mlScore` |

Um dos conjuntos de dados usa `customer_id` como seu identificador principal, enquanto os outros dois usam `email_id`. Se você enviasse uma solicitação de privacidade (acesso ou exclusão) usando somente `email_id` como o valor da ID do usuário, somente a variável `firstName`, `lastName`e `mlScore` os atributos seriam processados, enquanto `address` não seria afetada.

Para garantir que suas solicitações de privacidade processem todos os atributos relevantes do cliente, você deve fornecer os principais valores de identidade para todos os conjuntos de dados aplicáveis, onde esses atributos podem ser armazenados (até no máximo nove IDs por cliente). Consulte a seção sobre campos de identidade na seção [noções básicas da composição do schema](../xdm/schema/composition.md#identity) para obter mais informações sobre campos comumente marcados como identidades.

## Excluir processamento de solicitação {#delete}

When [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia confirmação para [!DNL Privacy Service] que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são removidos após a conclusão do trabalho de privacidade.

Dependendo de você também ter incluído o Serviço de identidade (`identity`) e o lago de dados (`aepDataLake`) como produtos em sua solicitação de privacidade para Perfil (`ProfileService`), conjuntos diferentes de dados relacionados ao perfil são removidos do sistema em momentos potencialmente diferentes:

| Produtos incluídos | Efeitos |
| --- | --- |
| `ProfileService` only | O perfil é imediatamente excluído assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. No entanto, o gráfico de identidade do perfil ainda permanece, e o perfil pode ser reconstruído como novos dados com as mesmas identidades são assimilados. Os dados associados ao perfil também permanecem no lago de dados. |
| `ProfileService` e `identity` | O perfil e seu gráfico de identidade associado são imediatamente excluídos assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. Os dados associados ao perfil permanecem no lago de dados. |
| `ProfileService` e `aepDataLake` | O perfil é imediatamente excluído assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. No entanto, o gráfico de identidade do perfil ainda permanece, e o perfil pode ser reconstruído como novos dados com as mesmas identidades são assimilados.<br><br>Quando o produto do data lake responde que a solicitação foi recebida e está em processamento no momento, os dados associados ao perfil são excluídos automaticamente e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço. Uma vez concluída a tarefa, os dados são totalmente removidos do lago de dados. |
| `ProfileService`, `identity`, e `aepDataLake` | O perfil e seu gráfico de identidade associado são imediatamente excluídos assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida.<br><br>Quando o produto do data lake responde que a solicitação foi recebida e está em processamento no momento, os dados associados ao perfil são excluídos automaticamente e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço. Uma vez concluída a tarefa, os dados são totalmente removidos do lago de dados. |

Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o rastreamento de status de trabalho.

### Solicitações de perfil versus solicitações de identidade {#profile-v-identity}

Se uma solicitação de exclusão for feita para o Perfil (`ProfileService`), mas não Serviço de identidade (`identity`), o trabalho resultante remove os dados do atributo coletados para um cliente (ou conjunto de clientes), mas não remove as associações estabelecidas no gráfico de identidade.

Por exemplo, uma solicitação de exclusão que usa um `email_id` e `customer_id` remove todos os dados do atributo armazenados nessas IDs. Contudo, quaisquer dados que sejam posteriormente assimilados ao abrigo do mesmo `customer_id` ainda estará associada ao `email_id`, já que a associação ainda existe.

Para remover o perfil e todas as associações de identidade de um determinado cliente, inclua o Perfil e o Serviço de identidade como produtos de destino nas solicitações de exclusão.

### Limitações da política de mesclagem {#merge-policy-limitations}

O Privacy Service só pode processar [!DNL Profile] dados que usam uma política de mesclagem que não executa a identificação. Se você estiver usando a interface do usuário para confirmar se as solicitações de privacidade estão sendo processadas, verifique se está usando uma política com **[!DNL None]** como [!UICONTROL Compilação de ID] tipo . Em outras palavras, não é possível usar uma política de mesclagem em que [!UICONTROL Compilação de ID] está definida como [!UICONTROL Gráfico privado].
>![A identificação da política de mesclagem está definida como Nenhum](./images/privacy/no-id-stitch.png)
>
## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Experience Platform]. É recomendável continuar lendo a documentação fornecida neste guia para aprofundar sua compreensão de como gerenciar dados de identidade e criar tarefas de privacidade.

Para obter informações sobre o processamento de solicitações de privacidade de [!DNL Platform] recursos não usados por [!DNL Profile], consulte o documento em [processamento de solicitação de privacidade no data lake](../catalog/privacy.md).

---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Processamento de solicitação de privacidade no perfil do cliente em tempo real
type: Documentation
description: O Adobe Experience Platform Privacy Service processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido por várias regulamentações de privacidade. Este documento aborda os conceitos essenciais relacionados ao processamento de solicitações de privacidade para o Perfil do cliente em tempo real.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 0%

---

# Processamento de solicitação de privacidade em [!DNL Real-Time Customer Profile]

O Adobe Experience Platform [!DNL Privacy Service] processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido pelos regulamentos de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e o [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Real-Time Customer Profile] no Adobe Experience Platform.

>[!NOTE]
>
>Este guia aborda apenas como fazer solicitações de privacidade para o Armazenamento de dados do perfil no Experience Platform. Se você também planeja fazer solicitações de privacidade para o data lake da Platform, consulte o manual sobre [processamento de solicitações de privacidade no data lake](../catalog/privacy.md), além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos da Adobe Experience Cloud, consulte a [documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>A solicitação de privacidade neste guia **não** cobre entidades B2B não pessoais.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do [!DNL Platform]:

* [[!DNL Privacy Service]](../privacy-service/home.md): gerencia solicitações de clientes para acesso, cancelamento de venda ou exclusão de dados pessoais nos aplicativos da Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente, unindo as identidades em dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Compreensão dos namespaces de identidade {#namespaces}

O Adobe Experience Platform [!DNL Identity Service] une dados de identidade do cliente entre sistemas e dispositivos. [!DNL Identity Service] usa **namespaces de identidade** para fornecer contexto aos valores de identidade, relacionando-os ao seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizado). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a [visão geral sobre namespaces de identidade](../identity-service/features/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Real-Time Customer Profile] usando a API ou a interface do usuário [!DNL Privacy Service]. Antes de ler estas seções, revise ou esteja ciente da documentação da [API de Privacy Service](../privacy-service/api/getting-started.md) ou da [IU de Privacy Service](../privacy-service/ui/overview.md). Esses documentos fornecem etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados em cargas de solicitação.

>[!IMPORTANT]
>
>O Privacy Service só pode processar dados [!DNL Profile] usando uma política de mesclagem que não execute a identificação. Consulte a seção sobre [limitações da política de mesclagem](#merge-policy-limitations) para obter mais informações.
>
>Observe que as solicitações de privacidade são processadas de forma assíncrona dentro dos requisitos normativos, e o tempo necessário para a conclusão pode variar. Se ocorrerem alterações nos dados do [!DNL Profile] enquanto uma solicitação ainda estiver sendo processada, não há garantia de que esses registros de entrada também serão processados nessa solicitação. Somente os perfis mantidos no data lake ou no Armazenamento de perfis no momento em que o trabalho de privacidade é solicitado têm garantia de exclusão. Se você assimilar dados de perfil relacionados ao assunto de uma solicitação de exclusão durante o trabalho de exclusão, não há garantia de que todos os fragmentos de perfil serão excluídos.
>É sua responsabilidade estar ciente de qualquer dado recebido na plataforma ou no serviço de perfil no momento de uma solicitação de exclusão, pois esses dados serão inseridos em seus armazenamentos de registro. Você deve ser criterioso na assimilação de dados que foram ou estão sendo excluídos.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer ID fornecida em `userIDs` deve usar um `namespace` e `type` específicos. Um [namespace de identidade](#namespaces) válido e reconhecido por [!DNL Identity Service] deve ser fornecido para o valor `namespace`, enquanto `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

>[!NOTE]
>
>Talvez seja necessário fornecer mais de uma ID para cada cliente, dependendo do gráfico de identidade e de como os fragmentos de perfil são distribuídos nos conjuntos de dados da Platform. Consulte a próxima seção [fragmentos de perfil](#fragments) para obter mais informações.

Além disso, a matriz `include` da carga da solicitação deve incluir os valores de produto para os diferentes armazenamentos de dados para os quais a solicitação está sendo feita. Para excluir os dados de perfil associados a uma identidade, a matriz deve incluir o valor `ProfileService`. Para excluir as associações de gráficos de identidade do cliente, a matriz deve incluir o valor `identity`.

>[!NOTE]
>
>Consulte a seção sobre [solicitações de perfil e solicitações de identidade](#profile-v-identity) mais adiante neste documento para obter informações mais detalhadas sobre os efeitos do uso de `ProfileService` e `identity` dentro da matriz `include`.

A solicitação a seguir cria um novo trabalho de privacidade para os dados de um único cliente no armazenamento [!DNL Profile]. Dois valores de identidade são fornecidos para o cliente na matriz `userIDs`: um usando o namespace de identidade `Email` padrão e o outro usando um namespace `Customer_ID` personalizado. Também inclui o valor do produto para [!DNL Profile] (`ProfileService`) na matriz `include`:

**Solicitação**

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
>A Platform processa solicitações de privacidade em todas as [sandboxes](../sandboxes/home.md) pertencentes à sua organização. Como resultado, qualquer cabeçalho `x-sandbox-name` incluído na solicitação é ignorado pelo sistema.

**Resposta do produto**

Para o Serviço de perfil, após a conclusão do trabalho de privacidade, uma resposta é retornada no formato JSON com informações sobre as IDs de usuário solicitadas.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### Uso da interface

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL Data Lake da AEP]** e/ou **[!UICONTROL Perfil]** em **[!UICONTROL Produtos]** para processar trabalhos para dados armazenados no data lake ou [!DNL Real-Time Customer Profile], respectivamente.

![Uma solicitação de trabalho de acesso está sendo criada na interface do usuário, com a opção de Perfil selecionada em Produtos](./images/privacy/product-value.png)

## Fragmentos de perfil em solicitações de privacidade {#fragments}

No armazenamento de dados do [!DNL Profile], os dados pessoais de um cliente individual geralmente serão compostos de vários fragmentos de perfil, que são associados à pessoa por meio do gráfico de identidade. Ao fazer solicitações de privacidade para o armazenamento [!DNL Profile], é importante observar que as solicitações são processadas somente no nível do fragmento de perfil, em vez do perfil inteiro.

Por exemplo, considere uma situação em que você está armazenando dados do atributo do cliente em três conjuntos de dados separados, que usam identificadores diferentes para associar esses dados a clientes individuais:

| Nome do conjunto de dados | Campo de identidade principal | Atributos armazenados |
| --- | --- | --- |
| Conjunto de dados 1 | `customer_id` | `address` |
| Conjunto de dados 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de dados 3 | `email_id` | `mlScore` |

Um dos conjuntos de dados usa `customer_id` como seu identificador principal, enquanto os outros dois usam `email_id`. Se você enviasse uma solicitação de privacidade (acesso ou exclusão) usando apenas `email_id` como valor de ID de usuário, somente os atributos `firstName`, `lastName` e `mlScore` seriam processados, enquanto `address` não seria afetado.

Para garantir que suas solicitações de privacidade processem todos os atributos relevantes do cliente, você deve fornecer os valores de identidade principais para todos os conjuntos de dados aplicáveis nos quais esses atributos podem ser armazenados (até um máximo de nove IDs por cliente). Consulte a seção sobre campos de identidade em [noções básicas da composição de esquema](../xdm/schema/composition.md#identity) para obter mais informações sobre campos comumente marcados como identidades.

## Processamento de solicitação de exclusão {#delete}

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia uma confirmação para [!DNL Privacy Service] de que a solicitação foi recebida e de que os dados afetados foram marcados para exclusão. Os registros são removidos depois que o trabalho de privacidade é concluído.

>[!IMPORTANT]
>
>As solicitações de exclusão de privacidade não são instantâneas e podem variar dependendo dos serviços envolvidos e de outros fatores de impacto, como localização geográfica. O período para a conclusão de processos de privacidade pode variar de 15 a 45 dias, mas não é garantido.

Se você também incluiu o Serviço de Identidade (`identity`) e o data lake (`aepDataLake`) como produtos em sua solicitação de privacidade para o Perfil (`ProfileService`), diferentes conjuntos de dados relacionados ao perfil serão removidos do sistema em momentos potencialmente diferentes:

| Produtos incluídos | Efeitos |
| --- | --- |
| Somente `ProfileService` | O perfil é excluído imediatamente assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. No entanto, o gráfico de identidade do perfil ainda permanece e o perfil pode ser reconstruído à medida que novos dados com as mesmas identidades são assimilados. Os dados associados ao perfil também permanecem no data lake. |
| `ProfileService` e `identity` | O perfil e seu gráfico de identidade associado são excluídos imediatamente assim que o Platform envia a confirmação de que a solicitação de exclusão foi recebida. Os dados associados ao perfil permanecem no data lake. |
| `ProfileService` e `aepDataLake` | O perfil é excluído imediatamente assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. No entanto, o gráfico de identidade do perfil ainda permanece e o perfil pode ser reconstruído à medida que novos dados com as mesmas identidades são assimilados.<br><br>Quando o produto do data lake responder que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por nenhum serviço [!DNL Platform]. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |
| `ProfileService`, `identity` e `aepDataLake` | O perfil e seu gráfico de identidade associado são excluídos imediatamente assim que o Platform envia a confirmação de que a solicitação de exclusão foi recebida.<br><br>Quando o produto do data lake responder que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por nenhum serviço [!DNL Platform]. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |

Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o rastreamento de status de trabalho.

### Solicitações de perfil versus solicitações de identidade {#profile-v-identity}

Se uma solicitação de exclusão for feita para o Perfil (`ProfileService`), mas não para o Serviço de identidade (`identity`), o trabalho resultante removerá os dados de atributo coletados para um cliente (ou conjunto de clientes), mas não removerá as associações estabelecidas no gráfico de identidade.

Por exemplo, uma solicitação de exclusão que usa `email_id` e `customer_id` de um cliente remove todos os dados de atributos armazenados nessas IDs. No entanto, quaisquer dados que forem assimilados sob o mesmo `customer_id` ainda serão associados com o `email_id` apropriado, pois a associação ainda existe.

Para remover o perfil e todas as associações de identidade de um determinado cliente, certifique-se de incluir Perfil e Serviço de identidade como produtos de destino em suas solicitações de exclusão.

### Limitações da política de mesclagem {#merge-policy-limitations}

O Privacy Service só pode processar dados [!DNL Profile] usando uma política de mesclagem que não execute a identificação. Se você estiver usando a interface para confirmar se as solicitações de privacidade estão sendo processadas, verifique se está usando uma política com **[!DNL None]** como seu tipo [!UICONTROL identificação]. Em outras palavras, você não pode usar uma política de mesclagem em que a [!UICONTROL Compilação de ID] esteja definida como [!UICONTROL Gráfico privado].

>![A identificação da política de mesclagem está definida como Nenhum](./images/privacy/no-id-stitch.png)

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Experience Platform]. Para aprofundar sua compreensão de como gerenciar dados de identidade e criar processos de privacidade, continue lendo a documentação fornecida neste guia.

Para obter informações sobre o processamento de solicitações de privacidade para [!DNL Platform] recursos não usados pelo [!DNL Profile], consulte o documento sobre [processamento de solicitação de privacidade no data lake](../catalog/privacy.md).

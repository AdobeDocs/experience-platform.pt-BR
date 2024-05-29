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

# Processamento de solicitação de privacidade no [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] O processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para [!DNL Real-Time Customer Profile] no Adobe Experience Platform.

>[!NOTE]
>
>Este guia aborda apenas como fazer solicitações de privacidade para o Armazenamento de dados do perfil no Experience Platform. Se você também planeja fazer solicitações de privacidade para o data lake da Platform, consulte o guia em [processamento de solicitação de privacidade no data lake](../catalog/privacy.md) além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos da Adobe Experience Cloud, consulte o [Documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>A solicitação de privacidade neste guia não **não** Abranger entidades não pessoais B2B.

## Introdução

Este guia requer o entendimento prático do seguinte [!DNL Platform] componentes:

* [[!DNL Privacy Service]](../privacy-service/home.md): gerencia as solicitações do cliente para acessar, cancelar a venda ou excluir seus dados pessoais nos aplicativos da Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): soluciona o desafio fundamental apresentado pela fragmentação dos dados de experiência do cliente, unindo identidades em dispositivos e sistemas.
* [[!DNL Real-Time Customer Profile]](home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

## Noções básicas sobre namespaces de identidade {#namespaces}

Adobe Experience Platform [!DNL Identity Service] conecta os dados de identidade do cliente entre sistemas e dispositivos. [!DNL Identity Service] usos **namespaces de identidade** para contextualizar os valores de identidade, relacionando-os com o seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Serviço de identidade mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizado). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade no [!DNL Experience Platform], consulte o [visão geral do namespace de identidade](../identity-service/features/namespaces.md).

## Envio de solicitações {#submit}

As seções abaixo descrevem como fazer solicitações de privacidade para [!DNL Real-Time Customer Profile] usando o [!DNL Privacy Service] API ou interface. Antes de ler estas seções, você deve revisar ou estar ciente da [API PRIVACY SERVICE](../privacy-service/api/getting-started.md) ou [IU DO PRIVACY SERVICE](../privacy-service/ui/overview.md) documentação. Esses documentos fornecem etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados em cargas de solicitação.

>[!IMPORTANT]
>
>O Privacy Service só pode ser processado [!DNL Profile] dados usando uma política de mesclagem que não executa a compilação de identidade. Consulte a seção sobre [limitações da política de mesclagem](#merge-policy-limitations) para obter mais informações.
>
>Observe que as solicitações de privacidade são processadas de forma assíncrona dentro dos requisitos normativos, e o tempo necessário para a conclusão pode variar. Se ocorrerem alterações no [!DNL Profile] enquanto uma solicitação ainda está processando, não há garantia de que esses registros de entrada também serão processados nessa solicitação. Somente os perfis mantidos no data lake ou no Armazenamento de perfis no momento em que o trabalho de privacidade é solicitado têm garantia de exclusão. Se você assimilar dados de perfil relacionados ao assunto de uma solicitação de exclusão durante o trabalho de exclusão, não há garantia de que todos os fragmentos de perfil serão excluídos.
>É sua responsabilidade estar ciente de qualquer dado recebido na plataforma ou no serviço de perfil no momento de uma solicitação de exclusão, pois esses dados serão inseridos em seus armazenamentos de registro. Você deve ser criterioso na assimilação de dados que foram ou estão sendo excluídos.

### Uso da API

Ao criar solicitações de trabalho na API, as IDs fornecidas em `userIDs` deve usar um `namespace` e `type`. Um válido [namespace de identidade](#namespaces) reconhecido por [!DNL Identity Service] deve ser previsto para o `namespace` valor, enquanto a variável `type` deve ser `standard` ou `unregistered` (para namespaces padrão e personalizados, respectivamente).

>[!NOTE]
>
>Talvez seja necessário fornecer mais de uma ID para cada cliente, dependendo do gráfico de identidade e de como os fragmentos de perfil são distribuídos nos conjuntos de dados da Platform. Consulte a próxima seção [fragmentos de perfil](#fragments) para obter mais informações.

Além disso, a `include` A matriz da carga da solicitação deve incluir os valores de produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Para excluir os dados do perfil associados a uma identidade, a matriz deve incluir o valor `ProfileService`. Para excluir as associações de gráficos de identidade do cliente, a matriz deve incluir o valor `identity`.

>[!NOTE]
>
>Consulte a seção sobre [solicitações de perfil e solicitações de identidade](#profile-v-identity) mais adiante neste documento para obter informações mais detalhadas sobre os `ProfileService` e `identity` no prazo de `include` matriz.

A solicitação a seguir cria um novo trabalho de privacidade para os dados de um único cliente na [!DNL Profile] armazenamento. Dois valores de identidade são fornecidos para o cliente na variável `userIDs` matriz; uma usando o padrão `Email` namespace de identidade e o outro usando um espaço de nome `Customer_ID` namespace. Também inclui o valor do produto para [!DNL Profile] (`ProfileService`) no `include` matriz:

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
>A Platform processa solicitações de privacidade em todos os [sandboxes](../sandboxes/home.md) pertencente à sua organização. Como resultado, qualquer `x-sandbox-name` o cabeçalho incluído na solicitação é ignorado pelo sistema.

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

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL Data lake da AEP]** e/ou **[!UICONTROL Perfil]** em **[!UICONTROL Produtos]** para processar tarefas de dados armazenados no data lake ou [!DNL Real-Time Customer Profile], respectivamente.

![Uma solicitação de tarefa de acesso está sendo criada na interface do usuário, com a opção de perfil selecionada em Produtos](./images/privacy/product-value.png)

## Fragmentos de perfil em solicitações de privacidade {#fragments}

No [!DNL Profile] armazenamento de dados, os dados pessoais de um cliente individual serão frequentemente compostos de vários fragmentos de perfil, que são associados à pessoa por meio do gráfico de identidade. Ao fazer solicitações de privacidade para o [!DNL Profile] armazenamento, é importante observar que as solicitações são processadas somente no nível do perfil-fragmento, em vez do perfil inteiro.

Por exemplo, considere uma situação em que você está armazenando dados do atributo do cliente em três conjuntos de dados separados, que usam identificadores diferentes para associar esses dados a clientes individuais:

| Nome do conjunto de dados | Campo de identidade principal | Atributos armazenados |
| --- | --- | --- |
| Conjunto de dados 1 | `customer_id` | `address` |
| Conjunto de dados 2 | `email_id` | `firstName`, `lastName` |
| Conjunto de dados 3 | `email_id` | `mlScore` |

Um dos conjuntos de dados usa `customer_id` como seu identificador principal, enquanto os outros dois usam `email_id`. Se você enviasse uma solicitação de acesso a dados pessoais (acesso ou exclusão) usando apenas o `email_id` como o valor da ID do usuário, somente a variável `firstName`, `lastName`, e `mlScore` os atributos seriam processados, enquanto `address` não seria afetada.

Para garantir que suas solicitações de privacidade processem todos os atributos relevantes do cliente, você deve fornecer os valores de identidade principais para todos os conjuntos de dados aplicáveis nos quais esses atributos podem ser armazenados (até um máximo de nove IDs por cliente). Consulte a seção sobre campos de identidade na [noções básicas da composição do esquema](../xdm/schema/composition.md#identity) para obter mais informações sobre campos normalmente marcados como identidades.

## Processamento de solicitação de exclusão {#delete}

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia confirmação para [!DNL Privacy Service] que a solicitação foi recebida e que os dados afetados foram marcados para exclusão. Os registros são removidos depois que o trabalho de privacidade é concluído.

>[!IMPORTANT]
>
>As solicitações de exclusão de privacidade não são instantâneas e podem variar dependendo dos serviços envolvidos e de outros fatores de impacto, como localização geográfica. O período para a conclusão de processos de privacidade pode variar de 15 a 45 dias, mas não é garantido.

Se você também incluiu o Serviço de identidade (`identity`) e o data lake (`aepDataLake`) como produtos em sua solicitação de privacidade para o Perfil (`ProfileService`), diferentes conjuntos de dados relacionados ao perfil são removidos do sistema em momentos potencialmente diferentes:

| Produtos incluídos | Efeitos |
| --- | --- |
| `ProfileService` somente | O perfil é excluído imediatamente assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. No entanto, o gráfico de identidade do perfil ainda permanece e o perfil pode ser reconstruído à medida que novos dados com as mesmas identidades são assimilados. Os dados associados ao perfil também permanecem no data lake. |
| `ProfileService` e `identity` | O perfil e seu gráfico de identidade associado são excluídos imediatamente assim que o Platform envia a confirmação de que a solicitação de exclusão foi recebida. Os dados associados ao perfil permanecem no data lake. |
| `ProfileService` e `aepDataLake` | O perfil é excluído imediatamente assim que a Platform envia a confirmação de que a solicitação de exclusão foi recebida. No entanto, o gráfico de identidade do perfil ainda permanece e o perfil pode ser reconstruído à medida que novos dados com as mesmas identidades são assimilados.<br><br>Quando o produto do data lake responde que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |
| `ProfileService`, `identity`, e `aepDataLake` | O perfil e seu gráfico de identidade associado são excluídos imediatamente assim que o Platform envia a confirmação de que a solicitação de exclusão foi recebida.<br><br>Quando o produto do data lake responde que a solicitação foi recebida e está processando no momento, os dados associados ao perfil são excluídos por software e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço. Quando o trabalho for concluído, os dados serão removidos completamente do data lake. |

Consulte a [[!DNL Privacy Service] documentação](../privacy-service/home.md#monitor) para obter mais informações sobre o rastreamento de status de tarefas.

### Solicitações de perfil versus solicitações de identidade {#profile-v-identity}

Se uma solicitação de exclusão for feita para o Perfil (`ProfileService`), mas não o Serviço de identidade (`identity`), a tarefa resultante remove os dados de atributo coletados de um cliente (ou conjunto de clientes), mas não remove as associações estabelecidas no gráfico de identidade.

Por exemplo, uma solicitação de exclusão que usa o `email_id` e `customer_id` O remove todos os dados de atributos armazenados nessas IDs. No entanto, quaisquer dados que sejam posteriormente assimilados sob o mesmo `customer_id` continuará a ser associado às medidas adequadas `email_id`, pois a associação ainda existe.

Para remover o perfil e todas as associações de identidade de um determinado cliente, certifique-se de incluir Perfil e Serviço de identidade como produtos de destino em suas solicitações de exclusão.

### Limitações da política de mesclagem {#merge-policy-limitations}

O Privacy Service só pode ser processado [!DNL Profile] dados usando uma política de mesclagem que não executa a compilação de identidade. Se você estiver usando a interface do para confirmar se as solicitações de privacidade estão sendo processadas, verifique se está usando uma política com **[!DNL None]** como seu [!UICONTROL Identificação de ID] tipo. Em outras palavras, não é possível usar uma política de mesclagem em que [!UICONTROL Identificação de ID] está definida como [!UICONTROL Gráfico privado].

>![A identificação da política de mesclagem está definida como Nenhum](./images/privacy/no-id-stitch.png)

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade no [!DNL Experience Platform]. Para aprofundar sua compreensão de como gerenciar dados de identidade e criar processos de privacidade, continue lendo a documentação fornecida neste guia.

Para obter informações sobre o processamento de solicitações de privacidade de [!DNL Platform] recursos não usados por [!DNL Profile], consulte o documento sobre [processamento de solicitação de privacidade no data lake](../catalog/privacy.md).

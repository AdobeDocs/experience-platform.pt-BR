---
title: Guia flexível de avaliação de público-alvo
description: Saiba como usar a avaliação flexível de público para executar trabalhos de segmentação em lote sob demanda.
role: Developer, User
exl-id: b85bf735-be02-4bf7-bd63-8d74ae905e58
source-git-commit: 7a0a98ea035892943a0e9a9a2b059701f6f1f612
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 5%

---

# Guia flexível de avaliação do público-alvo

>[!AVAILABILITY]
>
>A avaliação de público flexível está **somente** disponível em instâncias do Experience Platform em execução em [!DNL Microsoft Azure]. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../landing/multi-cloud.md).
>
>Além disso, a avaliação flexível de público-alvo está **somente** disponível para uso com o Real-Time CDP B2C Edition.

A avaliação flexível do público-alvo permite executar um trabalho de segmentação em lote sob demanda. Com a avaliação flexível do público-alvo, você pode executar lançamentos de campanhas ad-hoc, comunicações just-in-time ou outras atividades sensíveis ao tempo.

## Medidas de proteção {#guardrails}

>[!CONTEXTUALHELP]
>id="platform_segmentation_browse_flexibleaudienceevaluation"
>title="Limites de avaliação de público-alvo flexível"
>abstract="Você pode avaliar até 20 públicos-alvo em uma única execução de avaliação de público-alvo flexível.<br/><br/>Além disso, embora o trabalho de avaliação seja executado o mais rápido possível, pode haver atrasos no sistema, pois as avaliações sob demanda <b>não podem</b> ser executadas simultaneamente com outra avaliação sob demanda ou em lote."

Ao executar a avaliação flexível do público-alvo, lembre-se das seguintes condições:

- Você só pode usar a avaliação de público flexível **duas vezes** por dia por sandbox. Esse limite é redefinido à meia-noite (UTC).
- Você tem um **máximo** de 50 execuções de avaliação de público flexível por ano por sandbox de **produção**.
- Você tem um **máximo** de 100 execuções de avaliação de público flexível por ano por sandbox de **desenvolvimento**.
- Todos os públicos-alvo **devem** ter uma origem de &quot;Serviço de segmentação&quot;.
- Todos os públicos-alvo **devem** ser avaliados usando a segmentação em lote.
- Todos os públicos-alvo **devem** ser baseados em pessoas.
- Você pode selecionar no máximo 20 públicos-alvo por execução de avaliação de público-alvo flexível.

>[!NOTE]
>
>Você pode adquirir execuções adicionais de avaliação de público-alvo flexível por ano. Para obter mais informações, entre em contato com o Atendimento ao cliente da Adobe.

## Acesso {#access}

Para usar a avaliação flexível do público-alvo, você deve ter a seguinte permissão:

- **[!UICONTROL Evaluate Segment to an Audience]** na seção **[!DNL Profile Management]**.

Para obter mais informações sobre o controle de acesso baseado em função, leia a [visão geral do controle de acesso](../../access-control/home.md).

## Execução de avaliação de público-alvo flexível

Você pode executar a avaliação flexível do público usando as APIs do Experience Platform ou a interface do usuário.

>[!BEGINTABS]

>[!TAB APIs do Experience Platform]

Para executar uma avaliação flexível do público-alvo nas APIs do Experience Platform, será necessário criar um trabalho de segmento que contenha as IDs de todas as definições de segmento (públicos-alvo) que você deseja avaliar.

>[!NOTE]
>
>Você só pode adicionar um **máximo** de 20 IDs de definição de segmento por chamada de API de trabalho de segmento.

Você pode criar um novo trabalho de segmento fazendo uma solicitação POST para o ponto de extremidade `/segment/jobs` e incluindo as IDs das definições de segmento no corpo da solicitação.

+++Um exemplo de solicitação para criar um novo trabalho de segmento

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentId` | A ID da definição de segmento que você deseja avaliar. Essas definições de segmento podem pertencer a diferentes políticas de mesclagem. |

+++

Uma resposta bem-sucedida retorna o status HTTP 200 com informações sobre o trabalho de segmento recém-criado.

+++ Um exemplo de resposta ao criar um novo trabalho de segmento.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

+++

Depois de criar o trabalho de segmento, você pode verificar seu status fazendo uma solicitação GET para o ponto de extremidade `/segment/jobs`, fornecendo a ID do trabalho de segmento recém-criado no caminho da solicitação.

+++Exemplo de solicitação para recuperar um trabalho de segmento

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Uma resposta bem-sucedida retorna o status HTTP 200 com informações detalhadas sobre o trabalho de segmento especificado.


+++ Uma resposta de amostra para recuperar um trabalho de segmento.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

+++

>[!TAB INTERFACE DO USUÁRIO DO Experience Platform]

Para executar a avaliação de público-alvo flexível na interface do Experience Platform, selecione **[!UICONTROL Audiences]** na seção **[!UICONTROL Customers]**.

![O botão Públicos-alvo na seção Clientes é destacado. O Portal de Público-Alvo para perfis de clientes é exibido.](../images/methods/fae/audience-portal.png)

O Portal de público-alvo é exibido, mostrando uma lista de todos os públicos-alvo de pessoas da organização. No Portal de público-alvo, você pode escolher os públicos que deseja avaliar e selecionar **[!UICONTROL Evaluate audience]**.

![Os públicos-alvo nos quais você deseja usar a avaliação de público-alvo flexível estão selecionados.](../images/methods/fae/evaluate-audiences.png)

O popover **[!UICONTROL Evaluate audiences on demand]** é exibido, exibindo a lista de públicos-alvo que serão avaliados com o trabalho do segmento sob demanda. Se um público-alvo não for elegível para avaliação sob demanda, ele será removido automaticamente do trabalho de avaliação. Confirme se os públicos-alvo listados são aqueles que você deseja avaliar.

![Os públicos-alvo que podem ser avaliados usando a avaliação de público-alvo flexível são exibidos.](../images/methods/fae/evaluate-audiences-modal.png)

Depois de confirmar que os públicos-alvo corretos estão listados, você pode continuar com a solicitação e a avaliação do público-alvo flexível será iniciada. Você pode exibir o status desta avaliação de público na [exibição do monitoramento do trabalho de avaliação](../../dataflows/ui/monitor-audiences.md#evaluation-job-details).

>[!NOTE]
>
>O status do trabalho do segmento pode ser relatado como no estado &quot;Em fila&quot; no painel de monitoramento. Você pode visualizar o status mais atualizado do trabalho do segmento fazendo uma solicitação GET para o ponto de extremidade `/segment/jobs`, fornecendo a ID do trabalho do segmento no caminho da solicitação. Mais informações sobre como usar esse endpoint podem ser encontradas na guia API.
>
>Se você executar a avaliação de público-alvo flexível e quiser que a avaliação ative o público-alvo para um destino, será necessário garantir que a frequência esteja definida como **[!UICONTROL After segment evaluation]**. Executar a avaliação flexível do público-alvo em públicos que já estão definidos para serem ativados [após a avaliação do segmento](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files), ativará os públicos-alvo assim que o trabalho de avaliação flexível do público-alvo for concluído, independentemente de quaisquer trabalhos de ativação diários anteriores.

>[!ENDTABS]

## Vídeo {#video}

O vídeo a seguir demonstra como acessar e usar a avaliação de público-alvo flexível no Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3453645?captions=por_br&)

## Perguntas frequentes {#faq}

A seção a seguir lista as perguntas frequentes relacionadas à avaliação flexível do público-alvo.

### Em quanto tempo posso ativar um público-alvo usando a avaliação flexível de públicos-alvo?

+++ Resposta

Você pode ativar um público-alvo usando a avaliação de público-alvo flexível imediatamente após sua criação.

+++

### Quanto tempo leva a avaliação flexível do público-alvo?

+++ Resposta

Um trabalho de avaliação de público-alvo flexível pode levar até quatro horas para ser concluído.

+++

### Posso executar o agendamento com avaliação de público-alvo flexível?

+++ Resposta

Não, o agendamento não está disponível para uso com a avaliação flexível de público.

+++

### Preciso executar um trabalho de exportação adicional ao usar a avaliação de público flexível?

+++ Resposta

Não, o trabalho de exportação é executado automaticamente após a conclusão do trabalho do segmento correspondente.

+++

### Quais serviços posso usar na avaliação de públicos-alvo com uma avaliação de público-alvo flexível?

+++ Resposta

Você pode usar públicos-alvo em todos os serviços downstream, incluindo destinos e jornadas do Adobe Journey Optimizer.

+++

### Quando os limites flexíveis de avaliação de público-alvo são redefinidos?

+++ Resposta

O limite diário é redefinido à meia-noite (UTC). O limite anual é redefinido na data de aniversário do contrato.

+++

### Quais tipos de público-alvo são compatíveis com a avaliação flexível do público-alvo?

+++ Resposta

Somente os públicos-alvo com a origem do Serviço de segmentação são compatíveis com a avaliação flexível do público-alvo. Outros públicos, como composições, upload personalizado ou Data Distiller, não são compatíveis com a avaliação flexível do público.

+++

### Quais execuções contribuem para minha contagem de execuções de avaliação de público flexível?

+++ Resposta

Execuções de avaliação de público flexíveis que foram criadas usando a API ou a interface do usuário contam para o limite máximo. No entanto, a execução diária do trabalho de segmentação em lotes que é executado à noite **não** contribui para esse limite.

+++

### Preciso avaliar todos os públicos-alvo dependentes ao avaliar o público-alvo principal com uma avaliação de público-alvo flexível?

+++ Resposta

Não. A avaliação flexível do público-alvo avaliará automaticamente todos os públicos-alvo dependentes. Por exemplo, se o Público-alvo A depender do Público-alvo B, você só precisará avaliar o Público-alvo B. Uma avaliação flexível do público-alvo avaliará automaticamente o Público-alvo A e depois o Público-alvo B.

+++

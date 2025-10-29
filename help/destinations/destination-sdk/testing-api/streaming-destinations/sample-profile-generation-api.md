---
description: Saiba como usar a API de teste de destino para gerar perfis de amostra para seu destino de transmissão, que você pode usar em testes de destino.
title: Gerar perfis de amostra com base em um esquema de origem
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# Gerar perfis de amostra com base em um esquema de origem {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade de API**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Esta página lista e descreve todas as operações de API que você pode executar usando o ponto de extremidade de API `/authoring/sample-profiles`.

## Gerar tipos de perfil diferentes para APIs diferentes {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Use esse endpoint de API para gerar perfis de amostra para dois casos de uso separados. É possível:
>
>* gere perfis a serem usados ao [criar e testar um modelo de transformação de mensagem](create-template.md) - usando a *ID de destino* como parâmetro de consulta.
>* gere perfis a serem usados ao fazer chamadas para [testar se o destino está configurado corretamente](streaming-destination-testing-overview.md) - usando a *ID da instância de destino* como parâmetro de consulta.

Você pode gerar perfis de amostra com base no esquema de origem XDM do Adobe (para usar ao testar o destino) ou no esquema de destino compatível com o destino (para usar ao criar o modelo). Para entender a diferença entre o esquema de origem e o esquema de destino do Adobe XDM, leia a seção de visão geral do artigo [Formato da mensagem](../../functionality/destination-server/message-format.md).

Observe que as finalidades para as quais os perfis de amostra podem ser usados não são intercambiáveis. Os perfis gerados com base na *ID de destino* só podem ser usados para criar seus modelos de transformação de mensagem, e os perfis gerados com base na *ID da instância de destino* só podem ser usados para testar seu ponto de extremidade de destino.

## Introdução a operações de API de geração de perfil de amostra {#get-started}

Antes de continuar, consulte o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Gerar perfis de amostra com base no esquema de origem a ser usado ao testar o destino {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Adicione os perfis de exemplo gerados aqui a chamadas HTTP ao [testar seu destino](streaming-destination-testing-overview.md).

Você pode gerar perfis de amostra com base no esquema de origem fazendo uma solicitação GET para o ponto de extremidade `authoring/sample-profiles/` e fornecendo a ID de uma instância de destino criada com base na configuração de destino que você deseja testar.

Para obter a ID de uma instância de destino, primeiro crie uma conexão na interface do usuário do Experience Platform com seu destino antes de tentar testar seu destino. Leia o [tutorial sobre ativação de destino](../../../ui/activation-overview.md) e veja a dica abaixo sobre como obter a ID de instância de destino a ser usada para esta API.

>[!IMPORTANT]
>
>* Para usar essa API, é necessário ter uma conexão existente com o destino na interface do usuário do Experience Platform. Leia [conectar ao destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) e [ativar perfis e públicos a um destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html) para obter mais informações.
>* Depois de estabelecer a conexão com seu destino, obtenha a ID da instância de destino que você deve usar em chamadas de API para este ponto de extremidade ao [navegar em uma conexão com seu destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>
>![Imagem da interface do usuário sobre como obter a ID da instância de destino](../../assets/testing-api/get-destination-instance-id.png)

**Formato da API**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Parâmetro da consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino com base na qual você está gerando perfis de amostra. |
| `{COUNT}` | *Opcional*. O número de perfis de amostra que você está gerando. O parâmetro pode assumir valores entre `1 - 1000`. <br> Se o parâmetro count não for especificado, o número padrão de perfis gerados será determinado pelo valor `maxUsersPerRequest` na [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Se essa propriedade não estiver definida, o Adobe gerará um perfil de amostra. |

{style="table-layout:auto"}


**Solicitação**

A solicitação a seguir gera perfis de exemplo, configurados pelos parâmetros de consulta `{DESTINATION_INSTANCE_ID}` e `{COUNT}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com o número especificado de perfis de amostra, com associação de público-alvo, identidades e atributos de perfil que correspondem ao esquema XDM de origem.

>[!TIP]
>
> A resposta retorna somente a associação de público-alvo, as identidades e os atributos de perfil que são usados na instância de destino. Mesmo se o esquema de origem tiver outros campos, eles serão ignorados.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentMembership` | Um objeto de mapa que descreve as associações de público-alvo do indivíduo. Para obter mais informações sobre `segmentMembership`, leia [Detalhes da Associação de Público-Alvo](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Um carimbo de data e hora da última vez que esse perfil se qualificou para o segmento. |
| `xdm:status` | Um campo de string que indica se a associação de público-alvo foi realizada como parte da solicitação atual. Os seguintes valores são aceitos: <ul><li>`realized`: O perfil faz parte do segmento.</li><li>`exited`: O perfil está saindo do público como parte da solicitação atual.</li></ul> |
| `identityMap` | Um campo do tipo mapa que descreve os vários valores de identidade para um indivíduo, juntamente com seus namespaces associados. Para obter mais informações sobre `identityMap`, leia [Base da composição do esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap). |

{style="table-layout:auto"}

## Gerar perfis de amostra com base no schema de destino a ser usado ao criar um template de transformação de mensagem {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Use os perfis de exemplo gerados aqui ao criar seu modelo, na [etapa de modelo de renderização](render-template-api.md#multiple-profiles-with-body).

Você pode gerar perfis de amostra com base no esquema de destino fazendo uma solicitação GET para o ponto de extremidade `authoring/sample-profiles/` e fornecendo a ID de destino da configuração de destino com base na qual você está criando seu modelo.

>[!TIP]
>
>* A ID de destino que você deve usar aqui é o `instanceId` que corresponde a uma configuração de destino, criada usando o ponto de extremidade `/destinations`. Consulte [recuperar uma configuração de destino](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) para obter mais detalhes.

**Formato da API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Parâmetro da consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID da configuração de destino com base na qual você está gerando perfis de amostra. |
| `{COUNT}` | *Opcional*. O número de perfis de amostra que você está gerando. O parâmetro pode assumir valores entre `1 - 1000`. <br> Se o parâmetro count não for especificado, o número padrão de perfis gerados será determinado pelo valor `maxUsersPerRequest` na [configuração do servidor de destino](../../authoring-api/destination-server/create-destination-server.md). Se essa propriedade não estiver definida, o Adobe gerará um perfil de amostra. |

{style="table-layout:auto"}

**Solicitação**

A solicitação a seguir gera perfis de exemplo, configurados pelos parâmetros de consulta `{DESTINATION_ID}` e `{COUNT}`.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com o número especificado de perfis de amostra, com associação de público-alvo, identidades e atributos de perfil que correspondem ao esquema XDM do público-alvo.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "realized"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API do Destination SDK seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como gerar perfis de amostra a serem usados ao [testar um modelo de transformação de mensagem](create-template.md) ou ao [testar se o destino está configurado corretamente](streaming-destination-testing-overview.md).

---
description: Esta página lista e descreve todas as operações da API que podem ser executadas usando o endpoint da API `/authoring/sample-profiles' para gerar perfis de amostra para usar em testes de destino.
title: Exemplos de operações da API de geração de perfil
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 3%

---

# Exemplos de operações da API de geração de perfil {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Ponto de extremidade da API**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Esta página lista e descreve todas as operações de API que você pode executar usando o `/authoring/sample-profiles` Ponto de extremidade da API.

## Gerar diferentes tipos de perfil para APIs diferentes {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Use esse ponto de extremidade de API para gerar perfis de amostra para dois casos de uso separados. Você pode:
>* gerar perfis para usar quando [criação e teste de um template de transformação de mensagem](./create-template.md) - utilizando *ID de destino* como parâmetro de consulta.
>* gerar perfis para usar ao fazer chamadas para [teste se o destino está configurado corretamente](./test-destination.md) - utilizando *ID da instância de destino* como parâmetro de consulta.


Você pode gerar perfis de amostra com base no esquema de origem Adobe XDM (para usar ao testar seu destino) ou no esquema de destino compatível com seu destino (para usar ao criar seu modelo). Para entender a diferença entre o schema de origem Adobe XDM e o schema de destino, leia a seção de visão geral do [Formato de mensagem](./message-format.md) artigo 10. o

Observe que as finalidades para as quais os perfis de amostra podem ser usados não são permutáveis. Perfis gerados com base no *ID de destino* só podem ser usados para criar os modelos e perfis de transformação de mensagem gerados com base na variável *ID da instância de destino* O só pode ser usado para testar o terminal de destino.

## Introdução a operações de API de geração de perfil de amostra {#get-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Gere perfis de amostra com base no schema de origem a ser usado ao testar seu destino {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Adicione os perfis de amostra gerados aqui para chamadas HTTP quando [teste do destino](./test-destination.md).

Você pode gerar perfis de amostra com base no schema de origem, fazendo uma solicitação de GET para o `authoring/sample-profiles/` endpoint e fornecer a ID de uma instância de destino criada com base na configuração de destino que você deseja testar.

Para obter a ID de uma instância de destino, primeiro crie uma conexão na interface do usuário do Experience Platform para o destino antes de tentar testar o destino. Leia o [tutorial ativar destino](/help/destinations/ui/activation-overview.md) e consulte a dica abaixo sobre como obter a ID da instância de destinos a ser usada para essa API.

>[!TIP]
>
>* Obtenha a ID da instância de destino que deve ser usada aqui a partir do URL ao navegar por uma conexão com seu destino.
   >![Imagem da interface do usuário como obter a ID da instância de destino](./assets/get-destination-instance-id.png)


**Formato da API**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Parâmetro de consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | A ID da instância de destino com base na qual você está gerando perfis de amostra. |
| `{COUNT}` | *Opcional*. O número de perfis de amostra que você está gerando. O parâmetro pode ter valores entre `1 - 1000`. <br> Se o parâmetro de contagem não for especificado, o número padrão de perfis gerados será determinado pela variável `maxUsersPerRequest` na variável [configuração do servidor de destino](./destination-server-api.md#create). Se essa propriedade não estiver definida, o Adobe gerará um perfil de amostra. |

{style=&quot;table-layout:auto&quot;}


**Solicitação**

A solicitação a seguir gera perfis de amostra, configurados pela variável `{DESTINATION_INSTANCE_ID}` e `{COUNT}` parâmetros de consulta.

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

Uma resposta bem-sucedida retorna o status HTTP 200 com o número especificado de perfis de amostra, com associação de segmento, identidades e atributos de perfil que correspondem ao esquema XDM de origem.

>[!TIP]
>
> A resposta retorna somente associação de segmento, identidades e atributos de perfil que são usados na instância de destino. Mesmo que o schema de origem tenha outros campos, eles serão ignorados.

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
| `segmentMembership` | Um objeto de mapa que descreve as associações de segmento de cada indivíduo. Para obter mais informações sobre `segmentMembership`, ler [Detalhes da associação ao segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Um carimbo de data e hora da última vez que esse perfil se qualificou para o segmento. |
| `xdm:status` | Indica se a associação de segmento foi realizada como parte da solicitação atual. Os seguintes valores são aceitos: <ul><li>`existing`: O perfil já fazia parte do segmento antes da solicitação e continua mantendo sua associação.</li><li>`realized`: O perfil está inserindo o segmento como parte da solicitação atual.</li><li>`exited`: O perfil está saindo do segmento como parte da solicitação atual.</li></ul> |
| `identityMap` | Um campo do tipo mapa que descreve os vários valores de identidade de um indivíduo, juntamente com seus namespaces associados. Para obter mais informações sobre `identityMap`, ler [Base da composição do schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Gerar perfis de amostra com base no schema de destino para usar ao criar um template de transformação de mensagem {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Use os perfis de amostra gerados aqui ao criar seu modelo no [etapa do modelo de renderização](./render-template-api.md#multiple-profiles-with-body).

Você pode gerar perfis de amostra com base no schema de destino fazendo uma solicitação de GET para o `authoring/sample-profiles/` endpoint e fornecer a ID de destino da configuração de destino com base na qual você está criando o modelo.

>[!TIP]
>
>* A ID de destino que você deve usar aqui é a variável `instanceId` que corresponde a uma configuração de destino, criada usando o `/destinations` endpoint . Consulte a [referência da API de configuração de destino](./destination-configuration-api.md#retrieve-list).


**Formato da API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Parâmetro de consulta | Descrição |
| -------- | ----------- |
| `{DESTINATION_ID}` | A ID da configuração de destino com base na qual você está gerando perfis de amostra. |
| `{COUNT}` | *Opcional*. O número de perfis de amostra que você está gerando. O parâmetro pode ter valores entre `1 - 1000`. <br> Se o parâmetro de contagem não for especificado, o número padrão de perfis gerados será determinado pela variável `maxUsersPerRequest` na variável [configuração do servidor de destino](./destination-server-api.md#create). Se essa propriedade não estiver definida, o Adobe gerará um perfil de amostra. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir gera perfis de amostra, configurados pela variável `{DESTINATION_ID}` e `{COUNT}` parâmetros de consulta.

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

Uma resposta bem-sucedida retorna o status HTTP 200 com o número especificado de perfis de amostra, com associação de segmento, identidades e atributos de perfil que correspondem ao esquema XDM de destino.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
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
                    "status": "existing"
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
                    "status": "existing"
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

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Depois de ler este documento, você agora sabe como gerar perfis de amostra para serem usados ao [teste de um template de transformação de mensagem](./create-template.md) ou quando [teste se o destino está configurado corretamente](./test-destination.md).

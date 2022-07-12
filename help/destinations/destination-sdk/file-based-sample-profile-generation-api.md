---
description: Esta página explica como usar o endpoint da API /sample-profiles do Destination SDK para gerar perfis de amostra com base em um schema de origem. Você pode usar essas amostras de perfis para testar sua configuração de destino baseada em arquivo.
title: Gerar perfis de amostra com base em um schema de origem
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---


# Gerar perfis de amostra com base em um schema de origem

## Visão geral {#overview}

A primeira etapa para testar o destino baseado em arquivo é usar a variável `/sample-profiles` endpoint para gerar um perfil de amostra com base no esquema de origem existente.

Os perfis de amostra podem ajudar você a entender a estrutura JSON de um perfil. Além disso, elas fornecem um padrão que você pode personalizar com seus próprios dados de perfil, para testes de destino adicionais.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](./getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas para a API com sucesso, incluindo como obter a permissão de criação de destino necessária e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de usar a variável `/sample-profiles` , certifique-se de atender às seguintes condições:

* Você tem um destino com base em arquivo existente criado por meio do Destination SDK e pode vê-lo em seu [catálogo de destinos](../ui/destinations-workspace.md).
* Você criou pelo menos um fluxo de ativação para o seu destino na interface do usuário do Experience Platform. O `/sample-profiles` o endpoint cria os perfis com base no schema de origem definido no fluxo de ativação. Consulte a [tutorial de ativação](../ui/activate-batch-profile-destinations.md) para saber como criar um fluxo de ativação.
* Para fazer a solicitação da API com êxito, é necessário a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, do URL, ao navegar em uma conexão com seu destino na interface do usuário da plataforma.

   ![Imagem da interface do usuário que mostra como obter a ID da instância de destino do URL.](assets/get-destination-instance-id.png)

## Gerar perfis de amostra para teste de destino {#generate-sample-profiles}

Você pode gerar perfis de amostra com base no seu schema de origem, fazendo uma solicitação de GET para a variável `/sample-profiles` endpoint com a ID da instância de destino do destino que você deseja testar.

**Formato da API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parâmetros de consulta | Descrição |
| -------- | ----------- |
| `destinationInstanceId` | A ID da instância de destino para a qual você está gerando perfis de amostra. Consulte a [pré-requisitos](#prerequisites) para obter detalhes sobre como obter essa ID. |
| `count` | *Opcional*. O número de perfis de amostra que você deseja gerar. O parâmetro pode ter valores entre `1 - 1000`. Se essa propriedade não estiver definida, a API gerará um único perfil de amostra. |

**Solicitação**

A solicitação a seguir gera um perfil de amostra com base no schema de origem definido na instância de destino com o `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com o número especificado de perfis de amostra, com associação de segmento, identidades e atributos de perfil que correspondem ao esquema XDM de origem.

>[!NOTE]
>
> A resposta retorna somente associação de segmento, identidades e atributos de perfil que são usados na instância de destino. Mesmo que o schema de origem tenha outros campos, eles serão ignorados.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![Imagem que mostra o mapeamento da interface do usuário para os campos da resposta da API.](assets/sample-api-response-mapping.png)

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentMembership` | Um objeto de mapa que descreve as associações de segmento de cada indivíduo. Para obter mais informações sobre `segmentMembership`, ler [Detalhes da associação ao segmento](../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Um carimbo de data e hora da última vez que esse perfil se qualificou para o segmento. |
| `status` | Indica se a associação de segmento foi realizada como parte da solicitação atual. Os seguintes valores são aceitos: <ul><li>`existing`: O perfil já fazia parte do segmento antes da solicitação e continua mantendo sua associação.</li><li>`realized`: O perfil está inserindo o segmento como parte da solicitação atual.</li><li>`exited`: O perfil está saindo do segmento como parte da solicitação atual.</li></ul> |
| `identityMap` | Um campo do tipo mapa que descreve os vários valores de identidade de um indivíduo, juntamente com seus namespaces associados. Para obter mais informações sobre `identityMap`, consulte [base da composição do schema](../../xdm/schema/composition.md#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Tratamento de erros da API {#api-error-handling}

Os pontos de extremidade da API do Destination SDK seguem os princípios gerais da mensagem de erro da API do Experience Platform. Consulte [Códigos de status da API](../../landing/troubleshooting.md#api-status-codes) e [erros do cabeçalho da solicitação](../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da plataforma.

## Próximas etapas

Após ler este documento, você agora sabe gerar perfis de amostra com base no schema de origem que você configurou no destino [fluxo de ativação](../ui/activate-batch-profile-destinations.md).

Agora é possível personalizar esses perfis ou usá-los como são retornados pela API para [testar a configuração de destino baseada em arquivo](file-based-destination-testing-api.md).
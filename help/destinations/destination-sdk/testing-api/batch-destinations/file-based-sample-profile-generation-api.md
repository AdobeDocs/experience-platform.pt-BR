---
description: Esta página explica como usar o endpoint da API /sample-profiles no Destination SDK para gerar perfis de amostra com base em um esquema de origem. Você pode usar esses perfis de amostra para testar a configuração de destino baseada em arquivo.
title: Gerar perfis de amostra com base em um esquema de origem
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---


# Gerar perfis de amostra com base em um esquema de origem

A primeira etapa no teste do destino baseado em arquivo é usar o `/sample-profiles` endpoint para gerar um perfil de amostra com base no esquema de origem existente.

Os perfis de amostra podem ajudar você a entender a estrutura JSON de um perfil. Além disso, elas fornecem um padrão que pode ser personalizado com seus próprios dados de perfil para testes de destino adicionais.

## Introdução {#getting-started}

Antes de continuar, reveja o [guia de introdução](../../getting-started.md) para obter informações importantes que você precisa saber para fazer chamadas com êxito para a API, incluindo como obter a permissão de criação de destino e os cabeçalhos necessários.

## Pré-requisitos {#prerequisites}

Antes de poder usar o `/sample-profiles` verifique se você atende às seguintes condições:

* Você tem um destino baseado em arquivo existente criado por meio do Destination SDK e pode visualizá-lo em seu [catálogo de destinos](../../../ui/destinations-workspace.md).
* Você criou pelo menos um fluxo de ativação para o destino na interface do usuário do Experience Platform. A variável `/sample-profiles` O endpoint cria os perfis com base no schema de origem definido no fluxo de ativação. Consulte a [tutorial de ativação](../../../ui/activate-batch-profile-destinations.md) para saber como criar um fluxo de ativação.
* Para fazer a solicitação de API com êxito, é necessário ter a ID da instância de destino correspondente à instância de destino que você testará. Obtenha a ID da instância de destino que você deve usar na chamada da API, no URL, ao navegar por uma conexão com seu destino na interface do Platform.

   ![Imagem da interface mostrando como obter a ID da instância de destino do URL.](../../assets/testing-api/get-destination-instance-id.png)

## Gerar perfis de amostra para teste de destino {#generate-sample-profiles}

Você pode gerar perfis de amostra com base no esquema de origem fazendo uma solicitação GET para o `/sample-profiles` ponto de extremidade com a ID da instância de destino do destino que você deseja testar.

**Formato da API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parâmetros de consulta | Descrição |
| -------- | ----------- |
| `destinationInstanceId` | A ID da instância de destino para a qual você está gerando perfis de amostra. Consulte a [pré-requisitos](#prerequisites) para obter detalhes sobre como obter essa ID. |
| `count` | *Opcional*. O número de perfis de amostra que você deseja gerar. O parâmetro pode assumir valores entre `1 - 1000`. Se essa propriedade não estiver definida, a API gerará um único perfil de amostra. |

**Solicitação**

A solicitação a seguir gera um perfil de amostra com base no esquema de origem definido na instância de destino com o perfil correspondente `destinationInstanceId`.

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
> A resposta retorna somente a associação do segmento, as identidades e os atributos de perfil que são usados na instância de destino. Mesmo se o esquema de origem tiver outros campos, eles serão ignorados.

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

![Imagem que mostra o mapeamento da interface do usuário para os campos da resposta da API.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| Propriedade | Descrição |
| -------- | ----------- |
| `segmentMembership` | Um objeto de mapa que descreve as associações de segmento do indivíduo. Para obter mais informações sobre `segmentMembership`, ler [Detalhes da associação do segmento](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Um carimbo de data e hora da última vez que esse perfil se qualificou para o segmento. |
| `status` | Um campo de string que indica se a associação do segmento foi realizada como parte da solicitação atual. Os seguintes valores são aceitos: <ul><li>`realized`: O perfil faz parte do segmento.</li><li>`exited`: o perfil está saindo do segmento como parte da solicitação atual.</li></ul> |
| `identityMap` | Um campo do tipo mapa que descreve os vários valores de identidade para um indivíduo, juntamente com seus namespaces associados. Para obter mais informações sobre `identityMap`, consulte [base da composição do esquema](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## Manipulação de erros de API {#api-error-handling}

Os endpoints da API Destination SDK seguem os princípios gerais de mensagem de erro da API Experience Platform. Consulte [Códigos de status da API](../../../../landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](../../../../landing/troubleshooting.md#request-header-errors) no guia de solução de problemas da Platform.

## Próximas etapas

Depois de ler este documento, agora você sabe como gerar perfis de amostra com base no esquema de origem configurado no destino [fluxo de ativação](../../../ui/activate-batch-profile-destinations.md).

Agora é possível personalizar esses perfis ou usá-los conforme retornados pela API para [testar a configuração de destino baseada em arquivo](file-based-destination-testing-api.md).

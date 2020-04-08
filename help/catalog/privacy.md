---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Processamento de solicitação de privacidade no Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 409d98818888f2758258441ea2d993ced48caf9a

---


# Processamento de solicitação de privacidade no Data Lake

O Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado por regulamentos de privacidade, como o Regulamento Geral de Proteção de Dados (RGPD) e o Ato de Privacidade do Consumidor da Califórnia (CCPA).

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para dados de clientes armazenados no Data Lake.

## Introdução

É recomendável que você tenha uma compreensão prática dos seguintes serviços da plataforma de experiência antes de ler este guia:

* [Privacy Service](../privacy-service/home.md): Gerencia solicitações de clientes para acessar, opt out da venda ou excluir seus dados pessoais nos aplicativos da Adobe Experience Cloud.
* [Serviço](home.md)de catálogo: O sistema de registro para localização e linhagem de dados na Experience Platform. Fornece uma API que pode ser usada para atualizar metadados do conjunto de dados.
* [Sistema](../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.

## Adicionar rótulos de privacidade a conjuntos de dados {#privacy-labels}

Para que um conjunto de dados seja processado em uma solicitação de privacidade para o Data Lake, o conjunto de dados deve receber rótulos de privacidade. Os rótulos de privacidade indicam quais campos no schema associado a um conjunto de dados se aplicam às namespaces que você espera que sejam enviadas em solicitações de privacidade.

Esta seção demonstra como adicionar rótulos de privacidade a um conjunto de dados para uso em solicitações de privacidade do Data Lake. Para começar, considere o seguinte conjunto de dados:

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

A `schemaMetadata` propriedade do conjunto de dados contém uma `gdpr` matriz, que está vazia no momento. Para adicionar etiquetas de privacidade ao conjunto de dados, esta matriz tem de ser atualizada utilizando uma solicitação PATCH para a API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catálogo.

>[!NOTE] Embora o storage seja nomeado `gdpr`, a adição de etiquetas nele permitirá solicitações de trabalho de privacidade para as regulamentações de RGPD e CCPA.

**Formato da API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{DATASET_ID}` | O `id` valor do conjunto de dados a ser atualizado. |

**Solicitação**

Neste exemplo, um conjunto de dados inclui um endereço de email no `personalEmail.address` campo. Para que esse campo funcione como um identificador para solicitações de privacidade do Data Lake, uma etiqueta que usa uma namespace não registrada deve ser adicionada à sua `gdpr` matriz.

A solicitação a seguir adiciona um rótulo de privacidade que atribui a namespace &quot;email_label&quot; ao `personalEmail.address` campo.

>[!IMPORTANT] Ao executar uma operação PATCH na propriedade de um conjunto de dados, certifique-se de copiar quaisquer subpropriedades existentes na carga da solicitação. `schemaMetadata` Excluir quaisquer valores existentes da carga fará com que eles sejam removidos do conjunto de dados.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Propriedade | Descrição |
| --- | --- |
| `namespace` | Uma matriz que lista as namespaces a serem associadas ao campo especificado em `path`. As Namespaces são usadas para identificar campos relacionados à privacidade ao [enviar solicitações](#submit) de acesso ou exclusão na API do Privacy Service. |
| `path` | O caminho para o campo dentro do schema associado do conjunto de dados que se aplica ao `namespace`. Idealmente, os rótulos de privacidade devem ser aplicados somente aos campos &quot;folha&quot; (campos sem subcampos). |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 (OK) com a ID do conjunto de dados fornecida na carga. Usar a ID para pesquisar o conjunto de dados novamente revela que os rótulos de privacidade foram adicionados.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Como rotular campos de tipo de mapa aninhados

É importante observar que existem dois tipos de campos do tipo mapa aninhados que não suportam a rotulagem de privacidade:

* Um campo tipo mapa dentro de um campo tipo matriz
* Um campo tipo mapa dentro de outro campo tipo mapa

O processamento do trabalho de privacidade para qualquer um dos dois exemplos acima pode falhar. Por esse motivo, é recomendável evitar o uso de campos do tipo mapa aninhados para armazenar dados de clientes privados. As IDs de consumidor relevantes devem ser armazenadas como um tipo de dados não mapeado dentro do `identityMap` campo (por si só, um campo tipo mapa) para conjuntos de dados baseados em registros, ou o `endUserID` campo para conjuntos de dados baseados em séries de tempo.

## Enviando solicitações {#submit}

>[!NOTE] Esta seção aborda como formatar solicitações de privacidade para o Data Lake. É altamente recomendável que você leia a documentação da API [do Privacy Service ou da interface do usuário](../privacy-service/api/getting-started.md) do [](../privacy-service/ui/overview.md) Privacy Service para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

A seção a seguir descreve como fazer solicitações de privacidade para o Data Lake usando a API ou a interface do usuário do Privacy Service.

### Uso da API

Ao criar solicitações de trabalho na API, qualquer `userIDs` um fornecido deve usar um arquivo específico `namespace` e `type` dependendo do armazenamento de dados ao qual se aplicam. As IDs do Data Lake devem usar &quot;não registradas&quot; para o `type` valor e um `namespace` valor que corresponda a uma das etiquetas [de](#privacy-labels) privacidade que foram adicionadas aos conjuntos de dados aplicáveis.

Além disso, a `include` matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações para o Data Lake, a matriz deve incluir o valor &quot;aepDataLake&quot;.

A solicitação a seguir cria um novo trabalho de privacidade para o Data Lake, usando a namespace &quot;email_label&quot; não registrada. Ele também inclui o valor do produto para o Data Lake no `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### Uso da interface

Ao criar solicitações de trabalho na interface do usuário, selecione **AEP Data Lake** e/ou **Perfil** em _Products_ para processar jobs para dados armazenados no Data Lake ou no Perfil Real-time Customer, respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

## Excluir processamento de solicitação

Quando a Experience Platform recebe uma solicitação de exclusão do Privacy Service, a Platform envia uma confirmação ao Privacy Service de que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são então removidos do Data Lake dentro de sete dias. Durante esse período de sete dias, os dados são excluídos por software e, portanto, não podem ser acessados por nenhum serviço da plataforma.

Em versões futuras, a Plataforma enviará uma confirmação ao Privacy Service depois que os dados forem fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade para o Data Lake. É recomendável que você continue lendo a documentação fornecida em todo este guia para aprofundar sua compreensão sobre como gerenciar dados de identidade e criar trabalhos de privacidade.

Consulte o documento sobre o processamento de solicitações de [privacidade para o Perfil](../profile/privacy.md) Cliente em tempo real para obter as etapas sobre o processamento de solicitações de privacidade para a loja de Perfis.
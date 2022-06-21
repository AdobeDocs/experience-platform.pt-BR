---
title: Modelo CSV para Ponto de extremidade da API de conversão de esquema
description: O endpoint /rpc/csv2schema na API do Registro de Schema permite usar modelos CSV para criar esquemas do Experience Data Model (XDM) automaticamente.
source-git-commit: 3860724b97987e555e12807c47f65fe040912d69
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 6%

---

# Modelo CSV para o endpoint da API de conversão de esquema

O `/rpc/csv2schema` endpoint no [!DNL Schema Registry] A API permite criar automaticamente um esquema do Experience Data Model (XDM) usando um arquivo CSV como modelo. Usando esse endpoint, você pode criar modelos para importar campos de esquema em massa e fazer a redução na API manual ou no trabalho da interface do usuário.

## Introdução

O `/rpc/csv2schema` o ponto de extremidade é parte do [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Antes de continuar, reveja o [guia de introdução](./getting-started.md) para links para a documentação relacionada, um guia para ler as chamadas de API de exemplo neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API do Experience Platform.

O `/rpc/csv2schema` o ponto de extremidade faz parte das chamadas de procedimento remoto (RPCs) suportadas pelo [!DNL Schema Registry]. Diferente de outros endpoints no [!DNL Schema Registry] A API, os pontos de extremidade RPC não exigem cabeçalhos adicionais como `Accept` ou `Content-Type`e não use um `CONTAINER_ID`. Em vez disso, eles devem usar o `/rpc` namespace, conforme demonstrado nas chamadas de API abaixo.

## Requisitos do arquivo CSV

Para usar esse terminal, primeiro crie um arquivo CSV com cabeçalhos de coluna apropriados e valores correspondentes. Algumas colunas são necessárias, enquanto as outras são opcionais. A tabela abaixo descreve essas colunas e sua função na construção do schema.

| Posição do cabeçalho CSV | Nome do cabeçalho CSV | Obrigatório / Opcional | Descrição |
| --- | --- | --- | --- |
| 1 | `isIgnored` | Opcional | Quando incluído e definido como `true`, indica que o campo não está pronto para o upload da API e deve ser ignorado. |
| 2 | `isCustom` | Obrigatório | Indica se o campo é um campo personalizado ou não. |
| 3 | `fieldGroupId` | Opcional | A ID do grupo de campos ao qual um campo personalizado deve ser associado. |
| 4 | `fieldGroupName` | (Consulte a descrição) | O nome do grupo de campos ao qual associar este campo.<br><br>Opcional para campos personalizados que não estendem campos padrão existentes. Se deixado em branco, o sistema atribuirá automaticamente o nome.<br><br>Necessário para campos padrão ou campos personalizados que estendem grupos de campos padrão, que é usado para consultar a variável `fieldGroupId`. |
| 5 | `fieldPath` | Obrigatório | O caminho completo da notação de pontos XED para o campo. Para incluir todos os campos de um grupo de campos padrão (conforme indicado em `fieldGroupName`), defina o valor como `ALL`. |
| 6 | `displayName` | Opcional | O título ou nome de exibição amigável do campo. Também pode ser um alias para o título, se existir. |
| 7 | `fieldDescription` | Opcional | Uma descrição para o campo. Também pode ser um alias para a descrição, se existir. |
| 8 | `dataType` | (Consulte a descrição) | Indica o [tipo de dados básico](../schema/field-constraints.md#basic-types) para o campo . Obrigatório para todos os campos personalizados.<br><br>If `dataType` está definida como `object`ou `properties` ou `$ref` também precisa ser definido para a mesma linha, mas não para ambas. |
| 9 | `isRequired` | Opcional | Indica se o campo é obrigatório para a assimilação de dados. |
| 10 | `isArray` | Opcional | Indica se o campo é uma matriz de seus `dataType`. |
| 11 | `isIdentity` | Opcional | Indica se o campo é um campo de identidade. |
| 12 | `identityNamespace` | Obrigatório se `isIdentity` é verdadeiro | O [namespace de identidade](../../identity-service/namespaces.md) para o campo de identidade. |
| 13º | `isPrimaryIdentity` | Opcional | Indica se o campo é a identidade primária do esquema. |
| 14 | `minimum` | Opcional | (Somente para campos numéricos) O valor mínimo do campo. |
| 15 | `maximum` | Opcional | (Somente para campos numéricos) O valor máximo do campo. |
| 16 | `enum` | Opcional | Uma lista de valores de enumeração para o campo, expressos como uma matriz (por exemplo, `[value1,value2,value3]`). |
| 17 | `stringPattern` | Opcional | (Somente para campos de string) Um padrão regex que o valor da string deve corresponder para passar a validação durante a assimilação de dados. |
| 18 | `format` | Opcional | (Somente para campos de string) O formato do campo de string. |
| 19º | `minLength` | Opcional | (Somente para campos de string) O comprimento mínimo do campo de string. |
| 20 | `maxLength` | Opcional | (Somente para campos de string) O comprimento máximo do campo de string. |
| 21 | `properties` | (Consulte a descrição) | Obrigatório se `dataType` está definida como `object` e `$ref` não estiver definido. Isso define o corpo do objeto como uma string JSON (por exemplo, `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (Consulte a descrição) | Obrigatório se `dataType` está definida como `object` e `properties` não estiver definido. Isso define o `$id` do objeto referenciado para o tipo de objeto (por exemplo, `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | Opcional | When `isIgnored` está definida como `true`, essa coluna é usada para fornecer as informações de cabeçalho do schema. |

{style=&quot;table-layout:auto&quot;}

Consulte o seguinte [Modelo CSV](../assets/sample-csv-template.csv) para determinar como o arquivo CSV deve ser formatado.

## Criar uma carga de exportação a partir de um arquivo CSV

Depois de configurar seu modelo CSV, você pode enviar o arquivo para a `/rpc/csv2schema` e converta-o em uma carga de exportação.

**Formato da API**

```http
POST /rpc/csv2schema
```

**Solicitação**

A carga da solicitação deve usar os dados do formulário como seu formato. Os campos de formulário obrigatórios são mostrados abaixo.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| Propriedade | Descrição |
| --- | --- |
| `csv-file` | O caminho para o modelo CSV armazenado em sua máquina local. |
| `schema-class-id` | O `$id` do XDM [classe](../schema/composition.md#class) que este esquema utilizará. |
| `schema-name` | Um nome de exibição para o esquema. |
| `schema-description` | Uma descrição para o esquema. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga de exportação gerada a partir do arquivo CSV. A carga assume uma forma de matriz e cada item de matriz é um objeto que representa um componente XDM dependente para o esquema. Selecione a seção abaixo para visualizar um exemplo completo de uma carga de exportação gerada de um arquivo CSV.

+++ Exemplo de carga de resposta

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## Importe a carga do esquema

Depois de gerar a carga de exportação do arquivo CSV, você pode enviar essa carga para o `/rpc/import` endpoint para gerar o schema .

Consulte a [guia de endpoint de importação](./import.md) para obter detalhes sobre como gerar schemas a partir de cargas de exportação.

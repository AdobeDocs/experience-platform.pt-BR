---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Visão geral da combinação de privacidade
topic: guide
translation-type: tm+mt
source-git-commit: 02014c503dc9d4597e1129cafe3ba86f4abe37e9
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---


# [!DNL Privacy Consent] visão geral da mixagem

A [!DNL Privacy/Marketing Preferences (Consent)] mistura (a seguir denominada &quot;[!DNL Privacy Consent] mixin&quot;) é uma mistura [!DNL Experience Data Model] (XDM) destinada a suportar a coleta de permissões e preferências do usuário geradas por CMPs e outras fontes dos clientes. Este documento cobre a estrutura e a utilização prevista dos diversos campos fornecidos pela mistura.

## Pré-requisitos {#prerequisites}

Este documento requer um entendimento funcional do [!DNL Experience Data Model] (XDM) e o uso dos schemas no [!DNL Experience Platform]. Consulte a seguinte documentação antes de continuar:

* [Visão geral do sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Noções básicas da composição do schema](http://www.adobe.com/go/xdm-schema-best-practices-en)

## exemplo de Schema {#schema}

>[!NOTE]
>
>O exemplo abaixo serve para ilustrar a estrutura dos dados enviados [!DNL Platform] por meio da [!DNL Privacy Consent] mistura, a fim de contextualizar a próxima seção neste documento que explica os principais campos fornecidos pela mistura. Um exemplo completo da estrutura do schema pode ser encontrado no [apêndice](#full-schema) para fins de referência.

O JSON a seguir mostra um exemplo do tipo de dados que a [!DNL Privacy Consent] mistura pode processar. As informações sobre o uso específico de cada um desses campos são fornecidas na próxima seção.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Campos {#fields}

As seções abaixo abordam a utilização de cada um dos principais campos fornecidos pela [!DNL Privacy Consent] mistura e a forma como os seus subcampos devem ser estruturados.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` é uma matriz que representa as configurações gerais de não participação selecionadas pelo cliente. Vários objetos podem ser incluídos nesta matriz, cada um representando um tipo específico de opção de não participação e as preferências selecionadas pelo cliente para esse tipo.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:optOutType` | O tipo de opção de não participação. Consulte o [apêndice](#optOutType-values) para ver os valores e definições aceites. |
| `xdm:optOutValue` | A preferência selecionada que o cliente escolheu para esse tipo específico de opção de não participação. Consulte o [apêndice](#choice-optOutValue-values) para ver os valores e definições aceites. |
| `xdm:timestamp` | Um carimbo de data e hora ISO 8601 de quando a preferência de opção de não participação foi alterada, se aplicável. |
| `xdm:basisOfProcessing` | Indica a base relacionada à privacidade com a qual os dados devem ser coletados e processados. Por padrão, esse campo é definido como `consent`, o que indica que os dados só devem ser processados se o usuário tiver fornecido consentimento (conforme refletido em `xdm:optOutValue`).<br><br>Em algumas circunstâncias, os clientes não têm de dar o seu consentimento para o processamento de dados. `xdm:basisOfProcessing` deve ser incluído no objeto de opção de não participação nesses casos, indicando o motivo pelo qual um prompt de consentimento não foi fornecido. Consulte o [apêndice](#basisOfProcessing-values) para ver os valores e definições aceites. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` captura as preferências do cliente em relação às maneiras pelas quais seus dados podem ser usados para personalização. Os usuários podem opt out casos de uso de personalização específicos ou opt out de personalização totalmente.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` não abrange os casos de utilização da comercialização. Por exemplo, se um cliente opt out de personalização para e-mails, ele não deixará de receber e-mails. Em vez disso, os e-mails que recebem serão genéricos e não baseados no seu perfil.
>
>Pelo mesmo exemplo, se um cliente opt out de marketing por email (por meio `xdm:marketingPreferences`de, explicado na [próxima seção](#marketingPreferences)), então esse cliente não receberá nenhum email, mesmo que a personalização do email seja permitida.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:default` | Os dados fornecidos neste objeto representam as preferências do cliente para personalização como um todo. |
| `xdm:details` | Uma matriz de objetos, um para cada tipo de personalização específico para o qual o cliente forneceu preferências. |
| `xdm:choice` | A preferência de consentimento fornecido pelo cliente para personalização em geral, ou um tipo de personalização específico, dependendo se é fornecida sob `xdm:default` ou `xdm:details`, respectivamente. Consulte o [apêndice](#choice-optOutValue-values) para ver os valores e definições aceites. |
| `xdm:type` | Os objetos na `xdm:details` matriz devem fornecer esse campo para indicar o uso de personalização específico para o qual o cliente está fornecendo dados de consentimento. Consulte o [apêndice](#type-values) para ver os valores e definições aceites. |
| `xdm:timestamp` | Um carimbo de data e hora ISO 8601 de quando a preferência de opção de não participação foi alterada, se aplicável. |
| `xdm:basisOfProcessing` | Indica a base relacionada à privacidade com a qual os dados devem ser coletados e processados. Por padrão, esse campo é definido como `consent`, o que indica que os dados só devem ser processados se o usuário tiver fornecido consentimento (conforme refletido em `xdm:choice`).<br><br>Em algumas circunstâncias, os clientes não são solicitados a fornecer consentimento para a personalização. `xdm:basisOfProcessing` deve ser incluído no objeto de opção de não participação nesses casos, indicando o motivo pelo qual um prompt de consentimento não foi fornecido. Consulte o [apêndice](#basisOfProcessing-values) para ver os valores e definições aceites. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` captura as preferências do cliente em relação a quais fins de marketing seus dados podem ser usados. Os usuários podem opt out casos específicos de uso de marketing ou opt out totalmente o marketing direto.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:default` | Os dados fornecidos neste objeto representam as preferências do cliente para marketing direto como um todo. |
| `xdm:details` | Uma matriz de objetos, um para cada caso de uso de marketing específico para o qual o cliente forneceu preferências. |
| `xdm:choice` | A preferência de consentimento fornecido pelo cliente para comercialização em geral, ou um caso de uso de marketing específico, dependendo se é fornecido sob `xdm:default` ou `xdm:details`, respectivamente. Consulte o [apêndice](#choice-optOutValue-values) para ver os valores e definições aceites. |
| `xdm:subscriptions` | Um objeto cujas chaves representam subscrições específicas da empresa, como listas de correspondência ou boletins informativos. Cada objeto de subscrição deve, por sua vez, conter um `xdm:choice` valor para a subscrição em questão. |
| `xdm:type` | Os objetos no `xdm:details` array devem fornecer esse campo para indicar o caso de uso de marketing específico para o qual o cliente está fornecendo dados de consentimento. Consulte o [apêndice](#type-values) para ver os valores e definições aceites. |
| `xdm:timestamp` | Um carimbo de data e hora ISO 8601 de quando a preferência de opção de não participação foi alterada, se aplicável. |
| `xdm:basisOfProcessing` | Indica a base relacionada à privacidade com a qual os dados devem ser coletados e processados. Por padrão, esse campo é definido como `consent`, o que indica que os dados só devem ser processados se o usuário tiver fornecido consentimento (conforme refletido em `xdm:choice`).<br><br>Em algumas circunstâncias, os clientes não têm de ser solicitados a fornecer consentimento para a comercialização direta. `xdm:basisOfProcessing` deve ser incluído no objeto de opção de não participação nesses casos, indicando o motivo pelo qual um prompt de consentimento não foi fornecido. Consulte o [apêndice](#basisOfProcessing-values) para ver os valores e definições aceites. |

## Como inserir dados de consentimento usando a combinação {#ingest}

Para usar a [!DNL Privacy Consent] mistura para assimilar dados de consentimento de seus clientes, você deve adicionar a mistura a um schema novo ou existente e criar um conjunto de dados baseado nesse schema.

Consulte o tutorial sobre como [criar um schema na interface do usuário](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para obter as etapas sobre como adicionar combinações a um schema. A mistura[!DNL  Privacy Consent] é compatível com schemas com base nas classes [!DNL XDM Individual Profile] ou [!DNL XDM ExperienceEvent].

Depois de criar um schema contendo a [!DNL Privacy Consent] mistura, consulte a seção sobre como [criar um conjunto de dados](../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, seguindo as etapas para criar um conjunto de dados com um schema existente.

>[!IMPORTANT]
>
>Se desejar enviar dados de consentimento para [!DNL Real-time Customer Profile], é necessário criar um schema [!DNL Profile]habilitado com base na [!DNL XDM Individual Profile] classe que contém a [!DNL Privacy Consent] combinação. O conjunto de dados criado com base nesse schema também deve estar habilitado para [!DNL Profile]. Consulte os tutoriais acima para ver as etapas específicas relacionadas aos [!DNL Real-time Customer Profile] requisitos.

## Apêndice {#appendix}

As seções a seguir apresentam informações de referência adicionais relativas à [!DNL Privacy Consent] mistura.

### Valores aceitos para xdm:optOutType {#optOutType-values}

A tabela a seguir descreve os valores aceitos para `xdm:optOutType`:

| Valor | Descrição |
| --- | --- |
| `general_opt_out` | Os dados não podem ser usados para qualquer finalidade. Isso geralmente bloqueia a coleta de dados, exceto quando a base do processamento não é &quot;consentimento&quot;.<br><br>Ao usar esse tipo de opção de não participação, os valores aceitos `in` e `out` obtêm o seguinte significado contextual:<ul><li>`in`: O utilizador **deu o seu consentimento** para que os seus dados sejam utilizados para o tratamento geral.</li><li>`out`: O utilizador **não autoriza** a utilização dos seus dados para processamento geral.</li></ul>Consulte a tabela de valores [aceitos para xdm:optOutValue](#choice-optOutValue-values) para obter mais informações. |
| `anonymous_analysis` | Os dados não podem ser usados para métricas genéricas da Web que não exigem nenhum tipo de ID de usuário, como o número de vezes que uma página específica foi visualizada. |
| `device_linking` | Os dados de um dispositivo usado por um visitante não podem ser combinados com dados de outro dispositivo usado pelo mesmo visitante. Os dispositivos são vinculados usando técnicas como nome de usuário ou endereço de email comuns, geralmente por meio da cooperativa de dispositivos Adobe ou de um gráfico de dispositivos privados. |
| `pseudonymous_analysis` | Os dados não podem ser usados para métricas da Web fornecidas pela Adobe Analytics, que exigem IDs pseudônimas para identificar caminhos que os usuários percorrem em um site (como um relatório de fallout), para estabelecer sessões e para fins de atribuição. |
| `sales_sharing_opt_out` | Os dados não podem ser usados para fins de vendas ou compartilhamento com terceiros.<br><br>Ao usar esse tipo de opção de não participação, os valores aceitos `in` e `out` obtêm o seguinte significado contextual:<ul><li>`in`: O usuário **deu consentimento** para que seus dados sejam usados para fins de vendas e compartilhamento.</li><li>`out`: O usuário **não aceita** que seus dados sejam usados para fins de vendas e compartilhamento.</li></ul>Consulte a tabela de valores [aceitos para xdm:optOutValue](#choice-optOutValue-values) para obter mais informações. |

### Valores aceitos para xdm:basedOfProcessing {#basisOfProcessing-values}

A tabela a seguir descreve os valores aceitos para `xdm:basisOfProcessing`:

| Valor | Descrição |
| --- | --- |
| `consent` **(Padrão)** | A coleta de dados para a finalidade especificada é permitida, dado que o indivíduo forneceu permissão explícita. Esse é o valor padrão de `xdm:basisOfProcessing` se nenhum outro valor for fornecido. <br><br>**IMPORTANTE **: Os valores para`xdm:choice`e`xdm:optOutValue`só são respeitados quando`xdm:basisOfProcessing`está definido como`consent`. Se qualquer um dos outros valores descritos nesta tabela forem usados para`xdm:basisOfProcessing`, as opções de consentimento do indivíduo serão ignoradas. |
| `compliance` | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `contract` | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações contratuais com a pessoa singular. |
| `legitimate_interest` | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera os possíveis danos que isso representa para o indivíduo. |
| `public_interest` | A recolha de dados para o fim especificado é necessária para efetuar uma tarefa do interesse público ou para o exercício da autoridade pública. |
| `vital_interest` | A recolha de dados para a finalidade especificada é necessária para proteger os interesses vitais do indivíduo. |

### Valores aceitos para xdm:choice e xdm:optOutValue {#choice-optOutValue-values}

A tabela a seguir descreve os valores aceitos para `xdm:choice` e `xdm:optOutValue`:

| Valor | Descrição |
| --- | --- |
| `pending` | O sistema ainda não recebeu informações de preferência de consentimento do cliente. Pode ser usado para a primeira página de um site enquanto o consentimento é obtido. Pode também ser utilizado para indicar que o consentimento é &quot;presumido&quot;, em vez de explicitamente fornecido. |
| `in` | O usuário opt in para a preferência de consentimento. Por outras palavras, **consentiram** na utilização dos seus dados, tal como indicado pela preferência de consentimento em questão. |
| `out` | O usuário opt out da preferência de consentimento. Por outras palavras, **não** consentiram na utilização dos seus dados, tal como indicado pela preferência de consentimento em questão. |
| `not_applicable` | A preferência de consentimento em questão não se aplica ao cliente. |
| `not_provided` | O cliente não forneceu nenhuma informação de preferência de consentimento. |
| `unknown` | As informações de preferência de consentimento do cliente são desconhecidas. |

### Valores aceitos para xdm:type {#type-values}

A tabela a seguir descreve os valores aceitos para `xdm:type`:

| Valor | Descrição |
| --- | --- |
| `ads` | Anúncios que podem ser exibidos em sites não relacionados. |
| `content` | Conteúdo que aparece em seu site. |
| `customer_support` | Dados relacionados ao suporte ao cliente. |
| `email` | Mensagens de email. |
| `iot` | Dados relacionados à &quot;Internet das coisas&quot; (IoT). |
| `in_app_messages` | Mensagens no aplicativo. |
| `in_home` | Mensagens internas. |
| `in_store` | Mensagens na loja. |
| `in_vehicle` | Mensagens no veículo. |
| `offers` | ofertas especiais. |
| `phone_calls` | Dados relacionados às interações de chamadas telefônicas. |
| `push_notifications` | Notificações por push. |
| `sms` | Mensagens SMS. |
| `social_media` | Conteúdo de mídia social. |
| `snail_mail` | Mensagens enviadas através do delivery postal convencional. |
| `third_party_content` | Conteúdo ou artigos exibidos em seu site que são fornecidos por uma entidade independente. |
| `third_party_offers` | Ofertas ou anúncios exibidos em seus serviços de publicidade do site de uma entidade não relacionada. |

### schema [!DNL Privacy Consent] completo {#full-schema}

O seguinte JSON representa o [!DNL Privacy Consent] schema completo como aparece no Registro do Schema:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```

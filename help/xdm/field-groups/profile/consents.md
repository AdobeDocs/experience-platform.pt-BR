---
solution: Experience Platform
title: Grupo de campos de esquema de consentimentos e preferências
description: Saiba mais sobre o grupo de campos de esquema Consentimentos e Preferências.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# Grupo de campos [!UICONTROL Consents and Preferences]

[!UICONTROL Consents and Preferences] é um grupo de campos padrão para a [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura informações de consentimento e preferência de um cliente individual.

>[!NOTE]
>
>Como este grupo de campos é compatível somente com [!DNL XDM Individual Profile], ele não pode ser usado para esquemas [!DNL XDM ExperienceEvent]. Para incluir dados de consentimento e preferência no esquema do Evento de experiência, adicione o [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] tipo de dados](../../data-types/consents.md) ao esquema usando um [grupo de campos personalizado](../../ui/resources/field-groups.md#create).

## Estrutura do grupo de campos {#structure}

O grupo de campos [!UICONTROL Consents and Preferences] fornece um único campo de tipo de objeto, `consents`, para capturar informações de consentimento e preferência. Este campo estende o tipo de dados [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] &#x200B;](../../data-types/consents.md), removendo o campo `adID` e adicionando um campo de mapa `idSpecific`.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulte o guia em [explorando recursos XDM](../../ui/explore.md) para obter etapas sobre como pesquisar qualquer recurso XDM e inspecionar sua estrutura na interface do usuário do Experience Platform.

O JSON a seguir mostra um exemplo do tipo de dados que o grupo de campos [!UICONTROL Consents and Preferences] pode processar. Para obter informações sobre como usar a maioria dos campos fornecidos pelo grupo de campos, consulte o manual no [tipo de dados Consentimentos e Preferências](../../data-types/consents.md). As subseções abaixo se concentram nos atributos exclusivos que o grupo de campos adiciona ao tipo de dados.

```json
{
  "consents": {
    "collect": {
      "val": "VI"
    },
    "share": {
      "val": "y"
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "email": {
        "val": "y"
      }
    },
    "idSpecific": {
      "ECID": {
        "37784337855396895622558625508046772577": {
          "adID": {
            "val": "n",
          },
          "share": {
            "val": "n"
          },
          "marketing": {
            "push": {
              "val": "n",
              "time": "2020-09-30T01:02:33+00:00",
              "reason": "not relevant"
            }
          }
        }
      },
      "email": {
        "john@xyz.com": {
          "marketing": {
            "email": {
              "val": "y"
            }
          }
        }
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>Você pode gerar dados JSON de amostra para qualquer esquema XDM definido no Experience Platform para ajudar a visualizar como os dados de consentimento e preferência do cliente devem ser mapeados. Consulte a documentação a seguir para obter mais informações:
>
>* [Gerar dados de exemplo na interface](../../ui/sample.md)
>* [Gerar dados de amostra na API](../../api/sample-data.md)

### `idSpecific`

`idSpecific` pode ser usado quando um determinado consentimento ou preferência não se aplica universalmente a um cliente, mas está restrito a um único dispositivo ou ID. Por exemplo, um cliente pode recusar o recebimento de emails para um endereço, enquanto possivelmente permite emails em outro.

>[!IMPORTANT]
>
>Os consentimentos e preferências no nível do canal (ou seja, aqueles fornecidos em `consents` fora de `idSpecific`) se aplicam a todas as IDs nesse canal. Portanto, todos os consentimentos e preferências no nível do canal têm efeito direto se as configurações equivalentes específicas de ID ou dispositivo são respeitadas:
>
>* Se o cliente optou por não participar no nível do canal, quaisquer consentimentos ou preferências equivalentes em `idSpecific` serão ignorados.
>* Se o consentimento ou a preferência no nível do canal não estiver definido, ou se o cliente tiver optado, os consentimentos ou as preferências equivalentes em `idSpecific` serão honrados.

Cada chave no objeto `idSpecific` representa um namespace de identidade específico reconhecido pelo Adobe Experience Platform Identity Service. Embora você possa definir seus próprios namespaces personalizados para categorizar identificadores diferentes, é recomendável usar um dos namespaces padrão fornecidos pelo Serviço de identidade para reduzir os tamanhos de armazenamento do Perfil do cliente em tempo real. Para obter mais informações sobre namespaces de identidade, consulte a [visão geral sobre namespaces de identidade](/help/identity-service/features/namespaces.md) na documentação do Serviço de Identidade.

As chaves para cada objeto de namespace representam os valores de identidade exclusivos para os quais o cliente definiu preferências. Cada valor de identidade pode conter um conjunto completo de consentimentos e preferências, formatados da mesma forma que `consents`.

```json
"idSpecific": {
  "email": {
    "jdoe@example.com": {
      "marketing": {
        "email": {
          "val": "n"
        }
      }
    }
  },
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

Dentro de `marketing` objetos fornecidos na seção `idSpecific`, os campos `any` e `preferred` não têm suporte. Esses campos só podem ser configurados no nível do usuário. Além disso, as preferências de marketing do `idSpecific` para `email`, `sms` e `push` não oferecem suporte para campos `subscriptions`.

Também há um consentimento que só pode ser fornecido na seção `idSpecific`: `adID`. Esse campo é abordado na subseção abaixo.

#### `adID`

O consentimento de `adID` representa o consentimento do cliente para que uma ID de anunciante (IDFA ou GAID) possa ser usada para vincular o cliente em aplicativos neste dispositivo. Este valor só pode ser configurado no namespace de identidade `ECID` na seção `idSpecific` e não pode ser definido para outros namespaces ou no nível de usuário para este grupo de campos.

```json
"idSpecific": {
  "ECID": {
    "37784337855396895622558625508046772577": {
      "collect": {
        "val": "y"
      },
      "adID": {
        "val": "n"
      },
      "marketing": {
        "push": {
          "val": "n"
        }
      }
    }
  }
}
```

>[!NOTE]
>
>Não é esperado que você defina esse valor diretamente, já que o Adobe Experience Platform Mobile SDK o define automaticamente quando apropriado.

## Assimilar dados usando o grupo de campos {#ingest}

Para usar o grupo de campos [!UICONTROL Consents and Preferences] para assimilar dados de consentimento de seus clientes, você deve criar um conjunto de dados com base em um esquema que contenha esse grupo de campos.

Consulte o tutorial sobre [criação de um esquema na interface](https://www.adobe.com/go/xdm-schema-editor-tutorial-en_br) para ver etapas sobre como atribuir grupos de campos a campos. Depois de criar um esquema contendo um campo com o grupo de campos [!UICONTROL Consents and Preferences], consulte a seção sobre [criação de um conjunto de dados](/help/catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, seguindo as etapas para criar um conjunto de dados com um esquema existente.

>[!IMPORTANT]
>
>Para enviar dados de consentimento para [!DNL Real-Time Customer Profile], é necessário criar um esquema habilitado para [!DNL Profile] com base na classe [!DNL XDM Individual Profile] que contém o grupo de campos [!UICONTROL Consents and Preferences]. O conjunto de dados criado com base nesse esquema também deve ser habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para obter etapas específicas relacionadas aos requisitos de [!DNL Real-Time Customer Profile] para esquemas e conjuntos de dados.
>
>Além disso, você também deve garantir que suas políticas de mesclagem sejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral em [políticas de mesclagem](/help/rtcdp/profile/merge-policies.md) para obter mais informações.

## Lidar com alterações de consentimento e preferência

Quando um cliente altera os consentimentos ou preferências no site, essas alterações devem ser coletadas e imediatamente aplicadas, definindo o consentimento na biblioteca de coleta de dados usada. Se um cliente recusar a coleta de dados, toda a coleta de dados deverá ser interrompida imediatamente. Se um cliente recusar a personalização, não deverá haver personalização presente na próxima página que ele carregar. Consulte [`setConsent`](/help/collection/js/commands/setconsent.md) usando a biblioteca JavaScript ou a ação [[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md) usando a extensão de tag da Web SDK.

## Próximas etapas

Este documento abordou a estrutura e o uso do grupo de campos [!UICONTROL Consents and Preferences]. Para obter mais informações sobre os outros campos fornecidos pelo grupo de campos, consulte o documento no [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] tipo de dados](../../data-types/consents.md).

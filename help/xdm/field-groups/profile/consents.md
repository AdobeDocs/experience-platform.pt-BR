---
solution: Experience Platform
title: Grupo de campos de esquema de consentimentos e preferências
description: Este documento fornece uma visão geral do grupo de campos de esquema Consentimentos e Preferências.
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL Consentimentos e preferências] grupo de campos

[!UICONTROL Consentimentos e preferências] é um grupo de campos padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura informações de consentimento e preferência de um cliente individual.

>[!NOTE]
>
>Como este grupo de campos é compatível somente com [!DNL XDM Individual Profile], ele não pode ser usado para [!DNL XDM ExperienceEvent] esquemas. Se quiser incluir dados de consentimento e preferência no esquema do Evento de experiência, adicione o [[!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados](../../data-types/consents.md) ao esquema por meio do uso de um [grupo de campos personalizados](../../ui/resources/field-groups.md#create) em vez disso.

## Estrutura do grupo de campos {#structure}

A variável [!UICONTROL Consentimentos e preferências] o grupo de campos fornece um único campo do tipo objeto, `consents`, para capturar informações de consentimento e preferência. Esse campo estende a variável [[!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados](../../data-types/consents.md), removendo o `adID` e adicionando um `idSpecific` mapear campo.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulte o guia sobre [exploração de recursos XDM](../../ui/explore.md) Consulte para obter etapas sobre como pesquisar qualquer recurso XDM e inspecionar sua estrutura na interface do usuário da plataforma.

O JSON a seguir mostra um exemplo do tipo de dados que o [!UICONTROL Consentimentos e preferências] grupo de campos pode ser processado. Para obter informações sobre como usar a maioria dos campos fornecidos pelo grupo de campos, consulte o manual no [Tipo de dados Consentimentos e Preferências](../../data-types/consents.md). As subseções abaixo se concentram nos atributos exclusivos que o grupo de campos adiciona ao tipo de dados.

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
>* [Gerar dados de amostra na interface](../../ui/sample.md)
>* [Gerar dados de amostra na API](../../api/sample-data.md)


### `idSpecific`

`idSpecific` O pode ser usado quando um consentimento ou preferência específica não se aplica universalmente a um cliente, mas está restrita a um único dispositivo ou ID. Por exemplo, um cliente pode recusar o recebimento de emails para um endereço, enquanto possivelmente permite emails em outro.

>[!IMPORTANT]
>
>Consentimentos e preferências no nível do canal (ou seja, aqueles fornecidos sob `consents` fora de `idSpecific`) se aplicam a todas as IDs nesse canal. Portanto, todos os consentimentos e preferências no nível do canal têm efeito direto se as configurações equivalentes específicas de ID ou dispositivo são respeitadas:
>
>* Se o cliente tiver optado por não participar no nível do canal, quaisquer consentimentos ou preferências equivalentes em `idSpecific` são ignorados.
>* Se o consentimento ou a preferência no nível do canal não estiver definido, ou se o cliente tiver optado, os consentimentos ou preferências equivalentes em `idSpecific` são honrados.


Cada chave no `idSpecific` O objeto representa um namespace de identidade específico reconhecido pelo Adobe Experience Platform Identity Service. Embora você possa definir seus próprios namespaces personalizados para categorizar identificadores diferentes, é recomendável usar um dos namespaces padrão fornecidos pelo Serviço de identidade para reduzir os tamanhos de armazenamento do Perfil do cliente em tempo real. Para obter mais informações sobre namespaces de identidade, consulte o [visão geral do namespace de identidade](../../../identity-service/namespaces.md) na documentação do Serviço de identidade.

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

Dentro de `marketing` objetos fornecidos na `idSpecific` seção, a variável `any` e `preferred` Os campos do não são compatíveis. Esses campos só podem ser configurados no nível do usuário. Além disso, a `idSpecific` preferências de marketing para `email`, `sms`, e `push` não oferecem suporte `subscriptions` campos.

Também há um consentimento que só pode ser fornecido no `idSpecific` seção: `adID`. Esse campo é abordado na subseção abaixo.

#### `adID`

A variável `adID` o consentimento representa o consentimento do cliente para determinar se uma ID de anunciante (IDFA ou GAID) pode ser usada para vincular o cliente em aplicativos neste dispositivo. Esse valor só pode ser configurado no campo `ECID` namespace de identidade na variável `idSpecific` e não podem ser definidos para outros namespaces ou no nível do usuário para este grupo de campos.

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
>Não é esperado que você defina esse valor diretamente, já que o SDK do Adobe Experience Platform Mobile o define automaticamente quando apropriado.

## Assimilar dados usando o grupo de campos {#ingest}

Para utilizar a variável [!UICONTROL Consentimentos e preferências] grupo de campos para assimilar dados de consentimento de seus clientes, você deve criar um conjunto de dados com base em um esquema que contenha esse grupo de campos.

Veja o tutorial sobre [criação de um esquema na interface](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) para obter etapas sobre como atribuir grupos de campos a campos. Depois de criar um esquema contendo um campo com a variável [!UICONTROL Consentimentos e preferências] , consulte a seção sobre [criação de um conjunto de dados](../../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, siga as etapas para criar um conjunto de dados com um esquema existente.

>[!IMPORTANT]
>
>Se desejar enviar dados de consentimento para [!DNL Real-Time Customer Profile], é necessário criar um [!DNL Profile]Esquema habilitado para com base no [!DNL XDM Individual Profile] classe que contém a variável [!UICONTROL Consentimentos e preferências] grupo de campos. O conjunto de dados criado com base nesse esquema também deve ser habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para obter etapas específicas relacionadas ao [!DNL Real-Time Customer Profile] requisitos para esquemas e conjuntos de dados.
>
>Além disso, você também deve garantir que suas políticas de mesclagem sejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral em [políticas de mesclagem](../../../rtcdp/profile/merge-policies.md) para obter mais informações.

## Lidar com alterações de consentimento e preferência

Quando um cliente altera os consentimentos ou preferências no site, essas alterações devem ser coletadas e aplicadas imediatamente usando o [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Se um cliente recusar a coleta de dados, toda a coleta de dados deverá ser interrompida imediatamente. Se um cliente optar por não ser personalizado, não deverá haver personalização na próxima página que visitar.

## Próximas etapas

Este documento abordou a estrutura e a utilização do [!UICONTROL Consentimentos e preferências] grupo de campos. Para obter mais informações sobre os outros campos fornecidos pelo grupo de campos, consulte o documento sobre [[!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados](../../data-types/consents.md).

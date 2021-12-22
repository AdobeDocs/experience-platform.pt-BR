---
solution: Experience Platform
title: Grupo de campos Esquema de Consentimento e Preferências
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Consents and Preferences schema .
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
source-git-commit: 04e778d3318d60733772c2042c8bb272f0c87d5c
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# [!UICONTROL Consentimentos e preferências] grupo de campos

[!UICONTROL Consentimentos e preferências] é um grupo de campos padrão para a variável [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que captura informações de consentimento e preferência para um cliente individual.

>[!NOTE]
>
>Como esse grupo de campos é compatível somente com [!DNL XDM Individual Profile], ele não pode ser usado para [!DNL XDM ExperienceEvent] esquemas. Se desejar incluir dados de consentimento e preferência no esquema Evento de experiência, adicione a variável [[!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados](../../data-types/consents.md) para o schema por meio do uso de um [grupo de campos personalizado](../../ui/resources/field-groups.md#create) em vez disso.

## Estrutura do grupo de campos {#structure}

O [!UICONTROL Consentimentos e preferências] o grupo de campos fornece um único campo do tipo objeto, `consents`, para capturar informações de consentimento e preferência. Esse campo estende o [[!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados](../../data-types/consents.md), removendo o `adID` e adicionar um `idSpecific` campo de mapa.

![](../../images/field-groups/consent.png)

>[!TIP]
>
>Consulte o guia sobre [exploração de recursos XDM](../../ui/explore.md) para obter etapas sobre como pesquisar qualquer recurso XDM e inspecionar sua estrutura na interface do usuário da plataforma.

O JSON a seguir mostra um exemplo do tipo de dados que a variável [!UICONTROL Consentimentos e preferências] grupo de campos pode processar. Para obter informações sobre como usar a maioria dos campos fornecidos pelo grupo de campos, consulte o guia no [Tipo de dados de Consentimentos e Preferências](../../data-types/consents.md). As subseções abaixo focalizam os atributos exclusivos adicionados pelo grupo de campos ao tipo de dados.

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
>* [Gerar dados de amostra na interface do usuário](../../ui/sample.md)
>* [Gerar dados de amostra na API](../../api/sample-data.md)


### `idSpecific`

`idSpecific` pode ser usado quando um consentimento ou preferência específico não se aplica universalmente a um cliente, mas é restrito a um único dispositivo ou ID. Por exemplo, um cliente pode recusar o recebimento de emails para um endereço, enquanto pode permitir emails em outro.

>[!IMPORTANT]
>
>Consentimentos e preferências no nível do canal (ou seja, aqueles fornecidos em `consents` fora de `idSpecific`) se aplicam a todas as IDs nesse canal. Portanto, todos os consentimentos e preferências no nível do canal afetam diretamente se configurações equivalentes específicas de ID ou dispositivo são respeitadas:
>
>* Se o cliente tiver optado por não participar no nível do canal, quaisquer consentimentos ou preferências equivalentes em `idSpecific` são ignoradas.
>* Se o consentimento ou a preferência no nível do canal não estiver definida ou o cliente tiver optado por participar, os consentimentos ou preferências equivalentes em `idSpecific` são honradas.


Cada tecla na `idSpecific` representa um namespace de identidade específico reconhecido pelo Adobe Experience Platform Identity Service. Embora você possa definir seus próprios namespaces personalizados para categorizar identificadores diferentes, é recomendável usar um dos namespaces padrão fornecidos pelo Serviço de identidade para reduzir os tamanhos de armazenamento para o Perfil do cliente em tempo real. Para obter mais informações sobre namespaces de identidade, consulte [visão geral do namespace de identidade](../../../identity-service/namespaces.md) na documentação do Serviço de identidade.

As chaves de cada objeto de namespace representam os valores de identidade exclusivos para os quais o cliente definiu preferências. Cada valor de identidade pode conter um conjunto completo de consentimentos e preferências, formatados da mesma forma que `consents`.

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

Within `marketing` objetos fornecidos no `idSpecific` seção , a variável `any` e `preferred` campos não são compatíveis. Esses campos só podem ser configurados no nível do usuário. Além disso, a variável `idSpecific` preferências de marketing para `email`, `sms`e `push` não suporta `subscriptions` campos.

Há também um consentimento que só pode ser fornecido no `idSpecific` seção: `adID`. Este campo é coberto pela subseção abaixo.

#### `adID`

O `adID` o consentimento representa o consentimento do cliente para se uma ID do anunciante (IDFA ou GAID) pode ser usada para vincular o cliente entre aplicativos neste dispositivo. Esse valor só pode ser configurado na variável `ECID` namespace de identidade na `idSpecific` e não pode ser definido para outros namespaces ou no nível do usuário para esse grupo de campos.

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
>Não é esperado que você defina esse valor diretamente, pois o Adobe Experience Platform Mobile SDK o define automaticamente quando apropriado.

## Inserção de dados usando o grupo de campos {#ingest}

Para usar o [!UICONTROL Consentimentos e preferências] para assimilar dados de consentimento dos clientes, é necessário criar um conjunto de dados com base em um esquema que contenha esse grupo de campos.

Veja o tutorial em [criação de um schema na interface do usuário](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) para obter etapas sobre como atribuir grupos de campos a campos. Depois de criar um schema contendo um campo com a variável [!UICONTROL Consentimentos e preferências] grupo de campos, consulte a seção em [criação de um conjunto de dados](../../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, siga as etapas para criar um conjunto de dados com um esquema existente.

>[!IMPORTANT]
>
>Se desejar enviar dados de consentimento para o [!DNL Real-time Customer Profile], é necessário criar um [!DNL Profile]-enabled schema baseado no [!DNL XDM Individual Profile] classe que contém [!UICONTROL Consentimentos e preferências] grupo de campos. O conjunto de dados criado com base nesse esquema também deve ser habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para etapas específicas relacionadas a [!DNL Real-time Customer Profile] requisitos para esquemas e conjuntos de dados.
>
>Além disso, também é necessário garantir que suas políticas de mesclagem estejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral em [políticas de mesclagem](../../../rtcdp/profile/merge-policies.md) para obter mais informações.

## Lidar com alterações de consentimento e preferência

Quando um cliente altera seus consentimentos ou preferências no seu site, essas alterações devem ser coletadas e aplicadas imediatamente usando o [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Se um cliente recusar a coleta de dados, toda a coleta de dados deverá ser interrompida imediatamente. Se um cliente recusar a personalização, então não deverá haver personalização na próxima página que visitar.

## Próximas etapas

Este documento abrangia a estrutura e a utilização do [!UICONTROL Consentimentos e preferências] grupo de campos. Para obter mais informações sobre os outros campos fornecidos pelo grupo de campos, consulte o documento no [[!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados](../../data-types/consents.md).

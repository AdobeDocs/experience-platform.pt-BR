---
solution: Experience Platform
title: Privacidade/Personalização/Mistura de preferências de marketing (Consentimentos)
topic-legacy: overview
description: Este documento fornece uma visão geral da combinação Privacidade/Personalização/Preferências de marketing (Consentimentos).
exl-id: ec592102-a9d3-4cac-8b94-58296a138573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2238'
ht-degree: 1%

---

# [!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] mistura

[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] (a seguir denominada  [!DNL Privacy & Consents] mixin) é uma mistura padrão para a  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md), usada para capturar informações de consentimento e preferência do cliente.

>[!NOTE]
>
>Como essa mixin é compatível somente com [!DNL XDM Individual Profile], ela não pode ser usada para schemas [!DNL XDM ExperienceEvent]. Se desejar incluir dados de consentimento e preferência no esquema do Evento de Experiência, adicione o tipo de dados [[!UICONTROL Consent for Privacy, Personalization and Marketing Preferences]](../../data-types/consents.md) ao schema por meio do uso de um mixin [personalizado](../../ui/resources/mixins.md#create).

## Estrutura de mistura {#structure}

>[!IMPORTANT]
>
>A combinação [!DNL Consents & Preferences] foi projetada para abranger uma variedade de casos de uso de consentimento e gerenciamento de preferências. Como resultado, este documento descreve o uso dos campos do mixin em termos gerais, e só faz sugestões sobre como você deve interpretar o uso desses campos. Consulte sua equipe jurídica de privacidade para alinhar a estrutura do mixin com a forma como sua organização interpreta e apresenta essas opções de consentimento e preferência aos clientes.

O mixin [!DNL Consents & Preferences] fornece vários campos usados para capturar informações **consent** e **preferência**.

Um consentimento é uma opção que permite ao cliente especificar como seus dados podem ser usados. A maioria dos consentimentos tem um aspecto legal, na medida em que algumas jurisdições exigem a obtenção de permissão antes que os dados possam ser usados de uma maneira específica, ou exigem que o cliente tenha a opção de interromper esse uso (recusa) se não for necessário consentimento afirmativo.

Uma preferência é uma opção que permite ao cliente especificar como os diferentes aspectos de sua experiência com uma marca devem ser tratados. Eles se encaixam em duas categorias:

* **Preferências** de personalização: Preferências sobre como a marca deve personalizar experiências entregues a um cliente.
* **Preferências** de marketing: Preferências sobre se uma marca tem permissão para entrar em contato com um cliente por meio de vários canais.

A captura de tela a seguir mostra como a estrutura da mistura é representada na interface do usuário da plataforma:

![](../../images/mixins/consent.png)

>[!TIP]
>
>Consulte o guia em [exploração de recursos XDM](../../ui/explore.md) para obter etapas sobre como pesquisar qualquer recurso XDM e inspecionar sua estrutura na interface do usuário da plataforma.

O JSON a seguir mostra um exemplo do tipo de dados que a mistura [!DNL Consents & Preferences] pode processar. As informações sobre o uso específico de cada um desses campos são fornecidas nas seções a seguir.

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


## Casos de uso do campo

Os casos de uso planejados para cada um desses campos são fornecidos nas seções abaixo.

### `collect`

`collect` representa o consentimento do cliente em ter seus dados coletados.

```json
"collect" : {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para esse caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### `share`

`share` representa o consentimento do cliente para saber se seus dados podem ser compartilhados com (ou vendidos a) terceiros.

```json
"share" : {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para esse caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### `personalize` {#personalize}

`personalize` O captura as preferências do cliente sobre quais maneiras seus dados podem ser usados para personalização. Os clientes podem recusar casos de uso de personalização específica ou recusar totalmente a personalização.

>[!IMPORTANT]
>
>`personalize` não abrange casos de uso de marketing. Por exemplo, se um cliente recusar a personalização de todos os canais, ele não deverá parar de receber comunicações por meio desses canais. Em vez disso, as mensagens recebidas devem ser genéricas e não baseadas no seu perfil.
>
>Pelo mesmo exemplo, se um cliente recusar o marketing direto para todos os canais (por meio de `marketing`, explicado na [próxima seção](#marketing)), então esse cliente não deverá receber mensagens, mesmo que a personalização seja permitida.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `content` | Representa as preferências do cliente para conteúdo personalizado em seu site ou aplicativo. |
| `val` | A preferência de personalização fornecida pelo cliente para o caso de uso especificado. Nos casos em que o cliente não precisa ser solicitado a fornecer o consentimento, o valor desse campo deve indicar a base em que a personalização deve ocorrer. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### `marketing` {#marketing}

`marketing` O captura as preferências do cliente com relação aos fins de marketing para os quais seus dados podem ser usados. Os clientes podem recusar casos de uso de marketing específicos ou recusar totalmente o marketing direto.

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `preferred` | Indica o canal preferencial do cliente para receber comunicações. Consulte o [apêndice](#preferred-values) para obter os valores aceitos. |
| `any` | Representa as preferências do cliente para o marketing direto como um todo. A preferência de consentimento fornecida neste campo é considerada a preferência &quot;padrão&quot; para qualquer canal de marketing, a menos que seja substituída por subcampos adicionais fornecidos em `marketing`. Se você planeja usar opções de consentimento mais granulares, é recomendável excluir esse campo.<br><br>Se o valor estiver definido como  `n`, então todas as configurações de personalização mais específicas deverão ser ignoradas. Se o valor estiver definido como `y`, então todas as opções de personalização com granularidade mais fina também deverão ser tratadas como `y`, a menos que explicitamente definidas como `n`. Se o valor não for definido, os valores para cada opção de personalização deverão ser honrados conforme especificado. |
| `email` | Indica se o cliente concorda em receber mensagens de email. O cliente também pode fornecer preferências para assinaturas individuais dentro desse canal. Consulte a seção [subscriptions](#subscriptions) abaixo para obter mais informações. |
| `push` | Indica se o cliente permite receber notificações por push. O cliente também pode fornecer preferências para assinaturas individuais dentro desse canal. Consulte a seção [subscriptions](#subscriptions) abaixo para obter mais informações. |
| `sms` | Indica se o cliente concorda em receber mensagens de texto. O cliente também pode fornecer preferências para assinaturas individuais dentro desse canal. Consulte a seção [subscriptions](#subscriptions) abaixo para obter mais informações. |
| `val` | A preferência fornecida pelo cliente para o caso de uso especificado. Nos casos em que o cliente não tenha que ser solicitado a fornecer o consentimento, o valor desse campo deve indicar a base em que o caso de uso de marketing deve ocorrer. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |
| `time` | Um carimbo de data e hora ISO 8601 de quando a preferência de marketing foi alterada, se aplicável. Observe que, se o carimbo de data e hora de qualquer preferência individual for igual ao fornecido em `metadata`, esse campo não precisará ser definido para essa preferência. |
| `reason` | Quando um cliente recusa um caso de uso de marketing, esse campo de cadeia de caracteres representa o motivo pelo qual o cliente optou por não participar. |

#### `subscriptions` {#subscriptions}

As propriedades `email`, `push` e `sms` do objeto `marketing` podem representar as assinaturas do cliente para esses canais individuais. Isso é feito adicionando uma propriedade `subscriptions` ao canal de marketing em questão.

```json
"marketing": {
  "email": {
    "val": "y",
    "subscriptions": {
      "daily-mail": {
        "val": "y",
        "type": "paid",
        "subscribers": {
          "john@xyz.com": {
            "time": "2019-01-01T15:52:25+00:00",
            "source": "website"
          }
        }
      },
      "shipped": {
        "val": "y",

        "subscribers": {
          "john@xyz.com": {
            "time": "2021-01-01T08:32:53+07:00",
            "source": "website"
          },
          "jane@xyz.com": {
            "time": "2020-02-03T07:54:21+07:00",
            "source": "call center",
          }
        }
      }
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de assinatura. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos. |
| `subscribers` | Um campo opcional tipo mapa que representa um conjunto de identificadores (como endereços de email ou números de telefone) que assinaram uma assinatura específica. Cada chave nesse objeto representa o identificador em questão e contém duas subpropriedades: <ul><li>`time`: Um carimbo de data e hora ISO 8601, de quando a identidade é subscrita, se aplicável.</li><li>`source`: A origem do assinante. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos.</li></ul> |


### `metadata`

`metadata` captura metadados gerais sobre os consentimentos e preferências do cliente sempre que foram atualizados pela última vez.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriedade | Descrição |
| --- | --- |
| `time` | Um carimbo de data e hora ISO 8601 para a última vez que qualquer consentimento e preferência do cliente foi atualizado. Esse campo pode ser usado em vez de aplicar carimbos de data e hora a preferências individuais para reduzir a carga e a complexidade. Fornecer um valor `time` em uma preferência individual substitui o carimbo de data e hora `metadata` dessa preferência específica. |

### `idSpecific`

`idSpecific` pode ser usado quando um consentimento ou preferência específico não se aplica universalmente a um cliente, mas é restrito a um único dispositivo ou ID. Por exemplo, um cliente pode recusar o recebimento de emails para um endereço, enquanto pode permitir emails em outro.

>[!IMPORTANT]
>
>Os consentimentos e preferências de nível de canal (ou seja, aqueles fornecidos em `consents` fora de `idSpecific`) se aplicam às IDs nesse canal. Portanto, todos os consentimentos e preferências no nível do canal afetam diretamente se configurações equivalentes específicas de ID ou dispositivo são respeitadas:
>
>* Se o cliente tiver optado por não participar no nível do canal, quaisquer consentimentos ou preferências equivalentes em `idSpecific` serão ignorados.
>* Se o consentimento ou a preferência no nível do canal não estiver definida ou o cliente tiver optado por participar, os consentimentos ou preferências equivalentes em `idSpecific` serão honrados.


Cada chave no objeto `idSpecific` representa um namespace de identidade específico reconhecido pelo Adobe Experience Platform Identity Service. Embora você possa definir seus próprios namespaces personalizados para categorizar identificadores diferentes, é recomendável usar um dos namespaces padrão fornecidos pelo Serviço de identidade para reduzir os tamanhos de armazenamento para o Perfil do cliente em tempo real. Para obter mais informações sobre namespaces de identidade, consulte a [visão geral do namespace de identidade](../../../identity-service/namespaces.md) na documentação do Serviço de identidade.

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
  "ECID" : {
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

Nos objetos `marketing` fornecidos na seção `idSpecific`, os campos `any` e `preferred` não são compatíveis. Esses campos só podem ser configurados no nível do usuário. Além disso, as `idSpecific` preferências de marketing para `email`, `sms` e `push` não são compatíveis com os campos `subscriptions`.

Também há um consentimento que só pode ser fornecido na seção `idSpecific`: `adID`. Este campo é coberto pela subseção abaixo.

#### `adID`

O consentimento `adID` representa o consentimento do cliente para saber se uma ID do anunciante (IDFA ou GAID) pode ser usada para vincular o cliente entre aplicativos neste dispositivo. Esse valor só pode ser configurado no namespace de identidade `ECID` na seção `idSpecific` e não pode ser definido para outros namespaces ou no nível do usuário para esse mixin.

```json
"idSpecific": {
  "ECID" : {
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

## Inserir dados usando o mixin {#ingest}

Para usar o mixin [!DNL Consents & Preferences] para assimilar dados de consentimento dos clientes, é necessário criar um conjunto de dados com base em um schema que contenha esse mixin.

Consulte o tutorial em [criar um esquema na interface do usuário](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para obter etapas sobre como atribuir mixins a campos. Depois de criar um schema contendo um campo com a combinação [!DNL Consents & Preferences], consulte a seção sobre [criar um conjunto de dados](../../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, seguindo as etapas para criar um conjunto de dados com um esquema existente.

>[!IMPORTANT]
>
>Se desejar enviar dados de consentimento para [!DNL Real-time Customer Profile], é necessário criar um schema habilitado para [!DNL Profile] com base na classe [!DNL XDM Individual Profile] que contém a mesclagem [!DNL Consents & Preferences]. O conjunto de dados criado com base nesse esquema também deve ser habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para etapas específicas relacionadas aos requisitos [!DNL Real-time Customer Profile] para schemas e conjuntos de dados.
>
>Além disso, também é necessário garantir que suas políticas de mesclagem estejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral sobre [mesclar políticas](../../../rtcdp/profile/merge-policies.md) para obter mais informações.

## Lidar com alterações de consentimento e preferência

Quando um cliente altera seus consentimentos ou preferências no seu site, essas alterações devem ser coletadas e aplicadas imediatamente usando o [Adobe Experience Platform Web SDK](../../../edge/consent/supporting-consent.md). Se um cliente recusar a coleta de dados, toda a coleta de dados deverá ser interrompida imediatamente. Se um cliente recusar a personalização, então não deverá haver personalização na próxima página que visitar.

## Apêndice {#appendix}

As seções abaixo fornecem informações de referência adicionais sobre a mistura [!DNL Consents & Preferences].

### Valores aceitos para `val` {#choice-values}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Title | Descrição |
| --- | --- | --- |
| `y` | Sim | O cliente aceitou o consentimento ou a preferência. Em outras palavras, eles **do** consentiram com o uso de seus dados, conforme indicado pelo consentimento ou preferência em questão. |
| `n` | Não | O cliente recusou o consentimento ou a preferência. Em outras palavras, eles **não** consentiram com o uso de seus dados, conforme indicado pelo consentimento ou preferência em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu um consentimento ou valor de preferência final. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que selecione um link em um email para verificar se forneceu o endereço de email correto, momento em que o consentimento seria atualizado para `y`.<br><br>Se esse consentimento ou preferência não usar um processo de verificação de dois conjuntos, a  `p` escolha poderá ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor para `p` na primeira página de um site, antes que o cliente tenha respondido ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de consentimento ou preferência do cliente são desconhecidas. |
| `LI` | Interesse legítimo | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera o potencial dano que isso representa para o indivíduo. |
| `CT` | Contrato | A recolha de dados para o fim especificado é necessária para cumprir as obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para o fim especificado é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para o fim especificado é necessária para levar a cabo uma missão de interesse público ou no exercício da autoridade oficial. |

### Valores aceitos para `preferred` {#preferred-values}

A tabela a seguir descreve os valores aceitos para `preferred`:

| Valor | Descrição |
| --- | --- |
| `email` | Mensagens de email. |
| `push` | Notificações por push. |
| `inApp` | Mensagens no aplicativo. |
| `sms` | Mensagens SMS. |
| `phone` | Interações de chamada telefônica. |
| `phyMail` | Correio físico. |
| `inVehicle` | Mensagens no veículo. |
| `inHome` | Mensagens na casa. |
| `iot` | Mensagens de Internet of stuff (IoT). |
| `social` | Conteúdo de redes sociais. |
| `other` | Um canal que não se encaixa em uma categoria padrão. |
| `none` | Nenhum canal preferencial. |
| `unknown` | O canal preferido é desconhecido. |

### Schema [!DNL Consents & Preferences] completo {#full-schema}

Para exibir o esquema completo da mistura [!DNL Consents & Preferences], consulte o [repositório XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).

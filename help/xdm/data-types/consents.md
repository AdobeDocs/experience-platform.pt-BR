---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;consentimento;Consentimento;preferências;Preferências;privacidadeOptOuts;marketingPreferences;optOutType;basedOfProcessing;consentimento;Consent
title: Tipo de dados de consentimentos e preferências
description: O tipo de dados Preferências de privacidade/marketing (Consentimento) é destinado a suportar a coleta de permissões e preferências do cliente geradas pelas Plataformas de gerenciamento de consentimento (CMPs) e outras fontes das operações de dados.
topic: guide
translation-type: tm+mt
source-git-commit: caebdcd48e03bd8b91da624532569b55d8696fb4
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 1%

---


# [!DNL Consents & Preferences] tipo de dados

O tipo de dados [!DNL Privacy/Marketing Preferences (Consent)] (a seguir denominado &quot;[!DNL Consents & Preferences] tipo de dados&quot;) é um tipo de dados [!DNL Experience Data Model] (XDM) destinado a suportar a coleta de permissões e preferências do cliente geradas pelas Plataformas de Gerenciamento de Consentimento (CMPs) e outras fontes de suas operações de dados.

Este documento cobre a estrutura e o uso pretendido dos campos fornecidos pelo tipo de dados [!DNL Consents & Preferences].

## Pré-requisitos {#prerequisites}

Este documento requer uma compreensão funcional do XDM e o uso dos schemas em [!DNL Experience Platform]. Consulte a seguinte documentação antes de continuar:

* [Visão geral do sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Noções básicas da composição do schema](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Estrutura do tipo de dados {#structure}

>[!IMPORTANT]
>
>O tipo de dados [!DNL Consents & Preferences] foi projetado para abranger uma variedade de casos de uso de consentimento e gerenciamento de preferências. Como resultado, este documento descreve o uso dos campos do tipo de dados em termos gerais, e apenas faz sugestões sobre como você deve interpretar o uso desses campos. Consulte a sua equipe jurídica de privacidade para alinhar a estrutura do tipo de dados com a forma como a sua organização interpreta e apresenta essas opções de consentimento e preferência aos seus clientes.

O tipo de dados [!DNL Consents & Preferences] fornece vários campos usados para capturar informações **consentimento** e **preferenciais**.

Um consentimento é uma opção que permite ao cliente especificar como seus dados podem ser usados. A maioria dos consentimentos tem um aspecto legal, na medida em que algumas jurisdições exigem a obtenção de permissão antes que os dados possam ser usados de uma forma específica, ou exigem que o cliente tenha a opção de interromper esse uso (opt out) se não for necessário o consentimento afirmativo.

Uma preferência é uma opção que permite ao cliente especificar como diferentes aspectos de sua experiência com uma marca devem ser tratados. Elas se encaixam em duas categorias:

* **Preferências** de personalização: Preferências sobre como a marca deve personalizar as experiências entregues a um cliente.
* **Preferências** de marketing: Preferências relativas à permissão de uma marca para entrar em contato com um cliente por meio de vários canais.

O JSON a seguir mostra um exemplo do tipo de dados que o tipo de dados [!DNL Consents & Preferences] pode processar. As informações sobre o uso específico de cada um desses campos são fornecidas nas seções a seguir.

```json
{
  "xdm:consents": {
    "xdm:collect": {
      "xdm:val": "y",
    },
    "xdm:adID": {
      "xdm:val": "VI"
    },
    "xdm:share": {
      "xdm:val": "y",
    },
    "xdm:personalize": {
      "xdm:content": {
        "xdm:val": "y"
      }
    },
    "xdm:marketing": {
      "xdm:preferred": "email",
      "xdm:any": {
        "xdm:val": "u"
      },
      "xdm:push": {
        "xdm:val": "n",
        "xdm:reason": "Too Frequent",
        "xdm:time": "2019-01-01T15:52:25+00:00"
      }
    },
    "xdm:idSpecific": {
      "email": {
        "jdoe@example.com": {
          "xdm:marketing": {
            "xdm:email": {
              "xdm:val": "n"
            }
          }
        }
      }
    }
  },
  "xdm:metadata": {
    "xdm:time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>O exemplo acima serve para ilustrar a estrutura dos dados enviados para [!DNL Platform] por meio do tipo de dados [!DNL Consents & Preferences], a fim de contextualizar o restante desse documento, o que explica os principais campos fornecidos pelo tipo de dados. O schema completo da estrutura do tipo de dados pode ser encontrado no [apêndice](#full-schema) para fins de referência.

## xdm:consents {#choices}

`xdm:consents` contém vários campos que descrevem os consentimentos e preferências de um cliente. Esses campos são descritos com mais detalhes nas subseções abaixo.

```json
"xdm:consents": {
  "xdm:collect": {
    "xdm:val": "y",
  },
  "xdm:adID": {
    "xdm:val": "VI"
  },
  "xdm:share": {
    "xdm:val": "y",
  },
  "xdm:personalize": {
    "xdm:content": {
      "xdm:val": "y"
    }
  },
  "xdm:marketing": {
    "xdm:preferred": "email",
    "xdm:any": {
      "xdm:val": "u"
    },
    "xdm:email": {
      "xdm:val": "n",
      "xdm:reason": "Too Frequent",
      "xdm:time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### xdm:collect

`xdm:collect` representa o consentimento do cliente em ter seus dados coletados.

```json
"xdm:collect" : {
  "xdm:val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:val` | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### xdm:adID

`xdm:adID` representa o consentimento do cliente para saber se uma ID do anunciante (IDFA ou GAID) pode ser usada para vincular o cliente aos aplicativos neste dispositivo.

```json
"xdm:adID" : {
  "xdm:val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:val` | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### xdm:share

`xdm:share` representa o consentimento do cliente para saber se os dados podem ser compartilhados com (ou vendidos a) terceiros.

```json
"xdm:share" : {
  "xdm:val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:val` | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### xdm:personalize {#personalize}

`xdm:personalize` captura as preferências do cliente em relação às maneiras pelas quais seus dados podem ser usados para personalização. Os clientes podem opt out casos de uso de personalização específicos ou opt out totalmente a personalização.

>[!IMPORTANT]
>
>`xdm:personalize` não abrange os casos de utilização da comercialização. Por exemplo, se um cliente opt out da personalização para todos os canais, ele não deve parar de receber comunicações através desses canais. Em vez disso, as mensagens que recebem devem ser genéricas e não baseadas no seu perfil.
>
>Pelo mesmo exemplo, se um cliente opt out do marketing direto para todos os canais (por meio de `xdm:marketing`, explicado na [próxima seção](#marketing)), então esse cliente não deverá receber nenhuma mensagem, mesmo que a personalização seja permitida.

```json
"xdm:personalize": {
  "xdm:content": {
    "xdm:val": "y",
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:content` | Representa as preferências do cliente para conteúdo personalizado em seu site ou aplicativo. |
| `xdm:val` | A preferência de personalização fornecida pelo cliente para o caso de uso especificado. Nos casos em que o cliente não tenha que ser solicitado a fornecer o consentimento, o valor deste campo deve indicar a base em que a personalização deve ocorrer. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

### xdm:marketing {#marketing}

`xdm:marketing` captura as preferências do cliente em relação a quais fins de marketing seus dados podem ser usados. Os clientes podem opt out casos específicos de uso de marketing ou opt out totalmente o marketing direto.

```json
"xdm:marketing": {
  "xdm:preferred": "email",
  "xdm:any": {
    "xdm:val": "u"
  },
  "xdm:email": {
    "xdm:val": "n",
    "xdm:reason": "Too Frequent"
  },
  "xdm:push": {
    "xdm:val": "y"
  },
  "xdm:sms": {
    "xdm:val": "y"
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:preferred` | Indica o canal preferencial do cliente para receber comunicações. Consulte o [apêndice](#preferred-values) para obter os valores aceitos. |
| `xdm:any` | Representa as preferências do cliente para marketing direto como um todo. A preferência de consentimento fornecida neste campo é considerada a preferência &quot;padrão&quot; para qualquer canal de marketing, a menos que seja substituída por subcampos adicionais fornecidos em `xdm:marketing`. Se você planeja usar opções de consentimento mais granulares, é recomendável excluir esse campo.<br><br>Se o valor estiver definido como  `n`, então todas as configurações de personalização mais específicas devem ser ignoradas. Se o valor for definido como `y`, todas as opções de personalização de granulação fina também deverão ser tratadas como `y`, a menos que explicitamente definidas como `n`. Se o valor não estiver definido, então os valores para cada opção de personalização devem ser respeitados conforme especificado. |
| `xdm:email` | Indica se o cliente concorda em receber mensagens de email. |
| `xdm:push` | Indica se o cliente permite receber notificações por push. |
| `xdm:sms` | Indica se o cliente concorda em receber mensagens de texto. |
| `xdm:val` | A preferência fornecida pelo cliente para o caso de uso especificado. Nos casos em que o cliente não tenha de ser solicitado a dar o seu consentimento, o valor deste campo deve indicar a base em que o caso de utilização para comercialização deve ter lugar. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |
| `xdm:time` | Um carimbo de data e hora ISO 8601 de quando a preferência de marketing mudou, se aplicável. Observe que se o carimbo de data e hora de qualquer preferência individual for igual ao fornecido em `xdm:metadata`, esse campo não precisará ser definido para essa preferência. |
| `xdm:reason` | Quando um cliente opt out de um caso de uso de marketing, esse campo de string representa o motivo pelo qual o cliente opt out. |

### xdm:idSpecific

`xdm:idSpecific` pode ser usado quando um consentimento ou preferência específica não se aplica universalmente a um cliente, mas está restrito a um único dispositivo ou ID. Por exemplo, um cliente pode opt out de receber emails para um endereço, ao mesmo tempo que pode permitir emails em outro.

>[!IMPORTANT]
>
>Os consentimentos e preferências de nível de canal (ou seja, aqueles fornecidos em `xdm:consents` fora de `xdm:idSpecific`) se aplicam às IDs dentro desse canal. Portanto, todos os consentimentos e preferências em nível de canal afetam diretamente se configurações equivalentes específicas de ID ou dispositivo são respeitadas:
>
>* Se o cliente tiver opt out no nível do canal, quaisquer consentimentos ou preferências equivalentes em `xdm:idSpecific` serão ignorados.
>* Se o consentimento ou preferência em nível de canal não estiver definido, ou o cliente tiver opt in, os consentimentos ou preferências equivalentes em `xdm:idSpecific` serão respeitados.


Cada chave no objeto `xdm:idSpecific` representa uma namespace de identidade específica reconhecida pelo Adobe Experience Platform Identity Service. Embora você possa definir suas próprias namespaces personalizadas para categorizar identificadores diferentes, recomenda-se usar uma das namespaces padrão fornecidas pelo Serviço de identidade para reduzir os tamanhos dos armazenamentos para o Perfil do cliente em tempo real. Para obter mais informações sobre namespaces de identidade, consulte [visão geral da namespace de identidade](../../identity-service/namespaces.md) na documentação do Serviço de identidade.

As chaves para cada objeto de namespace representam os valores de identidade exclusivos para os quais o cliente definiu preferências. Cada valor de identidade pode conter um conjunto completo de consentimentos e preferências, formatados da mesma forma que `xdm:consents`.

```json
"xdm:idSpecific": {
  "email": {
    "jdoe@example.com": {
      "xdm:marketing": {
        "xdm:email": {
          "xdm:val": "n"
        }
      }
    }
  }
}
```

## xdm:metadados

`xdm:metadata` captura metadados gerais sobre os consentimentos e preferências do cliente sempre que foram atualizados pela última vez.

```json
"xdm:metadata": {
  "xdm:time": "2019-01-01T15:52:25+00:00",
}
```

| Propriedade | Descrição |
| --- | --- |
| `xdm:time` | Um carimbo de data e hora da última vez que qualquer um dos consentimentos e preferências do cliente foi atualizado. Esse campo pode ser usado em vez de aplicar carimbos de data e hora às preferências individuais para reduzir a carga e a complexidade. Fornecer um valor `xdm:time` sob uma preferência individual substitui o carimbo de data e hora `xdm:metadata` dessa preferência específica. |

## Como inserir dados usando o tipo de dados {#ingest}

Para usar o tipo de dados [!DNL Consents & Preferences] para assimilar dados de consentimento de seus clientes, você deve criar um conjunto de dados com base em um schema que contenha esse tipo de dados.

Consulte o tutorial em [criar um schema na interface do usuário](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) para obter etapas sobre como atribuir tipos de dados a campos. Depois de criar um schema contendo um campo com o tipo de dados [!DNL Consents & Preferences], consulte a seção em [criar um conjunto de dados](../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, seguindo as etapas para criar um conjunto de dados com um schema existente.

>[!IMPORTANT]
>
>Se quiser enviar dados de consentimento para [!DNL Real-time Customer Profile], é necessário criar um schema habilitado para [!DNL Profile] com base na classe [!DNL XDM Individual Profile] que contenha o tipo de dados [!DNL Consents & Preferences]. O conjunto de dados que você cria com base nesse schema também deve estar habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para obter etapas específicas relacionadas aos requisitos [!DNL Real-time Customer Profile] para schemas e conjuntos de dados.
>
>Além disso, você também deve garantir que suas políticas de mesclagem estejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral sobre [políticas de mesclagem](../../rtcdp/profile/merge-policies.md) para obter mais informações.

## Tratamento de alterações de consentimento e preferência

Quando um cliente altera seus consentimentos ou preferências em seu site, essas alterações devem ser coletadas e aplicadas imediatamente usando o [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Se um cliente opt out da coleta de dados, toda a coleta de dados deverá cessar imediatamente. Se um cliente opt out da personalização, não deverá haver personalização presente na próxima página que visitar.

## Apêndice {#appendix}

As seções abaixo fornecem informações de referência adicionais relacionadas ao tipo de dados [!DNL Consents & Preferences].

### Valores aceitos para xdm:val {#choice-values}

A tabela a seguir descreve os valores aceitos para `xdm:val`:

| Valor | Title | Descrição |
| --- | --- | --- |
| `y` | Sim | O cliente opt in o consentimento ou preferência. Em outras palavras, eles **do** consentiram na utilização de seus dados conforme indicado pelo consentimento ou preferência em questão. |
| `n` | Não | O cliente opt out do consentimento ou preferência. Por outras palavras, **não** consentiram na utilização dos seus dados, tal como indicado pelo consentimento ou preferência em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu o consentimento ou valor preferencial final. Isso é usado com mais frequência como parte de um consentimento que requer uma verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que selecione um link em um email para verificar se ele forneceu o endereço de email correto, e em que ponto o consentimento será atualizado para `y`.<br><br>Se esse consentimento ou preferência não usar um processo de verificação de dois conjuntos, então a  `p` escolha pode ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor como `p` na primeira página de um site, antes que o cliente responda ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não opt out explicitamente (ou seja, o consentimento é assumido). |
| `u` | Desconhecido | As informações de consentimento ou preferência do cliente são desconhecidas. |
| `LI` | Interesse legítimo | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera os possíveis danos que isso representa para o indivíduo. |
| `CT` | Contrato | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações contratuais com a pessoa singular. |
| `CP` | Cumprimento de uma obrigação legal | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para a finalidade especificada é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para o fim especificado é necessária para efetuar uma tarefa do interesse público ou para o exercício da autoridade pública. |

### Valores aceitos para xdm:preferencial {#preferred-values}

A tabela a seguir descreve os valores aceitos para `xdm:preferred`:

| Valor | Descrição |
| --- | --- |
| `email` | Mensagens de email. |
| `push` | Notificações por push. |
| `inApp` | Mensagens no aplicativo. |
| `sms` | Mensagens SMS. |
| `phone` | Interações de chamadas telefônicas. |
| `phyMail` | Correio físico. |
| `inVehicle` | Mensagens no veículo. |
| `inHome` | Mensagens internas. |
| `iot` | Mensagens de Internet das coisas (IoT). |
| `social` | Conteúdo de mídia social. |
| `other` | Um canal que não se encaixa em uma categoria padrão. |
| `none` | Nenhum canal preferencial. |
| `unknown` | O canal preferencial é desconhecido. |

### Schema [!DNL Consents & Preferences] completo {#full-schema}

Para visualização do schema completo para o tipo de dados [!DNL Consents & Preferences], consulte [repositório XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent-preferences.schema.json).

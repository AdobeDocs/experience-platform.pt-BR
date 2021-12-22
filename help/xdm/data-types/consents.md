---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, consentimento, preferências, Preferências, privacidade, OptOuts, marketingPreferences, optOutType, baseOfProcessing, consentimento, Consentimento
title: Tipo de dados de consentimentos e preferências
description: O tipo de dados Consent for Privacy, Personalization and Marketing Preferences tem como objetivo oferecer suporte à coleta de permissões e preferências do cliente geradas pelas CMPs (Consent Management Platforms) e outras fontes de suas operações de dados.
topic-legacy: guide
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 04e778d3318d60733772c2042c8bb272f0c87d5c
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 2%

---

# [!UICONTROL Consentimentos e preferências] tipo de dados

O [!UICONTROL Consentimento para privacidade, personalização e preferências de marketing] tipo de dados (a seguir designado por &quot;[!UICONTROL Consentimentos e preferências] data type&quot;) é um [!DNL Experience Data Model] (XDM) tipo de dados que tem como objetivo oferecer suporte à coleta de permissões e preferências do cliente geradas pelas Plataformas de gerenciamento de consentimento (CMPs) e outras fontes de suas operações de dados.

Este documento cobre a estrutura e o uso pretendido dos campos fornecidos pelo [!UICONTROL Consentimentos e preferências] tipo de dados.

## Pré-requisitos {#prerequisites}

Este documento requer uma compreensão funcional do XDM e o uso dos esquemas no [!DNL Experience Platform]. Consulte a seguinte documentação antes de continuar:

* [Visão geral do sistema XDM](https://www.adobe.com/go/xdm-home-en)
* [Noções básicas da composição do schema](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Estrutura do tipo de dados {#structure}

>[!IMPORTANT]
>
>O [!UICONTROL Consentimentos e preferências] O tipo de dados é projetado para abranger uma variedade de casos de uso de consentimento e de gerenciamento de preferências. Como resultado, este documento descreve o uso dos campos do tipo de dados em termos gerais e só faz sugestões sobre como você deve interpretar o uso desses campos. Consulte sua equipe jurídica de privacidade para alinhar a estrutura do tipo de dados com a forma como sua organização interpreta e apresenta essas opções de consentimento e preferência aos clientes.

O [!UICONTROL Consentimentos e preferências] o tipo de dados fornece vários campos usados para capturar **consentimento** e **preferência** informações.

Um consentimento é uma opção que permite ao cliente especificar como seus dados podem ser usados. A maioria dos consentimentos tem um aspecto legal, na medida em que algumas jurisdições exigem a obtenção de permissão antes que os dados possam ser usados de uma maneira específica, ou exigem que o cliente tenha a opção de interromper esse uso (recusa) se não for necessário consentimento afirmativo.

Uma preferência é uma opção que permite ao cliente especificar como os diferentes aspectos de sua experiência com uma marca devem ser tratados. Eles se encaixam em duas categorias:

* **Preferências de personalização**: Preferências sobre como a marca deve personalizar experiências entregues a um cliente.
* **Preferências de marketing**: Preferências sobre se uma marca tem permissão para entrar em contato com um cliente por meio de vários canais.

A captura de tela a seguir mostra como a estrutura do tipo de dados é representada na interface do usuário da plataforma:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulte o guia sobre [exploração de recursos XDM](../ui/explore.md) para obter etapas sobre como pesquisar qualquer recurso XDM e inspecionar sua estrutura na interface do usuário da plataforma.

O JSON a seguir mostra um exemplo do tipo de dados que a variável [!UICONTROL Consentimentos e preferências] o tipo de dados pode ser processado. As informações sobre o uso específico de cada um desses campos são fornecidas nas seções a seguir.

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "adID": {
      "val": "VI"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
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
>* [Gerar dados de amostra na interface do usuário](../ui/sample.md)
>* [Gerar dados de amostra na API](../api/sample-data.md)


## `consents` {#choices}

`consents` contém vários campos que descrevem os consentimentos e preferências de um cliente. Esses campos são descritos com mais detalhes nas subseções abaixo.

```json
"consents": {
  "collect": {
    "val": "y",
  },
  "adID": {
    "val": "VI"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` representa o consentimento do cliente em ter seus dados coletados.

```json
"collect": {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para esse caso de uso. Consulte a [apêndice](#choice-values) para os valores e definições aceites. |

{style=&quot;table-layout:auto&quot;}

### `adID`

`adID` representa o consentimento do cliente para que uma ID do anunciante (IDFA ou GAID) possa ser usada para vincular o cliente entre aplicativos neste dispositivo.

```json
"adID": {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para esse caso de uso. Consulte a [apêndice](#choice-values) para os valores e definições aceites. |

{style=&quot;table-layout:auto&quot;}

### `share`

`share` representa o consentimento do cliente para saber se seus dados podem ser compartilhados com (ou vendidos a) terceiros.

```json
"share": {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para esse caso de uso. Consulte a [apêndice](#choice-values) para os valores e definições aceites. |

{style=&quot;table-layout:auto&quot;}

### `personalize` {#personalize}

`personalize` O captura as preferências do cliente sobre quais maneiras seus dados podem ser usados para personalização. Os clientes podem recusar casos de uso de personalização específica ou recusar totalmente a personalização.

>[!IMPORTANT]
>
>`personalize` não abrange casos de uso de marketing. Por exemplo, se um cliente recusar a personalização de todos os canais, ele não deverá parar de receber comunicações por meio desses canais. Em vez disso, as mensagens recebidas devem ser genéricas e não baseadas no seu perfil.
>
>Pelo mesmo exemplo, se um cliente optar por não participar do marketing direto para todos os canais (por meio de `marketing`, explicadas na [próxima seção](#marketing)), esse cliente não deve receber mensagens, mesmo que a personalização seja permitida.

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
| `val` | A preferência de personalização fornecida pelo cliente para o caso de uso especificado. Nos casos em que o cliente não precisa ser solicitado a fornecer o consentimento, o valor desse campo deve indicar a base em que a personalização deve ocorrer. Consulte a [apêndice](#choice-values) para os valores e definições aceites. |

{style=&quot;table-layout:auto&quot;}

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
| `preferred` | Indica o canal preferencial do cliente para receber comunicações. Consulte a [apêndice](#preferred-values) para obter valores aceitos. |
| `any` | Representa as preferências do cliente para o marketing direto como um todo. A preferência de consentimento fornecida neste campo é considerada a preferência &quot;padrão&quot; de qualquer canal de marketing, a menos que seja substituída por subcampos adicionais fornecidos em `marketing`. Se você planeja usar opções de consentimento mais granulares, é recomendável excluir esse campo.<br><br>Se o valor estiver definido como `n`, todas as configurações de personalização mais específicas devem ser ignoradas. Se o valor estiver definido como `y`, então todas as opções de personalização otimizadas também devem ser tratadas como `y`, a menos que explicitamente definido como `n`. Se o valor não for definido, os valores para cada opção de personalização deverão ser honrados conforme especificado. |
| `email` | Indica se o cliente concorda em receber mensagens de email. |
| `push` | Indica se o cliente permite receber notificações por push. |
| `sms` | Indica se o cliente concorda em receber mensagens de texto. |
| `val` | A preferência fornecida pelo cliente para o caso de uso especificado. Nos casos em que o cliente não tenha que ser solicitado a fornecer o consentimento, o valor desse campo deve indicar a base em que o caso de uso de marketing deve ocorrer. Consulte a [apêndice](#choice-values) para os valores e definições aceites. |
| `time` | Um carimbo de data e hora ISO 8601 de quando a preferência de marketing foi alterada, se aplicável. Observe que, se o carimbo de data e hora de qualquer preferência individual for o mesmo que o fornecido em `metadata`, esse campo não deve ser definido para essa preferência. |
| `reason` | Quando um cliente recusa um caso de uso de marketing, esse campo de cadeia de caracteres representa o motivo pelo qual o cliente optou por não participar. |

{style=&quot;table-layout:auto&quot;}

### `metadata`

`metadata` captura metadados gerais sobre os consentimentos e preferências do cliente sempre que foram atualizados pela última vez.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriedade | Descrição |
| --- | --- |
| `time` | Um carimbo de data e hora ISO 8601 para a última vez que qualquer consentimento e preferência do cliente foi atualizado. Esse campo pode ser usado em vez de aplicar carimbos de data e hora a preferências individuais para reduzir a carga e a complexidade. Fornecer uma `time` em uma preferência individual, o valor substitui `metadata` carimbo de data e hora dessa preferência específica. |

{style=&quot;table-layout:auto&quot;}

## Inserção de dados usando o tipo de dados {#ingest}

Para usar o [!UICONTROL Consentimentos e preferências] para assimilar dados de consentimento dos clientes, é necessário criar um conjunto de dados com base em um esquema que contenha esse tipo de dados.

Veja o tutorial em [criação de um schema na interface do usuário](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) para obter etapas sobre como atribuir tipos de dados a campos. Depois de criar um schema contendo um campo com a variável [!UICONTROL Consentimentos e preferências] tipo de dados, consulte a seção em [criação de um conjunto de dados](../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, siga as etapas para criar um conjunto de dados com um esquema existente.

>[!IMPORTANT]
>
>Se desejar enviar dados de consentimento para o [!DNL Real-time Customer Profile], é necessário criar um [!DNL Profile]-enabled schema baseado no [!DNL XDM Individual Profile] classe que contém [!UICONTROL Consentimentos e preferências] tipo de dados. O conjunto de dados criado com base nesse esquema também deve ser habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para etapas específicas relacionadas a [!DNL Real-time Customer Profile] requisitos para esquemas e conjuntos de dados.
>
>Além disso, também é necessário garantir que suas políticas de mesclagem estejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral em [políticas de mesclagem](../../rtcdp/profile/merge-policies.md) para obter mais informações.

## Lidar com alterações de consentimento e preferência

Quando um cliente altera seus consentimentos ou preferências no seu site, essas alterações devem ser coletadas e aplicadas imediatamente usando o [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). Se um cliente recusar a coleta de dados, toda a coleta de dados deverá ser interrompida imediatamente. Se um cliente recusar a personalização, então não deverá haver personalização na próxima página que visitar.

## Apêndice {#appendix}

As seções abaixo fornecem informações de referência adicionais sobre o [!UICONTROL Consentimentos e preferências] tipo de dados.

### Valores aceitos para `val` {#choice-values}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Title | Descrição |
| --- | --- | --- |
| `y` | Sim (opt-in) | O cliente aceitou o consentimento ou a preferência. Em outras palavras, eles **do** consentimento para a utilização dos seus dados, conforme indicado pelo consentimento ou preferência em causa. |
| `n` | Não (opt-out) | O cliente recusou o consentimento ou a preferência. Em outras palavras, eles **não** consentimento para a utilização dos seus dados, conforme indicado pelo consentimento ou preferência em causa. |
| `p` | Verificação pendente | O sistema ainda não recebeu um consentimento ou valor de preferência final. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até selecionarem um link em um email para verificar se forneceram o endereço de email correto, em que o consentimento seria atualizado para `y`.<br><br>Se esse consentimento ou preferência não usar um processo de verificação de dois conjuntos, a variável `p` pode ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, é possível definir automaticamente o valor como `p` na primeira página de um site, antes do cliente responder ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de consentimento ou preferência do cliente são desconhecidas. |
| `dy` | Padrão de Sim (aceitação) | O cliente não forneceu um valor de consentimento em si e é tratado como uma aceitação (&quot;Sim&quot;) por padrão. Em outras palavras, o consentimento é presumido até que o cliente indique o contrário.<br><br>Observe que, se as leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contêm valores padrão. |
| `dn` | Padrão de Não (opt out) | O cliente não forneceu um valor de consentimento por si só e é tratado como um opt out (&quot;Não&quot;) por padrão. Em outras palavras, presume-se que o cliente tenha negado o consentimento até que indique o contrário.<br><br>Observe que, se as leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contêm valores padrão. |
| `LI` | Interesse legítimo | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera o potencial dano que isso representa para o indivíduo. |
| `CT` | Contrato | A recolha de dados para o fim especificado é necessária para cumprir as obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para o fim especificado é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para o fim especificado é necessária para levar a cabo uma missão de interesse público ou no exercício da autoridade oficial. |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

### Total [!UICONTROL Consentimentos e preferências] schema {#full-schema}

Para exibir o esquema completo da variável [!UICONTROL Consentimentos e preferências] tipo de dados, consulte a [repositório XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).

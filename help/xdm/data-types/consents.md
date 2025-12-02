---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;consentimento;Consentimento;preferências;privacidadeOptOuts;marketingPreferences;optOutType;baseOfProcessing;consentimento;Consentimento
title: Tipo de dados de consentimentos e preferências
description: O tipo de dados Consentimento para privacidade, Personalization e Preferências de marketing tem como objetivo oferecer suporte à coleção de permissões e preferências do cliente geradas pelas Plataformas de gerenciamento de consentimento (CMPs) e outras fontes das operações de dados.
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '2305'
ht-degree: 1%

---

# [!UICONTROL Consents and Preferences] tipo de dados

O tipo de dados [!UICONTROL Consent for Privacy, Personalization and Marketing Preferences] (a seguir denominado &quot;[!UICONTROL Consents and Preferences] tipo de dados&quot;) é um tipo de dados [!DNL Experience Data Model] (XDM) que tem como objetivo oferecer suporte à coleta de permissões e preferências do cliente geradas pelas Plataformas de Gerenciamento de Consentimento (CMPs) e outras fontes de suas operações de dados.

Este documento aborda a estrutura e o uso pretendido dos campos fornecidos pelo tipo de dados [!UICONTROL Consents and Preferences].

## Pré-requisitos {#prerequisites}

Este documento requer uma compreensão funcional do XDM e o uso dos esquemas em [!DNL Experience Platform]. Revise a documentação a seguir antes de continuar:

* [Visão geral do sistema XDM](https://www.adobe.com/go/xdm-home-en)
* [Noções básicas sobre a composição do esquema](https://www.adobe.com/go/xdm-schema-best-practices-en)

## Estrutura do tipo de dados {#structure}

>[!IMPORTANT]
>
>O tipo de dados [!UICONTROL Consents and Preferences] foi desenvolvido para abranger uma variedade de casos de uso de gerenciamento de preferências e consentimento. Como resultado, este documento descreve o uso dos campos do tipo de dados em termos gerais e faz sugestões apenas sobre como você deve interpretar o uso desses campos. Consulte sua equipe jurídica de privacidade para alinhar a estrutura do tipo de dados com a forma como sua organização interpreta e apresenta essas opções de consentimento e preferência aos clientes.

O tipo de dados [!UICONTROL Consents and Preferences] fornece vários campos usados para capturar informações de **consentimento** e **preferência**.

Um consentimento é uma opção que permite que um cliente especifique como seus dados podem ser usados. A maioria dos consentimentos tem um aspecto legal, já que algumas jurisdições exigem a obtenção de permissão antes que os dados possam ser usados de uma determinada maneira, ou exigem que o cliente tenha uma opção para interromper esse uso (opt out) se o consentimento positivo não for necessário.

Uma preferência é uma opção que permite ao cliente especificar como diferentes aspectos de sua experiência com uma marca devem ser tratados. Eles se encaixam em duas categorias:

* **Preferências do Personalization**: preferências relacionadas a como a marca deve personalizar experiências entregues a um cliente.
* **Preferências de marketing**: preferências que especificam se uma marca pode contatar um cliente por meio de vários canais.

A captura de tela a seguir mostra como a estrutura do tipo de dados é representada na interface do usuário do Experience Platform:

![](../images/data-types/consents.png)

>[!TIP]
>
>Consulte o guia em [explorando recursos XDM](../ui/explore.md) para obter etapas sobre como pesquisar qualquer recurso XDM e inspecionar sua estrutura na interface do usuário do Experience Platform.

O JSON a seguir mostra um exemplo do tipo de dados que o tipo de dados [!UICONTROL Consents and Preferences] pode processar. As informações sobre o uso específico de cada um desses campos são fornecidas nas seções a seguir.

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
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
>* [Gerar dados de exemplo na interface](../ui/sample.md)
>* [Gerar dados de amostra na API](../api/sample-data.md)

## `consents` {#choices}

`consents` contém vários campos que descrevem os consentimentos e preferências de um cliente. Esses campos são descritos com mais detalhes nas subseções abaixo.

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
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

`collect` representa o consentimento do cliente para que seus dados sejam coletados.

```json
"collect": {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

{style="table-layout:auto"}

### `adID`

`adID` representa o consentimento do cliente para que uma ID de anunciante possa ser usada para vincular o cliente em aplicativos neste dispositivo.

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `idType` | O tipo de ID do anúncio, `IDFA` para a ID do Apple para anunciantes ou `GAID` para a ID do anunciante da Google, também conhecida como AAID (Android Advertiser ID). |
| `val` | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

{style="table-layout:auto"}

### `share`

`share` representa o consentimento do cliente para que os dados sejam compartilhados com (ou vendidos a) segundos ou terceiros.

```json
"share": {
  "val": "y"
}
```

| Propriedade | Descrição |
| --- | --- |
| `val` | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` captura as preferências do cliente com relação a quais maneiras seus dados podem ser usados para personalização. Os clientes podem recusar casos de uso de personalização específicos ou recusar totalmente a personalização.

>[!IMPORTANT]
>
>`personalize` não abrange casos de uso de marketing. Por exemplo, se um cliente optar por não ser personalizado para todos os canais, ele não deverá parar de receber comunicações por meio desses canais. Em vez disso, as mensagens que recebem devem ser genéricas e não baseadas em seus perfis.
>
>Pelo mesmo exemplo, se um cliente optar por não participar do marketing direto para todos os canais (por meio do `marketing`, explicado na [próxima seção](#marketing)), ele não deverá receber nenhuma mensagem, mesmo que a personalização seja permitida.

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `content` | Representa as preferências do cliente para conteúdo personalizado no site ou aplicativo. |
| `val` | A preferência de personalização fornecida pelo cliente para o caso de uso especificado. Nos casos em que não é necessário solicitar o consentimento do cliente, o valor desse campo deve indicar a base sobre a qual a personalização deve ocorrer. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` captura as preferências do cliente com relação às finalidades de marketing para as quais seus dados podem ser usados. Os clientes podem recusar casos de uso de marketing específicos ou recusar totalmente o marketing direto.

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
| `preferred` | Indica o canal preferido do cliente para receber comunicações. Consulte o [apêndice](#preferred-values) para ver os valores aceitos. |
| `any` | Representa as preferências do cliente para marketing direto como um todo. A preferência de consentimento fornecida neste campo é considerada a preferência &quot;padrão&quot; para qualquer canal de marketing, a menos que seja substituída por subcampos adicionais fornecidos em `marketing`. Se você planeja usar opções de consentimento mais granulares, é recomendável excluir esse campo.<br><br>Se o valor for definido como `n`, todas as configurações de personalização mais específicas deverão ser ignoradas. Se o valor for definido como `y`, todas as opções de personalização mais refinadas também deverão ser tratadas como `y`, a menos que explicitamente definidas como `n`. Se o valor não for definido, os valores de cada opção de personalização deverão ser honrados conforme especificado. |
| `email` | Indica se o cliente concorda em receber mensagens de email. |
| `push` | Indica se o cliente permite receber notificações por push. |
| `sms` | Indica se o cliente concorda em receber mensagens de texto. |
| `val` | A preferência fornecida pelo cliente para o caso de uso especificado. Nos casos em que não é necessário solicitar o consentimento do cliente, o valor deste campo deve indicar a base em que o caso de uso de marketing deve ocorrer. Consulte o [apêndice](#choice-values) para obter os valores e as definições aceitos. |
| `time` | Um carimbo de data e hora ISO 8601 que indica quando a preferência de marketing foi alterada, se aplicável. Observe que se o carimbo de data e hora de qualquer preferência individual for igual ao fornecido em `metadata`, esse campo não deverá ser definido para essa preferência. |
| `reason` | Quando um cliente recusa um caso de uso de marketing, esse campo de string representa o motivo pelo qual o cliente recusou. |

{style="table-layout:auto"}

### `metadata`

`metadata` captura metadados gerais sobre os consentimentos e preferências do cliente sempre que foram atualizados pela última vez.

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| Propriedade | Descrição |
| --- | --- |
| `time` | Um carimbo de data e hora ISO 8601 pela última vez que qualquer consentimento e preferência do cliente foi atualizado. Esse campo pode ser usado em vez de aplicar carimbos de data e hora a preferências individuais para reduzir a carga e a complexidade. Fornecer um valor `time` sob uma preferência individual substitui o carimbo de data/hora `metadata` dessa preferência específica. |

{style="table-layout:auto"}

## Assimilar dados usando o tipo de dados {#ingest}

Para usar o tipo de dados [!UICONTROL Consents and Preferences] para assimilar dados de consentimento de seus clientes, você deve criar um conjunto de dados com base em um esquema que contenha esse tipo de dados.

Consulte o tutorial sobre [criação de um esquema na interface](https://www.adobe.com/go/xdm-schema-editor-tutorial-en_br) para ver etapas sobre como atribuir tipos de dados a campos. Depois de criar um esquema contendo um campo com o tipo de dados [!UICONTROL Consents and Preferences], consulte a seção sobre [criação de um conjunto de dados](../../catalog/datasets/user-guide.md#create) no guia do usuário do conjunto de dados, seguindo as etapas para criar um conjunto de dados com um esquema existente.

>[!IMPORTANT]
>
>Para enviar dados de consentimento para [!DNL Real-Time Customer Profile], é necessário criar um esquema habilitado para [!DNL Profile] com base na classe [!DNL XDM Individual Profile] que contenha o tipo de dados [!UICONTROL Consents and Preferences]. O conjunto de dados criado com base nesse esquema também deve ser habilitado para [!DNL Profile]. Consulte os tutoriais vinculados acima para obter etapas específicas relacionadas aos requisitos de [!DNL Real-Time Customer Profile] para esquemas e conjuntos de dados.
>
>Além disso, você também deve garantir que suas políticas de mesclagem sejam configuradas para priorizar os conjuntos de dados que contêm os dados de consentimento e preferência mais recentes, para que os perfis do cliente sejam atualizados corretamente. Consulte a visão geral em [políticas de mesclagem](../../rtcdp/profile/merge-policies.md) para obter mais informações.

## Lidar com alterações de consentimento e preferência

Quando um cliente altera os consentimentos ou preferências no site, essas alterações devem ser coletadas e imediatamente aplicadas, definindo o consentimento na biblioteca de coleta de dados usada. Se um cliente recusar a coleta de dados, toda a coleta de dados deverá ser interrompida imediatamente. Se um cliente optar por não ser personalizado, não deverá haver personalização na próxima página que visitar. Consulte [`setConsent`](/help/collection/js/commands/setconsent.md) usando a biblioteca JavaScript ou a ação [[!UICONTROL Set consent]](/help/tags/extensions/client/web-sdk/actions/set-consent.md) usando a extensão de tag.

## Apêndice {#appendix}

As seções abaixo fornecem informações de referência adicionais sobre o tipo de dados [!UICONTROL Consents and Preferences].

### Valores aceitos para `val` {#choice-values}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Título | Descrição |
| --- | --- | --- |
| `y` | Sim (aceitação) | O cliente optou pelo consentimento ou preferência. Em outras palavras, eles **consentem** o uso de seus dados conforme indicado pelo consentimento ou preferência em questão. |
| `n` | Não (recusar) | O cliente recusou o consentimento ou a preferência. Em outras palavras, **não** consente com o uso de seus dados conforme indicado pelo consentimento ou preferência em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu um consentimento final ou valor de preferência. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que ele selecione um link em um email para verificar se forneceu o endereço de email correto. Nesse momento, o consentimento será atualizado para `y`.<br><br>Se este consentimento ou preferência não utilizar um processo de verificação de dois conjuntos, a opção `p` poderá ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor como `p` na primeira página de um site, antes que o cliente tenha respondido ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido).<br><br> Embora este valor possa ser assimilado no [!DNL Profile] usando outros mecanismos, como a assimilação de streaming, **não há suporte** para a coleta de dados ou de consentimento em [!DNL Edge Network]. Embora o valor `p` não possa ser enviado explicitamente, o enfileiramento de eventos ainda será manipulado por [[!DNL Web SDK]](../../landing/governance-privacy-security/consent/sdk.md) e o evento será despachado para [!DNL Edge Network] assim que o consentimento do usuário final for explicitamente `in`. |
| `u` | Desconhecido | As informações de consentimento ou preferência do cliente são desconhecidas. |
| `dy` | Padrão de Sim (aceitação) | O cliente não forneceu um valor de consentimento e é tratado como uma aceitação (&quot;Sim&quot;) por padrão. Em outras palavras, o consentimento é presumido até que o cliente indique o contrário.<br><br>Observe que, se leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contenham valores padrão. |
| `dn` | Padrão de Não (recusar) | O cliente não forneceu um valor de consentimento e é tratado como uma opção de não participação (&quot;Não&quot;) por padrão. Em outras palavras, presume-se que o cliente tenha negado o consentimento até que indique o contrário.<br><br>Observe que, se leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contenham valores padrão. |
| `LI` | Interesse legítimo | O interesse comercial legítimo de coletar e processar esses dados para a finalidade especificada supera o dano potencial que eles representam para o indivíduo. |
| `CT` | Contrato | A coleta de dados para a finalidade especificada é necessária para cumprir obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A coleta de dados para a finalidade especificada é necessária para atender às obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para os fins especificados é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para os fins especificados é necessária para executar uma missão de interesse público ou para o exercício da autoridade pública. |

{style="table-layout:auto"}

### Valores aceitos para `preferred` {#preferred-values}

A tabela a seguir descreve os valores aceitos para `preferred`. Os valores de `preferred` indicam o canal de preferência do cliente para receber comunicações que informem sobre a coleta de dados, as políticas de privacidade e as opções de personalização.

| Valor | Descrição |
| --- | --- |
| `email` | Esta preferência indica o consentimento do cliente para receber mensagens por email. |
| `push` | Esta preferência indica o consentimento do cliente para receber notificações por push. São mensagens ou alertas enviados diretamente ao dispositivo, geralmente um aplicativo móvel. |
| `inApp` | Esta preferência indica o consentimento do cliente para receber mensagens no aplicativo. Essas mensagens são entregues em um aplicativo móvel ou Web e fornecem informações enquanto o usuário está ativamente envolvido no aplicativo. |
| `sms` | Esta preferência indica o consentimento do cliente para receber mensagens via SMS (Short Message Service). São mensagens de texto enviadas para o celular deles. |
| `phone` | Esta preferência indica o consentimento do cliente para receber comunicações por meio de interações de chamada telefônica. |
| `phyMail` | Esta preferência indica o consentimento do cliente para receber material por correio físico. |
| `inVehicle` | Esta preferência indica o consentimento do cliente para receber notificações enquanto estiver em seu veículo. Estas mensagens podem ser entregues através de sistemas de informação do veículo ou outros canais de comunicação no veículo. |
| `inHome` | Esta preferência indica o consentimento do cliente para receber mensagens em casa. Essas mensagens podem ser entregues por meio de dispositivos residenciais inteligentes ou outros canais de comunicação baseados em residências. |
| `iot` | Esta preferência denota o consentimento do cliente para receber mensagens relacionadas à IoT (Internet das Coisas). Essas mensagens podem ser entregues por meio de dispositivos e sistemas conectados em seu ambiente. |
| `social` | Esta preferência indica o consentimento do cliente para receber comunicações por meio de plataformas de redes sociais. |
| `other` | Essa preferência engloba canais que não se encaixam em categorias padrão. Representa canais de comunicação alternativos ou especializados que podem ser específicos de uma determinada empresa ou indústria. |
| `none` | Essa preferência indica que o cliente não tem um canal de comunicação preferido. |
| `unknown` | Esta preferência significa que o canal de comunicação preferido do cliente não é conhecido ou não foi especificado. Isso pode ocorrer se o cliente não tiver fornecido consentimento explícito ou informações de preferência. |

{style="table-layout:auto"}

### Esquema [!UICONTROL Consents and Preferences] completo {#full-schema}

Para exibir o esquema completo do tipo de dados [!UICONTROL Consents and Preferences], consulte o [repositório XDM oficial](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).

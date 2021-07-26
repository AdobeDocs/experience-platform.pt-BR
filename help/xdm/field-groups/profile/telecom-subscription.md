---
keywords: Experience Platform, home, tópicos populares, schema, esquema, XDM, perfil individual, campos, esquemas, esquemas, telecom, subscrição, telecomunicações, design de esquema, grupo de campos, grupo de campos;
solution: Experience Platform
title: Grupo de campos do esquema de assinatura Telecom
topic-legacy: overview
description: Este documento fornece uma visão geral do grupo de campos Telecom Subscription schema .
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 6%

---

# [!UICONTROL Grupo ] de campos Telecom Subscriptionschema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento em [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL A ] Subscrição Telecom é um grupo de campos de esquema padrão para a  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe que descreve um plano de assinatura de telecom do cliente, incluindo preços, pacotes e subscrições individuais de produtos.

O grupo de campos fornece um único campo do tipo de objeto, `telecomSubscription`, cujas propriedades são descritas abaixo.

![Estrutura de assinatura Telecom](../../images/field-groups/telecom-subscription/structure.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `internetSubscription` | Matriz de objetos | Descreve detalhes do plano de assinatura da Internet, como limite de dados, tipo de conexão e detalhes de velocidade. Consulte a seção [abaixo](#internetSubscription) para obter mais informações. |
| `landlineSubscription` | Matriz de objetos | Descreve detalhes do plano de assinatura da linha de terra, incluindo recursos selecionados, minutos e planos de discagem. Consulte a seção [abaixo](#landlineSubscription) para obter mais informações. |
| `mediaSubscription` | Matriz de objetos | Descreve detalhes do plano de assinatura de mídia, incluindo o número de canais e os serviços de transmissão incluídos. Consulte a seção [abaixo](#mediaSubscription) para obter mais informações. |
| `mobileSubscription` | Matriz de objetos | Descreve detalhes do plano de assinatura móvel, incluindo o número de linhas, taxas de dados, custo e muito mais. Consulte a seção [abaixo](#mobileSubscription) para obter mais informações. |
| `primarySubscriber` | [[!UICONTROL Pessoa]](../../data-types/person.md) | Descreve o proprietário da subscrição. |
| `bundleName` | String | Captura o nome de qualquer tipo de pacote de assinatura em que o cliente está inscrito, como `Internet + Media`. |
| `primaryPartyID` | String | Um identificador da pessoa principal responsável pela assinatura, que normalmente pode ser o número de telefone do dispositivo. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` O é fornecido com uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Subscrição Telecom]](../../data-types/telecom-subscription.md) | Descreve detalhes gerais sobre a assinatura, incluindo duração da assinatura, tarifas, status e muito mais. Descreve detalhes gerais sobre a assinatura, incluindo duração da assinatura, tarifas, status e muito mais. |
| `connectionType` | String | O tipo de conexão da assinatura. |
| `dataCap` | Número inteiro | O limite de dados da conta, em megabytes (MB). |
| `downloadSpeed` | Número inteiro | A velocidade máxima de download disponível para a assinatura, em megabytes (MB). |
| `selfSetup` | Booleano | Indica se um cliente está qualificado para a configuração da Internet sem uma visita de um técnico. |
| `uploadSpeed` | Número inteiro | A velocidade máxima de upload disponível para a assinatura, em megabytes (MB). |

{style=&quot;table-layout:auto&quot;}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` O é fornecido com uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/telecom-subscription.md) | O número de telefone atribuído a esta assinatura. |
| `subscriptionDetails` | [[!UICONTROL Subscrição Telecom]](../../data-types/telecom-subscription.md) | Descreve detalhes gerais sobre a assinatura, incluindo duração da assinatura, tarifas, status e muito mais. |
| `callBlocking` | Booleano | Indica se os recursos de assinatura fixa incluem bloqueio de chamada. |
| `callForwarding` | Booleano | Indica se os recursos de assinatura fixa incluem o encaminhamento de chamadas. |
| `callWaiting` | Booleano | Indica se os recursos de assinatura fixa incluem espera de chamada. |
| `callerID` | Booleano | Indica se os recursos de assinatura fixa incluem a ID do chamador. |
| `internationalCalling` | Booleano | Indica se os recursos de assinatura fixa incluem chamadas internacionais. |
| `minutes` | Número inteiro | O número de minutos mensais disponíveis na assinatura. |
| `threeWayCalling` | Booleano | Indica se os recursos de assinatura fixa incluem uma chamada de três vias. |
| `unlimitedDomesticLongDistance` | Booleano | Indica se os recursos de assinatura fixa incluem chamada doméstica de longa distância ilimitada. |
| `unlimitedLocalCalling` | Booleano | Indica se os recursos de assinatura fixa incluem chamada local ilimitada. |
| `voicemail` | Booleano | Indica se os recursos de assinatura fixa incluem caixa postal. |

{style=&quot;table-layout:auto&quot;}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` O é fornecido com uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `streamingServices` | Matriz de objetos | Uma lista de todos os serviços de transmissão incluídos na assinatura. Cada item de matriz inclui as seguintes propriedades: <ul><li>`promotionLength`: A duração da promoção, em meses, se o serviço de transmissão foi adicionado como parte de uma promoção.</li><li>`promotionalAddition`: Indica se o serviço de transmissão foi adicionado como parte de uma promoção.</li><li>`serviceName`: O nome do serviço de transmissão.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Subscrição Telecom]](../../data-types/telecom-subscription.md) | Descreve detalhes gerais sobre a assinatura, incluindo duração da assinatura, tarifas, status e muito mais. |
| `channels` | Número inteiro | O número de canais incluídos na assinatura de mídia. |

{style=&quot;table-layout:auto&quot;}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` O é fornecido com uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/telecom-subscription.md) | O número de telefone atribuído a esta assinatura. |
| `subscriptionDetails` | [[!UICONTROL Subscrição Telecom]](../../data-types/telecom-subscription.md) | Descreve detalhes gerais sobre a assinatura, incluindo duração da assinatura, tarifas, status e muito mais. |
| `earlyUpgradeEnrollment` | Booleano | Indica se o cliente opta por atualizações antecipadas. |
| `planLevel` | String | O nome do plano móvel atribuído a esta assinatura. |
| `portedNumber` | Booleano | Indica se o cliente portas o número de outra operadora. |

{style=&quot;table-layout:auto&quot;}


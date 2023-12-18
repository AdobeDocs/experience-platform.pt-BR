---
keywords: Experience Platform;página inicial;tópicos populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;telecom;assinatura;telecomunicações;Design de esquema;grupo de campos;Grupo de campos;
solution: Experience Platform
title: Grupo de Campos de Esquema de Assinatura de Telecom
description: Saiba mais sobre o grupo de campos de esquema Assinatura de telecomunicação.
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 6%

---

# [!UICONTROL Assinatura de serviço de telecomunicação] grupo de campos de esquema

>[!NOTE]
>
>Os nomes de vários grupos de campos de esquema foram alterados. Consulte o documento sobre [atualizações do nome do grupo de campos](../name-updates.md) para obter mais informações.

[!UICONTROL Assinatura de serviço de telecomunicação] é um grupo de campos de esquema padrão para o [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) que descreve o plano de assinatura de telecomunicações de um cliente, incluindo preços, pacotes e assinaturas de produtos individuais.

O grupo de campos fornece um único campo do tipo objeto, `telecomSubscription`, cujas propriedades estão descritas abaixo.

![Estrutura de assinatura de telecomunicação](../../images/field-groups/telecom-subscription/structure.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `internetSubscription` | Matriz de objetos | Descreve os detalhes do plano de assinatura da Internet, como limite de dados, tipo de conexão e detalhes de velocidade. Consulte a [seção abaixo](#internetSubscription) para obter mais informações. |
| `landlineSubscription` | Matriz de objetos | Descreve os detalhes do plano de assinatura de telefone fixo, incluindo recursos, minutos e planos de discagem selecionados. Consulte a [seção abaixo](#landlineSubscription) para obter mais informações. |
| `mediaSubscription` | Matriz de objetos | Descreve os detalhes do plano de assinatura de mídia, incluindo o número de canais e os serviços de streaming incluídos. Consulte a [seção abaixo](#mediaSubscription) para obter mais informações. |
| `mobileSubscription` | Matriz de objetos | Descreve os detalhes do plano de assinatura móvel, incluindo o número de linhas, taxas de dados, custo e muito mais. Consulte a [seção abaixo](#mobileSubscription) para obter mais informações. |
| `primarySubscriber` | [[!UICONTROL Pessoa]](../../data-types/person.md) | Descreve o proprietário da assinatura. |
| `bundleName` | String | Registra o nome de qualquer tipo de pacote de assinatura no qual o cliente está inscrito, como `Internet + Media`. |
| `primaryPartyID` | String | Um identificador da pessoa responsável pela assinatura, que normalmente pode ser o número de telefone do dispositivo. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Assinatura de serviço de telecomunicação]](../../data-types/telecom-subscription.md) | Descreve os detalhes gerais sobre a assinatura, incluindo duração da assinatura, taxas, status e muito mais. Descreve os detalhes gerais sobre a assinatura, incluindo duração da assinatura, taxas, status e muito mais. |
| `connectionType` | String | O tipo de conexão da assinatura. |
| `dataCap` | Número inteiro | O limite de dados da conta, em megabytes (MB). |
| `downloadSpeed` | Número inteiro | A velocidade máxima de download disponível para a assinatura, em megabytes (MB). |
| `selfSetup` | Booleano | Indica se um cliente está qualificado para configuração de Internet sem a visita de um técnico. |
| `uploadSpeed` | Número inteiro | A velocidade máxima de upload disponível para a assinatura, em megabytes (MB). |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/telecom-subscription.md) | O número de telefone atribuído a esta assinatura. |
| `subscriptionDetails` | [[!UICONTROL Assinatura de serviço de telecomunicação]](../../data-types/telecom-subscription.md) | Descreve os detalhes gerais sobre a assinatura, incluindo duração da assinatura, taxas, status e muito mais. |
| `callBlocking` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem bloqueio de chamadas. |
| `callForwarding` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem encaminhamento de chamadas. |
| `callWaiting` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem chamada em espera. |
| `callerID` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem a ID do chamador. |
| `internationalCalling` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem chamadas internacionais. |
| `minutes` | Número inteiro | O número de minutos mensais disponíveis na assinatura. |
| `threeWayCalling` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem chamadas de três vias. |
| `unlimitedDomesticLongDistance` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem chamadas domésticas de longa distância ilimitadas. |
| `unlimitedLocalCalling` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem chamadas locais ilimitadas. |
| `voicemail` | Booleano | Indica se os recursos de assinatura de telefone fixo incluem correio de voz. |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `streamingServices` | Matriz de objetos | Uma lista de todos os serviços de streaming incluídos na assinatura. Cada item da matriz inclui as seguintes propriedades: <ul><li>`promotionLength`: a duração da promoção, em meses, se o serviço de streaming foi adicionado como parte de uma promoção.</li><li>`promotionalAddition`: indica se o serviço de streaming foi adicionado como parte de uma promoção.</li><li>`serviceName`: o nome do serviço de streaming.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Assinatura de serviço de telecomunicação]](../../data-types/telecom-subscription.md) | Descreve os detalhes gerais sobre a assinatura, incluindo duração da assinatura, taxas, status e muito mais. |
| `channels` | Número inteiro | O número de canais incluídos na assinatura de mídia. |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Número de telefone]](../../data-types/telecom-subscription.md) | O número de telefone atribuído a esta assinatura. |
| `subscriptionDetails` | [[!UICONTROL Assinatura de serviço de telecomunicação]](../../data-types/telecom-subscription.md) | Descreve os detalhes gerais sobre a assinatura, incluindo duração da assinatura, taxas, status e muito mais. |
| `earlyUpgradeEnrollment` | Booleano | Indica se o cliente opta por atualizações antecipadas. |
| `planLevel` | String | O nome do plano móvel atribuído a esta assinatura. |
| `portedNumber` | Booleano | Indica se o cliente transfere seu número de outra operadora. |

{style="table-layout:auto"}

---
title: Exemplo de configurações
description: Saiba mais sobre configurações de exemplo com o usando a ferramenta de simulação de gráfico.
badge: Beta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 10%

---

# Exemplo de configurações de gráfico

>[!AVAILABILITY]
>
>As regras de vinculação do gráfico de identidade estão na versão beta. Entre em contato com a equipe de conta do Adobe para obter informações sobre os critérios de participação. O recurso e a documentação estão sujeitos a alterações.

>[!NOTE]
>
>* &quot;CRMID&quot; e &quot;loginID&quot; são namespaces personalizados. Neste documento, &quot;CRMID&quot; é um identificador de pessoa e &quot;loginID&quot; é um identificador de logon associado a uma determinada pessoa.
>* Para simular os cenários de gráficos de exemplo descritos neste documento, primeiro você deve criar dois namespaces personalizados, um com o símbolo de identidade &quot;CRMID&quot; e outro com o símbolo de identidade &quot;loginID&quot;. Os símbolos de identidade diferenciam maiúsculas de minúsculas.

Este documento descreve exemplos de configurações de gráfico de cenários comuns que você pode encontrar ao trabalhar com dados de identidade.

## Somente CRMID

Este é um exemplo de um cenário de implementação simples em que os eventos online (CRMID e ECID) são assimilados e os eventos offline (registros de perfil) são armazenados somente no CRMID.

**Implementação:**

| Namespaces usados | Método de coleta de comportamento da Web |
| --- | --- |
| CRMID, ECID | Web SDK |

**Eventos:**

Você pode criar esse cenário na simulação de gráfico copiando os seguintes eventos no modo de texto:

* CRMID: Tom, ECID: 111

**Configuração do algoritmo:**

Você pode criar esse cenário na simulação de gráfico definindo a seguinte configuração para a configuração do algoritmo:

| Prioridade | Nome de exibição | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sim |
| 2 | ECID | COOKIE | Não |

**Seleção de identidade principal para o Perfil de Cliente em Tempo Real:**

No contexto dessa configuração, a identidade primária será definida da seguinte maneira:

| Status de autenticação | Namespace(s) em eventos | Identidade principal |
| --- | --- | --- |
| Autenticado | CRMID, ECID | CRMID |
| Não autenticado | ECID | ECID |

>[!BEGINTABS]

>[!TAB Cenário ideal de gráficos em uma única pessoa]

Veja a seguir um exemplo de um gráfico ideal para uma única pessoa, em que a CRMID é exclusiva e recebe a maior prioridade.

![Um exemplo simulado de um gráfico ideal para uma única pessoa, em que a CRMID é exclusiva e recebe a maior prioridade.](../images/graph-examples/crmid_only_single.png)

>[!TAB cenário de gráficos entre várias pessoas]

Veja a seguir um exemplo de gráfico com várias pessoas. Este exemplo exibe um cenário de &quot;dispositivo compartilhado&quot;, em que há dois CRMIDs e o que tem o link estabelecido mais antigo é removido.

![Um exemplo simulado de um gráfico de várias pessoas. Este exemplo exibe um cenário de dispositivo compartilhado, em que há dois CRMIDs e o link estabelecido mais antigo é removido.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## CRMID com email com hash

Nesse cenário, um CRMID é assimilado e representa os dados online (evento de experiência) e offline (registro de perfil). Esse cenário também envolve a assimilação de um email com hash, que representa outro namespace enviado no conjunto de dados de registro do CRM junto com o CRMID.

**Implementação:**

| Namespaces usados | Método de coleta de comportamento da Web |
| --- | --- |
| CRMID, Email_LC_SHA256, ECID | Web SDK |

**Eventos:**

Você pode criar esse cenário na simulação de gráfico copiando os seguintes eventos no modo de texto:

* CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRMID: Tom, ECID: 111
* CRMID: Summer, Email_LC_SHA256: verão<span>@acme.com
* CRMID: Summer, ECID: 222

**Configuração do algoritmo:**

Você pode criar esse cenário na simulação de gráfico definindo a seguinte configuração para a configuração do algoritmo:

| Prioridade | Nome de exibição | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sim |
| 2 | Emails (SHA256, em letras minúsculas) | Email | Não |
| 3 | ECID | COOKIE | Não |

**Seleção de identidade principal para o Perfil:**

No contexto dessa configuração, a identidade primária será definida da seguinte maneira:

| Status de autenticação | Namespace(s) em eventos | Identidade principal |
| --- | --- | --- |
| Autenticado | CRMID, ECID | CRMID |
| Não autenticado | ECID | ECID |

>[!BEGINTABS]

>[!TAB Cenário ideal de gráficos em uma única pessoa]

![Neste exemplo, dois gráficos separados são gerados, cada um representando uma entidade de uma única pessoa.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB gráfico multipessoa: dispositivo compartilhado]

![Neste exemplo, o gráfico simulado exibe um cenário de &quot;dispositivo compartilhado&quot; porque Tom e Summer estão associados à mesma ECID.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB gráfico de várias pessoas: email não exclusivo]

![Este cenário é semelhante a um cenário de &quot;dispositivo compartilhado&quot;. No entanto, em vez de as entidades de pessoa compartilharem ECID, elas são associadas à mesma conta de email.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID com email com hash, telefone com hash, GAID e IDFA

Esse cenário é semelhante ao anterior. No entanto, nesse cenário, emails com hash e telefones estão sendo marcados como identidades a serem utilizadas na correspondência do segmento.

**Implementação:**

| Namespaces usados | Método de coleta de comportamento da Web |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | Web SDK |

**Eventos:**

Você pode criar esse cenário na simulação de gráfico copiando os seguintes eventos no modo de texto:

* CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: Tom, ECID: 111
* CRMID: Tom, ECID: 222, IDFA: A-A-A
* CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Summer, ECID: 333
* CRMID: Summer, ECID: 444, GAID:B-B-B

**Configuração do algoritmo:**

Você pode criar esse cenário na simulação de gráfico definindo a seguinte configuração para a configuração do algoritmo:

| Prioridade | Nome de exibição | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Sim |
| 2 | Emails (SHA256, em letras minúsculas) | Email | Não |
| 3 | Telefone (SHA256) | Telefone | Não |
| 4 | ID de anúncio do Google (GAID) | DISPOSITIVO | Não |
| 5 | Apple IDFA (ID para Apple) | DISPOSITIVO | Não |
| 6 | ECID | COOKIE | Não |

**Seleção de identidade principal para o Perfil:**

No contexto dessa configuração, a identidade primária será definida da seguinte maneira:

| Status de autenticação | Namespace(s) em eventos | Identidade principal |
| --- | --- | --- |
| Autenticado | CRMID, IDFA, ECID | CRMID |
| Autenticado | CRMID, GAID, ECID | CRMID |
| Autenticado | CRMID, ECID | CRMID |
| Não autenticado | GAID, ECID | GAID |
| Não autenticado | IDFA, ECID | IDFA |
| Não autenticado | ECID | ECID |

>[!BEGINTABS]

>[!TAB Cenário ideal de gráficos em uma única pessoa]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->

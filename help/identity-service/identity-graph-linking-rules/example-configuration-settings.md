---
title: Exemplo de configurações
description: Saiba mais sobre configurações de exemplo com o usando a ferramenta de simulação de gráfico.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 22%

---

# Exemplo de configurações de gráfico

>[!NOTE]
>
>&quot;ID do CRM&quot; é um namespace personalizado. Portanto, os exemplos abaixo exigem que você crie um namespace personalizado com um nome para exibição e um símbolo de identidade de &quot;ID do CRM&quot;.

Os seguintes exemplos de seção de cenários de gráficos que você pode encontrar com a Simulação de gráfico.

## Somente ID do CRM

Eventos:

* ID do CRM: Tom, ECID: 111

Configuração do algoritmo:

| Prioridade | Nome de exibição | Símbolo de identidade | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID do CRM | ID do CRM | CROSS_DEVICE | Sim |
| 2 | ECID | ECID | COOKIE | NÃO |

+++Selecione para exibir o gráfico simulado

+++

## ID do CRM com email com hash

Nesse cenário, uma ID do CRM é assimilada e representa os dados online (evento de experiência) e offline (registro de perfil). Esse cenário também envolve a assimilação de um email com hash, que representa outro namespace enviado no conjunto de dados do registro do CRM junto com a ID do CRM.

Eventos:

* ID do CRM: Tom, Email_LC_SHA256: tom<span>@acme.com
* ID do CRM: Tom, ECID: 111
* ID do CRM: Summer, Email_LC_SHA256: summer<span>@acme.com
* ID do CRM: Verão, ECID: 222

Configuração do algoritmo:

| Prioridade | Nome de exibição | Símbolo de identidade | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID do CRM | ID do CRM | CROSS_DEVICE | Sim |
| 2 | Emails (SHA256, em letras minúsculas) | Email_LC_SHA256 | Email | NÃO |
| 3 | ECID | ECID | COOKIE | NÃO |

+++Selecione para exibir o gráfico simulado

+++

## ID do CRM com email com hash, telefone com hash, GAID e IDFA

Eventos:

* ID do CRM: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* ID do CRM: Tom, ECID: 111
* ID do CRM: Tom, ECID: 222, IDFA: A-A-A
* ID do CRM: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* ID do CRM: Summer, ECID: 333
* ID do CRM: Verão, ECID: 444, GAID:B-B-B

Configuração do algoritmo:

| Prioridade | Nome de exibição | Símbolo de identidade | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID do CRM | ID do CRM | CROSS_DEVICE | Sim |
| 2 | Emails (SHA256, em letras minúsculas) | Email_LC_SHA256 | Email | NÃO |
| 3 | Telefone (SHA256) | Phone_SHA256 | Telefone | NÃO |
| 4 | ID de anúncio do Google (GAID) | GAID | DISPOSITIVO | NÃO |
| 5 | Apple IDFA (ID para Apple) | IDFA | DISPOSITIVO | NÃO |
| 6 | ECID | ECID | COOKIE | NÃO |

+++Selecione para exibir o gráfico simulado

+++
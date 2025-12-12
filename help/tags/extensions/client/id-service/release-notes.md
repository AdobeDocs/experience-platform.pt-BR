---
title: Notas de versão da Extensão do Serviço de identidade da Adobe Experience Cloud
description: As notas de versão mais recentes da extensão de tag do Serviço de identidade da Adobe Experience Cloud na Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 76%

---

# Notas de versão da extensão do Serviço de identidade da Adobe Experience Cloud

Este documento aborda as notas de versão da extensão de tag do Adobe Experience Cloud Identity Service. Para obter as notas de versão do Experience Cloud Identity Service, consulte a [documentação do Identity Service](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=pt-BR).

## 17 de outubro de 2022

### Extensão da Experience Cloud ID 5.5.0

* A extensão agora dá suporte à versão 5.5.0 do [Cliente JS do Visitante](https://github.com/Adobe-Marketing-Cloud/id-service). Consulte as [notas de versão do visitante](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0) para obter atualizações específicas.

## 9 de março de 2022

### Extensão da Experience Cloud ID 5.4.0

* Esta versão contém o Visitante 5.4.0 mais recente, com as seguintes atualizações:

   * Capacidade de configurar a duração do cookie `s_ecid` usando a configuração cookieLifetime
   * Atualização para um problema do navegador Firefox que ocorre quando uma página é carregada em um iFrame secundário

## 10 de outubro de 2021

### Extensão da Experience Cloud ID 5.3.1

* Esta versão contém o Visitante 5.3.0 mais recente, com as seguintes novas atualizações:

   * Algoritmo atualizado para gerar o ECID local
   * Última aceitação com os sinalizadores `Secure` e `SameSite` para o cookie de privacidade
   * Correção para um problema do navegador Firefox quando uma página é carregada em um iFrame secundário

## 12 de janeiro de 2021

### Extensão da Experience Cloud ID 5.2.0

* A atualização para o patch VisitorJS 5.2.0 com uma correção para ECID DataElement não podia ser atualizada ao receber consentimento.

## 3 de novembro de 2020

### Extensão da Experience Cloud ID 5.2.1

* Este patch contém uma correção para gravar cookies de um iFrame com o atributo `SameSite=None` no navegador Google Chrome.

## 27 de outubro de 2020

### Extensão da Experience Cloud ID 5.1.0

* Adicionar configuração de `sameSiteCookie` para especificar o atributo `SameSite` do cookie `AMCV`. Essa configuração aceita os seguintes valores para o atributo `SameSite`:

   * `Strict`
   * `Lax`
   * `None`

Detalhes desses valores de atributo estão em [web.dev](https://web.dev/samesite-cookies-explained/) e [chromium](https://www.chromium.org/updates/same-site)


## 13 de agosto de 2020

### Extensão da Experience Cloud ID 5.0.1

* Atualização para o patch VisitorJS 5.0.1 com uma correção para adicionar o sinalizador d_cf quando a string de consentimento do IAB foi alterada.

## 15 de junho de 2020

### Extensão da Experience Cloud ID 5.0.0

* Adição de suporte para `IAB TCF` – Estrutura de transparência e consentimento – `Version 2.0`.

## 13 de abril de 2020

### Extensão do Experience Cloud ID 4.6.0

* Sinalizador ativado `loadSSL` por padrão. Todas as chamadas para o Serviço de identidade serão ativadas `https` por padrão. Os clientes podem defini-lo como falso se quiserem chamar os Serviços de identidade em http a partir de suas páginas não ssl.
* Atualização da função usada para detectar a versão do Internet Explorer (IE), para corrigir um problema relatado pelo ESLint.
* Correção de erro para um problema de desempenho no Internet Explorer (IE) 11 quando a ECID recebe a pré-aprovação do opt-in e é atualizada posteriormente.

## 22 de janeiro de 2020

### Extensão do Experience Cloud ID 4.5.2

* Atualização do visitor.js para 4.5.2
* O Visitante 4.5.1 inclui uma correção de erro para o plug-in IAB para Optin
* Atualização do `setCustomerIDs` método para rejeitar IDs vazias enviadas.

## 7 de janeiro de 2020

### Extensão do Experience Cloud ID 4.4.2

* Atualização do visitor.js para 4.4.2
* Melhorias no `getVisitorValues` método para obter valores mais rapidamente.


## 19 de setembro de 2019

### Extensão do Experience Cloud ID 4.4.1

* Atualização do visitor.js para 4.4.1
* Correção de um erro para obter a Entrada de pré-aprovações de inclusão
* VIDEO_ANALYTICS renomeado para MEDIA_ANALYTICS em preOptInApprovals

  ![](../../../images/ecid-media-analytics.png)

## 17 de julho de 2019

### Extensão do Experience Cloud ID 4.4.0

* Atualização do visitor.js para 4.4.0
* Suporte para hashing SHA256 adicionado para setCustomerIDs

  ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 de maio de 2019

### Extensão do Experience Cloud ID 4.3.1

* Atualização do visitor.js para 4.3
* Adição do tipo de elemento de dados para ECID como parte da extensão de tag

  ![](../../../images/ecid-data-element.png)

## 9 de abril de 2019

### Extensão do Experience Cloud ID 4.2.0

* Atualização do visitor.js para a versão 4.2, que inclui suporte para o plug-in do Audience Manager IAB TCF.

## 25 de fevereiro de 2019

### Extensão do Experience Cloud ID 4.1.0

* Atualização de visitor.js para 4.1, que atualizou publishDestinations por nova alteração da API. Com essa atualização, as informações do referenciador da página podem ser expostas durante a sincronização de ID, se desejado.

## 15 de fevereiro de 2019

### Extensão do Experience Cloud ID 4.0.0

* Atualização do visitor.js para 4.0
* Adicionadas opções de configuração para o novo objeto Aceitar integrado. Configurações do aceitação podem ser usadas para suprimir chamadas de cookie e de sinais feitas pelas soluções da Adobe para melhor suportar regulamentos, como o RGPD

  ![](../../../images/ext-mcid-opt-in.png)

## 20 de março de 2018

### Extensão do Experience Cloud ID 3.1.0

* Atualização do visitor.js para 3.1
* Adiciona duas propriedades de configuração: `resetBeforeVersion` e `serverState`.

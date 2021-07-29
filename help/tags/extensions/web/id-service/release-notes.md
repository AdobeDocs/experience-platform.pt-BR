---
title: Notas de versão da Extensão do Adobe Experience Cloud Identity Service
description: As notas de versão mais recentes para a extensão de tag do Adobe Experience Cloud Identity Service no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 83%

---

# Notas de versão da extensão do Adobe Experience Cloud Identity Service

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Para obter as notas de versão sobre o próprio Experience Cloud Identity Service e não apenas sobre a extensão da tag do Adobe Experience Platform, consulte: [https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=pt-BR)

## 3 de novembro de 2020

### Extensão da Experience Cloud ID 5.2.1

#### **Recursos**

* Este patch contém uma correção para gravar cookies de um iFrame com o atributo `SameSite=None` no navegador Google Chrome.

## 12 de janeiro de 2021

### Extensão da Experience Cloud ID 5.2.0

#### **Recursos**

* A atualização para o patch VisitorJS 5.2.0 com uma correção para ECID DataElement não podia ser atualizada ao receber consentimento.

## 27 de outubro de 2020

### Extensão da Experience Cloud ID 5.1.0

#### **Recursos**

* Adicionar configuração de `sameSiteCookie` para especificar o atributo `SameSite` do cookie `AMCV`. Essa configuração aceita os seguintes valores para o atributo `SameSite`:

   * `Strict`
   * `Lax`
   * `None`

Detalhes desses valores de atributo estão em [web.dev](https://web.dev/samesite-cookies-explained/) e [chromium](https://www.chromium.org/updates/same-site)


## 13 de agosto de 2020

### Extensão da Experience Cloud ID 5.0.1

#### **Recursos**

* Atualização para o patch VisitorJS 5.0.1 com uma correção para adicionar o sinalizador d_cf quando a string de consentimento do IAB foi alterada.

## 15 de junho de 2020

### Extensão da Experience Cloud ID 5.0.0

#### **Recursos**

* Adição de suporte para `IAB TCF` – Estrutura de transparência e consentimento – `Version 2.0`.

## 13 de abril de 2020

### Extensão do Experience Cloud ID 4.6.0

#### **Recursos**

* Sinalizador ativado `loadSSL` por padrão. Todas as chamadas para o Serviço de identidade serão ativadas `https` por padrão. Os clientes podem defini-lo como falso se quiserem chamar os Serviços de identidade em http a partir de suas páginas não ssl.
* Atualização da função usada para detectar a versão do Internet Explorer (IE), para corrigir um problema relatado pelo ESLint.
* Correção de bug para um problema de desempenho no Internet Explorer (IE) 11 quando a ECID recebe a pré-aprovação do opt-in e é atualizada posteriormente.

## 22 de janeiro de 2020

### Extensão do Experience Cloud ID 4.5.2

#### **Recursos**

* Atualização do visitor.js para 4.5.2
* O Visitante 4.5.1 inclui uma correção de erro para o plug-in IAB para Optin
* Atualização do `setCustomerIDs` método para rejeitar IDs vazias enviadas.

## 7 de janeiro de 2020

### Extensão do Experience Cloud ID 4.4.2

#### **Recursos**

* Atualização do visitor.js para 4.4.2
* Melhorias no `getVisitorValues` método para obter valores mais rapidamente.


## 19 de setembro de 2019

### Extensão do Experience Cloud ID 4.4.1

#### **Recursos**

* Atualização do visitor.js para 4.4.1
* Correção de um erro para obter a Entrada de pré-aprovações de inclusão
* VIDEO_ANALYTICS renomeado para MEDIA_ANALYTICS em preOptInApprovals

   ![](../../../images/ecid-media-analytics.png)

## 17 de julho de 2019

### Extensão do Experience Cloud ID 4.4.0

#### **Recursos**

* Atualização do visitor.js para 4.4.0
* Suporte para hashing SHA256 adicionado para setCustomerIDs

   ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 de maio de 2019

### Extensão do Experience Cloud ID 4.3.1

#### **Recursos**

* Atualização do visitor.js para 4.3
* Adição do tipo de elemento de dados para ECID como parte da extensão de tag

   ![](../../../images/ecid-data-element.png)

## 9 de abril de 2019

### Extensão do Experience Cloud ID 4.2.0

#### **Recursos**

* Atualização do visitor.js para a versão 4.2, que inclui suporte para o plug-in do Audience Manager IAB TCF.

## 25 de fevereiro de 2019

### Extensão do Experience Cloud ID 4.1.0

#### **Recursos**

* Atualização de visitor.js para 4.1, que atualizou publishDestinations por nova alteração da API. Com essa atualização, as informações do referenciador da página podem ser expostas durante a sincronização de ID, se desejado.

## 15 de fevereiro de 2019

### Extensão do Experience Cloud ID 4.0.0

#### **Recursos**

* Atualização do visitor.js para 4.0
* Adicionadas opções de configuração para o novo objeto Aceitar incorporado. Configurações do aceitação podem ser usadas para suprimir chamadas de cookie e de sinais feitas pelas soluções da Adobe para melhor suportar regulamentos, como o GDPR

   ![](../../../images/ext-mcid-opt-in.png)

## 20 de março de 2018

### Extensão do Experience Cloud ID 3.1.0

#### **Recursos**

* Atualização do visitor.js para 3.1
* Adiciona duas propriedades de configuração: `resetBeforeVersion` e `serverState`.

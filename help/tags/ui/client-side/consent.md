---
title: Implantar tags do JavaScript para gerenciar o consentimento do cliente
description: Saiba como gerenciar sinais de aceitação e recusa do cliente para várias soluções de Adobe no Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 94%

---

# Implantar tags do JavaScript para gerenciar o consentimento do cliente

As regulamentações legais de privacidade, como o Regulamento Geral sobre a Proteção de Dados (GDPR), exigem que as empresas consigam gerenciar o consentimento de seus usuários. Os clientes da Adobe podem exigir a aceitação dos visitantes antes que as soluções da Adobe sejam executadas para qualquer visitante. Os visitantes devem ter a capacidade de gerenciar seu status de participação e não participação.

Os clientes da Adobe Experience Cloud exigem uma variedade de implementações desses requisitos. Alguns usam os gerentes de consentimento de nível empresarial e outros criam os seus próprios.

Desenvolvedores de extensões da Adobe Experience Platform usam o criador de regras e extensões para definir soluções de aceitação e de recusa.

Este documento contém informações sobre como impedir que tags da Adobe sejam acionadas antes que o consentimento tenha sido adquirido.

## Advertising Cloud

A Adobe Experience Platform não dispara o [!DNL Advertising Cloud] automaticamente. O [!DNL Advertising Cloud] somente será acionado se você indicar especificamente em uma ação de regra que ele deve ser acionado. Use as condições da regra para determinar quando e o que acionar. Por exemplo, para usar cookies para determinar o status de aceitação, defina um elemento de dados para ler esse cookie e use-o como uma condição na regra para determinar quando acionar a ação Conversão de rastreamento.

Integrações com gerentes de consentimento (como o OneTrust) podem definir e rastrear os cookies de consentimento dos clientes, que podem ser usados no criador de regras.

## Analytics

Na seção Rastreamento de link das definições das configurações da extensão do [!DNL Analytics], verifique se o seguinte *não* está selecionado:

* Rastrear os links de download
* Rastrear links externos

Quando essas configurações não estão selecionadas, o Experience Platform não dispara o [!DNL Adobe Analytics] automaticamente. O [!DNL Analytics] somente será acionado se você indicar especificamente em uma ação de regra que ele deve ser acionado. Use as condições da regra para determinar quando e o que acionar. Por exemplo, para usar cookies para determinar o status de aceitação, defina um elemento de dados para ler esse cookie e use-o como uma condição na regra para determinar quando acionar a ação Enviar Beacon.

Separadamente, você pode considerar o uso do [objeto de aceitação da Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=pt-BR) para controlar o acionamento dessa tag em conjunto com sua plataforma de gerenciamento de consentimento.

Integrações com gerentes de consentimento (como o OneTrust) podem definir e rastrear os cookies de consentimento dos clientes, que podem ser usados no criador de regras.

## Audience Manager

No momento, o DIL está definido para ser acionado automaticamente, se for colocado em uma página do cliente. Considere usar o [objeto de aceitação da Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=pt-BR) para controlar o acionamento desta tag em conjunto com a sua plataforma de gerenciamento de consentimento.

O [!DNL Adobe] recomenda o uso do encaminhamento pelo lado do servidor dentro do [!DNL Analytics].

## Experience Cloud ID

No momento, o [!DNL Experience Cloud ID] é acionado automaticamente, se for colocado em uma página do cliente. 

Considere usar o [objeto de aceitação da Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=pt-BR) para controlar o acionamento desta tag em conjunto com a sua plataforma de gerenciamento de consentimento.

## Target

A Adobe Experience Platform não dispara o [!DNL Target] automaticamente. O [!DNL Target] somente será acionado se você indicar especificamente em uma ação de regra que ele deve ser acionado. Use as condições da regra para determinar quando e o que acionar. Por exemplo, para usar cookies para determinar o status de aceitação, defina um elemento de dados para ler esse cookie e use-o como uma condição na regra para determinar quando acionar a ação Carregar [!DNL Target].

Separadamente, você pode considerar o uso do [objeto de aceitação da Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=pt-BR) para controlar o acionamento dessa tag em conjunto com sua plataforma de gerenciamento de consentimento.

Integrações com gerentes de consentimento (como o OneTrust) podem definir e rastrear os cookies de consentimento dos clientes, que podem ser usados no criador de regras.

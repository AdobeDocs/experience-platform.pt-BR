---
title: Definições de configuração de identidade
description: Defina como a extensão de tag identifica visitantes.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 2%

---

# Definições de configuração de identidade

Esta seção de configuração permite definir o comportamento do Web SDK quando se trata de lidar com a identificação do usuário.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role até a seção **[!UICONTROL Identity]**.

![Imagem mostrando as configurações de identidade da extensão de marca do Web SDK na interface do usuário de Marcas](../assets/web-sdk-ext-identity.png)

As opções disponíveis são as seguintes:

## [!UICONTROL Migrate ECID from VisitorAPI]

Uma caixa de seleção que permite que o Web SDK leia os cookies `AMCV` e `s_ecid` e defina o cookie `AMCV` usado por `Visitor.js`. Esse recurso é importante ao migrar de bibliotecas que usam o `VisitorAPI.js` para o Web SDK, pois algumas páginas ainda podem estar usando o `Visitor.js`. Essa opção permite que o SDK continue usando a mesma ECID para que os usuários não sejam identificados como dois usuários separados. O equivalente a esta caixa de seleção na biblioteca de JavaScript é [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## [!UICONTROL Use third-party cookies]

Quando essa opção é ativada, o Web SDK tenta armazenar um identificador do usuário em um cookie de terceiros. Se for bem-sucedido, o usuário será identificado como um único usuário durante a navegação em vários domínios, em vez de ser identificado como um usuário separado em cada domínio. Se essa opção estiver ativada, o SDK ainda poderá não conseguir armazenar o identificador do usuário em um cookie de terceiros se o navegador não for compatível com cookies de terceiros ou tiver sido configurado pelo usuário para não permitir cookies de terceiros. Nesse caso, o SDK armazena apenas o identificador no domínio próprio. O equivalente a esta caixa de seleção na biblioteca de JavaScript é [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md).

>[!IMPORTANT]
>
>Cookies de terceiros não são compatíveis com a funcionalidade [ID de dispositivo próprio](/help/collection/use-cases/identity/first-party-device-ids.md) no Web SDK. Você pode usar IDs de dispositivo primário ou cookies de terceiros; não é possível usar ambos os recursos simultaneamente.

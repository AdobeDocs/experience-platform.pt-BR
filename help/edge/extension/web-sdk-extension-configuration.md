---
title: Configuração do SDK da Web da Adobe Experience Platform
description: Saiba mais sobre a extensão de tag do SDK da Web da Adobe Experience Platform.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 8%

---

# Visão geral

A extensão Adobe Experience Platform Web SDK envia dados para a Adobe Experience Cloud a partir de propriedades da Web por meio da rede de borda Adobe Experience Platform. A extensão permite fazer o stream de dados para a Plataforma, sincronizar identidades, processar sinais de consentimento do cliente e coletar dados de contexto automaticamente.

Este documento aborda como configurar a extensão na interface do usuário da coleta de dados.

## Configurar a extensão

Se a extensão SDK da Web da plataforma já tiver sido instalada para uma propriedade, abra a propriedade na interface do usuário da coleta de dados e selecione a guia **[!UICONTROL Extensões]**. No SDK da Web da plataforma, selecione **[!UICONTROL Configurar]**.

![](../images/extension/overview/configure.png)

Se ainda não tiver instalado a extensão, selecione a guia **[!UICONTROL Catalog]**. Na lista de extensões disponíveis, encontre a extensão SDK da Web da plataforma e selecione **[!UICONTROL Instalar]**.

![](../images/extension/overview/install.png)

Em ambos os casos, você chega à página de configuração do SDK da Web da plataforma. As seções abaixo explicam as opções de configuração da extensão.

![](../images/extension/overview/config-screen.png)

## Opções gerais de configuração

As opções de configuração na parte superior da página informam à Adobe Experience Platform onde rotear os dados e quais configurações usar no servidor.

### [!UICONTROL Nome]

A extensão Adobe Experience Platform Web SDK oferece suporte a várias instâncias na página. O nome é usado para enviar dados para várias organizações com uma configuração de tag.

O nome da extensão assume como padrão &quot;[!DNL alloy]&quot;. No entanto, é possível alterar o nome da instância para qualquer nome de objeto JavaScript válido.

### **[!UICONTROL ID da organização IMS]**

A [!UICONTROL IMS Organization ID] é a organização para a qual você deseja que os dados sejam enviados no Adobe. Na maioria das vezes, use o valor padrão preenchido automaticamente. Quando houver várias instâncias na página, preencha este campo com o valor da segunda organização para a qual deseja enviar dados.

### **[!UICONTROL Domínio de borda]**

O [!UICONTROL Domínio de borda] é o domínio do qual a extensão Adobe Experience Platform envia e recebe dados. A extensão requer o uso de um CNAME próprio para o tráfego de produção. O domínio padrão de terceiros funciona em ambientes de desenvolvimento, mas não é adequado para ambientes de produção. As instruções sobre como configurar um CNAME primário estão listadas [aqui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=pt-BR).

## [!UICONTROL Datastreams]

Quando uma solicitação é enviada para a Rede de borda da Adobe Experience Platform, uma ID de armazenamento de dados é usada para fazer referência à configuração do lado do servidor. Você pode atualizar a configuração sem precisar fazer alterações de código em seu site.

Consulte o guia em [datastreams](../fundamentals/datastreams.md) para obter mais informações.


## [!UICONTROL Privacidade]

![](../images/extension/overview/privacy.png)

A seção [!UICONTROL Privacy] permite configurar como o SDK lida com sinais de consentimento do usuário em seu site. Especificamente, permite selecionar o nível padrão de consentimento que é presumido de um usuário se nenhuma outra preferência de consentimento explícita tiver sido fornecida. O nível de consentimento padrão não é salvo no perfil do usuário. O quadro a seguir detalha o que cada opção implica:

| [!UICONTROL Nível de consentimento padrão] | Descrição |
| --- | --- |
| [!UICONTROL Em] | Colete eventos que ocorrem antes que o usuário forneça as preferências de consentimento. |
| [!UICONTROL Out] | Descarte os eventos que ocorrem antes que o usuário forneça as preferências de consentimento. |
| [!UICONTROL Pending] | Enfileirar eventos que ocorrem antes que o usuário forneça as preferências de consentimento. Quando as preferências de consentimento são fornecidas, os eventos são coletados ou descartados, dependendo das preferências fornecidas. |
| [!UICONTROL Fornecido pelo elemento de dados] | O nível de consentimento padrão é determinado por um elemento de dados separado que você define. Ao usar essa opção, você deve especificar o elemento de dados usando o menu suspenso fornecido. |

Use Fora ou Pendente se precisar de consentimento explícito do usuário para suas operações comerciais.

## [!UICONTROL Identidade]

![](../images/extension/overview/identity.png)

### [!UICONTROL Migrar ECID da VisitorAPI]

Essa opção está ativada por padrão. Quando esse recurso é ativado, o SDK pode ler os cookies AMCV e s_ecid e definir o cookie AMCV usado por Visitor.js. Esse recurso é importante ao migrar para o SDK da Web da Adobe Experience Platform, pois algumas páginas ainda podem estar usando o Visitor.js. Ela permite que o SDK continue a usar a mesma ECID para que os usuários não sejam identificados como dois usuários separados.

### [!UICONTROL Usar cookies de terceiros]

Essa opção permite que o SDK tente armazenar um identificador de usuário em um cookie de terceiros. Se bem-sucedido, o usuário é identificado como um único usuário enquanto navega em vários domínios, em vez de ser identificado como um usuário separado em cada domínio. Se essa opção estiver ativada, o SDK ainda poderá não conseguir armazenar o identificador do usuário em um cookie de terceiros se o navegador não oferecer suporte a cookies de terceiros ou se tiver sido configurado pelo usuário para não permitir cookies de terceiros. Nesse caso, o SDK armazena apenas o identificador no domínio próprio.

## [!UICONTROL Personalização]

![](../images/extension/overview/personalization.png)

Se você quiser ocultar determinadas partes se o site enquanto o conteúdo personalizado estiver carregado, é possível especificar os elementos a serem ocultados no editor de estilo pré-ocultado. Em seguida, você pode copiar o trecho pré-ocultação padrão fornecido a você e colá-lo dentro do elemento `<head>`do site HTML.

## [!UICONTROL Coleta de dados]

![](../images/extension/overview/data-collection.png)

### [!UICONTROL Função de retorno de chamada]

A função de retorno de chamada fornecida na extensão também é chamada de função [`onBeforeEventSend`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) na biblioteca. Essa função permite modificar eventos globalmente antes de serem enviados para a Adobe Edge Network. Informações mais detalhadas sobre como usar esta função podem ser encontradas [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Clique em coleção de dados]

O SDK pode coletar automaticamente as informações de clique do link para você. Por padrão, esse recurso está ativado, mas pode ser desativado usando essa opção. Os links também são rotulados como links de download se contiverem uma das expressões de download listadas na caixa de texto [!UICONTROL Baixar qualificador de link]. O Adobe fornece alguns qualificadores padrão de link de download, mas eles podem ser editados a qualquer momento.

### [!UICONTROL Dados de contexto coletados automaticamente]

Por padrão, o SDK coleta determinados dados de contexto relacionados ao dispositivo, à Web, ao ambiente e ao contexto de local. Se quiser ver uma lista das informações coletadas pelo Adobe, poderá encontrá-la [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Se não quiser que esses dados sejam coletados ou se quiser que apenas determinadas categorias de dados sejam coletadas, é possível alterar essas opções.

## [!UICONTROL Configurações avançadas]

![](../images/extension/overview/advanced-settings.png)

### [!UICONTROL Caminho base da borda]

Use esse campo se precisar alterar o caminho base usado para interagir com a Rede Adobe Edge. Isso não deve exigir atualização, mas, no caso de participar de um beta ou alfa, o Adobe pode solicitar que você altere esse campo.

---
title: Configurar a extensão Adobe Experience Platform Web SDK
description: Como configurar a extensão de tag do SDK da Web da Adobe Experience Platform na interface do usuário.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 6%

---

# Configurar a extensão Adobe Experience Platform Web SDK

A extensão de tag do SDK da Web da Adobe Experience Platform envia dados para a Adobe Experience Cloud a partir de propriedades da Web por meio da Rede de borda da Adobe Experience Platform. A extensão permite fazer o stream de dados para a Plataforma, sincronizar identidades, processar sinais de consentimento do cliente e coletar dados de contexto automaticamente.

Este documento aborda como configurar a extensão na interface do usuário do .

## Introdução

Se a extensão SDK da Web da plataforma já tiver sido instalada para uma propriedade, abra a propriedade na interface do usuário e selecione a variável **[!UICONTROL Extensões]** guia . No SDK da Web da plataforma, selecione **[!UICONTROL Configurar]**.

![](../assets/extension/overview/configure.png)

Se ainda não tiver instalado a extensão, selecione a **[!UICONTROL Catálogo]** guia . Na lista de extensões disponíveis, encontre a extensão SDK da Web da plataforma e selecione **[!UICONTROL Instalar]**.

![](../assets/extension/overview/install.png)

Em ambos os casos, você chega à página de configuração do SDK da Web da plataforma. As seções abaixo explicam as opções de configuração da extensão.

![](../assets/extension/overview/config-screen.png)

## Opções gerais de configuração

As opções de configuração na parte superior da página informam à Adobe Experience Platform onde rotear os dados e quais configurações usar no servidor.

### [!UICONTROL Nome]

A extensão Adobe Experience Platform Web SDK oferece suporte a várias instâncias na página. O nome é usado para enviar dados para várias organizações com uma configuração de tag.

O nome padrão da extensão é &quot;[!DNL alloy]&quot;. No entanto, é possível alterar o nome da instância para qualquer nome de objeto JavaScript válido.

### **[!UICONTROL ID da organização IMS]**

O [!UICONTROL IMS Organization ID] é a organização para a qual você deseja que os dados sejam enviados no Adobe. Na maioria das vezes, use o valor padrão preenchido automaticamente. Quando houver várias instâncias na página, preencha este campo com o valor da segunda organização para a qual deseja enviar dados.

### **[!UICONTROL Domínio de borda]**

O [!UICONTROL Domínio de borda] é o domínio do qual a extensão Adobe Experience Platform envia e recebe dados. O Adobe recomenda usar um domínio próprio (CNAME) para essa extensão. O domínio padrão de terceiros funciona em ambientes de desenvolvimento, mas não é adequado para ambientes de produção. As instruções sobre como configurar um CNAME primário estão listadas [aqui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=pt-BR).

## [!UICONTROL Datastreams]

Quando uma solicitação é enviada para a Rede de borda da Adobe Experience Platform, uma ID de armazenamento de dados é usada para fazer referência à configuração do lado do servidor. Você pode atualizar a configuração sem precisar fazer alterações de código em seu site.

Consulte o guia sobre [datastreams](../datastreams/overview.md) para obter mais informações.


## [!UICONTROL Privacidade]

![](../assets/extension/overview/privacy.png)

O [!UICONTROL Privacidade] permite configurar como o SDK lida com sinais de consentimento do usuário em seu site. Especificamente, permite selecionar o nível padrão de consentimento que é presumido de um usuário se nenhuma outra preferência de consentimento explícita tiver sido fornecida. O nível de consentimento padrão não é salvo no perfil do usuário. O quadro a seguir detalha o que cada opção implica:

| [!UICONTROL Nível de consentimento padrão] | Descrição |
| --- | --- |
| [!UICONTROL Em] | Colete eventos que ocorrem antes que o usuário forneça as preferências de consentimento. |
| [!UICONTROL Out] | Descarte os eventos que ocorrem antes que o usuário forneça as preferências de consentimento. |
| [!UICONTROL Pending] | Enfileirar eventos que ocorrem antes que o usuário forneça as preferências de consentimento. Quando as preferências de consentimento são fornecidas, os eventos são coletados ou descartados, dependendo das preferências fornecidas. |
| [!UICONTROL Fornecido pelo elemento de dados] | O nível de consentimento padrão é determinado por um elemento de dados separado que você define. Ao usar essa opção, você deve especificar o elemento de dados usando o menu suspenso fornecido. |

Use Fora ou Pendente se precisar de consentimento explícito do usuário para suas operações comerciais.

## [!UICONTROL Identidade]

![](../assets/extension/overview/identity.png)

### [!UICONTROL Migrar ECID da VisitorAPI]

Essa opção está ativada por padrão. Quando esse recurso é ativado, o SDK pode ler os cookies AMCV e s_ecid e definir o cookie AMCV usado por Visitor.js. Esse recurso é importante ao migrar para o SDK da Web da Adobe Experience Platform, pois algumas páginas ainda podem estar usando o Visitor.js. Ela permite que o SDK continue a usar a mesma ECID para que os usuários não sejam identificados como dois usuários separados.

### [!UICONTROL Usar cookies de terceiros]

Essa opção permite que o SDK tente armazenar um identificador de usuário em um cookie de terceiros. Se bem-sucedido, o usuário é identificado como um único usuário enquanto navega em vários domínios, em vez de ser identificado como um usuário separado em cada domínio. Se essa opção estiver ativada, o SDK ainda poderá não conseguir armazenar o identificador do usuário em um cookie de terceiros se o navegador não oferecer suporte a cookies de terceiros ou se tiver sido configurado pelo usuário para não permitir cookies de terceiros. Nesse caso, o SDK armazena apenas o identificador no domínio próprio.

## [!UICONTROL Personalização]

![](../assets/extension/overview/personalization.png)

Se você quiser ocultar determinadas partes se o site enquanto o conteúdo personalizado estiver carregado, é possível especificar os elementos a serem ocultados no editor de estilo pré-ocultado. Em seguida, você pode copiar o trecho pré-ocultação padrão fornecido para você e colá-lo dentro do `<head>`elemento do seu HTML site.

## [!UICONTROL Coleta de dados]

![](../assets/extension/overview/data-collection.png)

### [!UICONTROL Função de retorno de chamada]

A função de retorno de chamada fornecida na extensão também é chamada de [`onBeforeEventSend` função](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=pt-BR) na biblioteca. Essa função permite modificar eventos globalmente antes de serem enviados para a Adobe Edge Network. Encontre informações mais detalhadas sobre como usar essa função [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Clique em coleção de dados]

O SDK pode coletar automaticamente as informações de clique do link para você. Por padrão, esse recurso está ativado, mas pode ser desativado usando essa opção. Os links também são rotulados como links de download se contiverem uma das expressões de download listadas na [!UICONTROL Qualificador de link de download] caixa de texto. O Adobe fornece alguns qualificadores padrão de link de download, mas eles podem ser editados a qualquer momento.

### [!UICONTROL Dados de contexto coletados automaticamente]

Por padrão, o SDK coleta determinados dados de contexto relacionados ao dispositivo, à Web, ao ambiente e ao contexto de local. Se quiser ver uma lista das informações coletadas pelo Adobe, poderá encontrá-la [here](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Se não quiser que esses dados sejam coletados ou se quiser que apenas determinadas categorias de dados sejam coletadas, é possível alterar essas opções.

## [!UICONTROL Substituições de configuração do fluxo de dados]

As substituições de conjunto de dados permitem definir configurações adicionais para seus conjuntos de dados, que são passados para a Rede de borda por meio do SDK da Web.

Isso ajuda você a acionar diferentes comportamentos do conjunto de dados do que os padrão, sem criar um novo conjunto de dados ou modificar as configurações existentes.

A substituição da configuração do conjunto de dados é um processo de duas etapas:

1. Primeiro, você deve definir as substituições de configuração do conjunto de dados na variável [página de configuração do datastream](../datastreams/configure.md).
2. Em seguida, você deve enviar as substituições para a Edge Network por meio de um comando do SDK da Web ou usando a extensão de tag do SDK da Web.

Consulte o datastream [documentação de substituições de configuração](../datastreams/overrides.md) para obter instruções detalhadas sobre como substituir configurações do conjunto de dados.

Como alternativa a transmitir as substituições por meio de um comando do SDK da Web, é possível configurar as substituições na tela de extensão da tag mostrada abaixo.

![Imagem que mostra as substituições de configuração do conjunto de dados na página de extensão da tag do SDK da Web.](../assets/extension/overview/datastream-overrides.png)

## [!UICONTROL Configurações avançadas]

![](../assets/extension/overview/advanced-settings.png)

### [!UICONTROL Caminho base da borda]

Use esse campo se precisar alterar o caminho base usado para interagir com a Rede Adobe Edge. Isso não deve exigir atualização, mas, no caso de participar de um beta ou alfa, o Adobe pode solicitar que você altere esse campo.

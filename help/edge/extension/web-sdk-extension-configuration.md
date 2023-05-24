---
title: Configurar a extensão SDK da Web do Adobe Experience Platform
description: Como configurar a extensão de tag do SDK da Web da Adobe Experience Platform na interface do usuário do.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 6%

---

# Configurar a extensão SDK da Web do Adobe Experience Platform

A extensão de tag do SDK da Web da Adobe Experience Platform envia dados para a Adobe Experience Cloud a partir das propriedades da Web por meio da Rede de borda da Adobe Experience Platform. A extensão permite transmitir dados para a Platform, sincronizar identidades, processar sinais de consentimento do cliente e coletar automaticamente dados de contexto.

Este documento aborda como configurar a extensão na interface do usuário do.

## Introdução

Se a extensão SDK da Web da Platform já tiver sido instalada para uma propriedade, abra a propriedade na interface do usuário e selecione a **[!UICONTROL Extensões]** guia. No SDK da Web da Platform, selecione **[!UICONTROL Configurar]**.

![](../assets/extension/overview/configure.png)

Se ainda não tiver instalado a extensão, selecione a opção **[!UICONTROL Catálogo]** guia. Na lista de extensões disponíveis, localize a extensão SDK da Web da plataforma e selecione **[!UICONTROL Instalar]**.

![](../assets/extension/overview/install.png)

Em ambos os casos, você acessa a página de configuração do SDK da Web da plataforma. As seções abaixo explicam as opções de configuração da extensão.

![](../assets/extension/overview/config-screen.png)

## Opções gerais de configuração

As opções de configuração na parte superior da página informam à Adobe Experience Platform para onde rotear os dados e quais configurações usar no servidor.

### [!UICONTROL Nome]

A extensão SDK da Web da Adobe Experience Platform é compatível com várias instâncias na página. O nome é usado para enviar dados para várias organizações com uma configuração de tag.

O nome padrão da extensão é &quot;[!DNL alloy]&quot;. No entanto, é possível alterar o nome da instância para qualquer nome de objeto JavaScript válido.

### **[!UICONTROL ID da organização IMS]**

A variável [!UICONTROL IMS Organization ID] é a organização para a qual você deseja que os dados sejam enviados no Adobe. Na maioria das vezes, use o valor padrão preenchido automaticamente. Quando houver várias instâncias na página, preencha esse campo com o valor da segunda organização para a qual deseja enviar dados.

### **[!UICONTROL Domínio de borda]**

A variável [!UICONTROL Domínio de borda] é o domínio do qual a extensão do Adobe Experience Platform envia e recebe dados. O Adobe recomenda usar um domínio próprio (CNAME) para essa extensão. O domínio padrão de terceiros funciona em ambientes de desenvolvimento, mas não é adequado para ambientes de produção. As instruções sobre como configurar um CNAME primário estão listadas [aqui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=pt-BR).

## [!UICONTROL Datastreams]

Quando uma solicitação é enviada para a Rede de borda da Adobe Experience Platform, uma ID de sequência de dados é usada para fazer referência à configuração do lado do servidor. Você pode atualizar a configuração sem precisar fazer alterações de código no site.

Consulte o guia sobre [sequências de dados](../datastreams/overview.md) para obter mais informações.


## [!UICONTROL Privacidade]

![](../assets/extension/overview/privacy.png)

A variável [!UICONTROL Privacidade] permite configurar como o SDK lida com sinais de consentimento do usuário do seu site. Especificamente, ela permite selecionar o nível padrão de consentimento assumido de um usuário se nenhuma outra preferência de consentimento explícito tiver sido fornecida. O nível de consentimento padrão não é salvo no perfil do usuário. A tabela a seguir detalha o que cada opção implica:

| [!UICONTROL Nível de consentimento padrão] | Descrição |
| --- | --- |
| [!UICONTROL Em] | Colete eventos que ocorrem antes de o usuário fornecer preferências de consentimento. |
| [!UICONTROL Saída] | Descartar eventos que ocorrem antes de o usuário fornecer preferências de consentimento. |
| [!UICONTROL Pending] | Enfileirar eventos que ocorrem antes de o usuário fornecer preferências de consentimento. Quando as preferências de consentimento são fornecidas, os eventos são coletados ou descartados, dependendo das preferências fornecidas. |
| [!UICONTROL Fornecido pelo elemento de dados] | O nível de consentimento padrão é determinado por um elemento de dados separado que você define. Ao usar essa opção, você deve especificar o elemento de dados usando o menu suspenso fornecido. |

Use Fora ou Pendente se você precisar de consentimento explícito do usuário para suas operações comerciais.

## [!UICONTROL Identidade]

![](../assets/extension/overview/identity.png)

### [!UICONTROL Migrar ECID da VisitorAPI]

Essa opção está ativada por padrão. Quando esse recurso está ativado, o SDK pode ler os cookies AMCV e s_ecid e definir o cookie AMCV usado pelo Visitor.js. Esse recurso é importante ao migrar para o Adobe Experience Platform Web SDK, pois algumas páginas ainda podem estar usando o Visitor.js. Ele permite que o SDK continue usando a mesma ECID para que os usuários não sejam identificados como dois usuários separados.

### [!UICONTROL Usar cookies de terceiros]

Essa opção permite que o SDK tente armazenar um identificador do usuário em um cookie de terceiros. Se for bem-sucedido, o usuário será identificado como um único usuário durante a navegação em vários domínios, em vez de ser identificado como um usuário separado em cada domínio. Se essa opção estiver ativada, o SDK ainda poderá não ser capaz de armazenar o identificador do usuário em um cookie de terceiros se o navegador não for compatível com cookies de terceiros ou tiver sido configurado pelo usuário para não permitir cookies de terceiros. Nesse caso, o SDK armazena apenas o identificador no domínio próprio.

## [!UICONTROL Personalização]

![](../assets/extension/overview/personalization.png)

Se você quiser ocultar determinadas partes do site enquanto o conteúdo personalizado estiver carregado, especifique os elementos a serem ocultados no editor de estilos de pré-ocultação. Em seguida, você pode copiar o trecho pré-ocultação padrão fornecido e colá-lo dentro do `<head>`elemento do site HTML.

## [!UICONTROL Coleta de dados]

![](../assets/extension/overview/data-collection.png)

### [!UICONTROL Função de retorno de chamada]

A função de retorno de chamada fornecida na extensão também é chamada de [`onBeforeEventSend` função](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=pt-BR) na biblioteca. Essa função permite modificar eventos globalmente antes que sejam enviados para a Rede da Adobe Edge. Informações mais detalhadas sobre como usar esta função podem ser encontradas [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Clique em coleta de dados]

O SDK pode coletar automaticamente informações de cliques em links para você. Por padrão, esse recurso está ativado, mas pode ser desativado usando essa opção. Os links também são rotulados como links de download se contiverem uma das expressões de download listadas no [!UICONTROL Baixar qualificador de link] caixa de texto. O Adobe fornece alguns qualificadores de link de download padrão, mas eles podem ser editados a qualquer momento.

### [!UICONTROL Dados de contexto coletados automaticamente]

Por padrão, o SDK coleta determinados dados de contexto relacionados ao dispositivo, Web, ambiente e contexto de local. Se quiser ver uma lista dos Adobe de informações coletados, você pode encontrá-la [aqui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Se você não quiser que esses dados sejam coletados ou se quiser apenas determinadas categorias de dados, poderá alterar essas opções.

## [!UICONTROL Substituições da configuração da sequência de dados]

As substituições de sequência de dados permitem definir configurações adicionais para suas sequências de dados, que são transmitidas para a Rede de borda por meio do SDK da Web.

Isso ajuda a acionar comportamentos de sequência de dados diferentes dos padrão, sem criar uma nova sequência de dados ou modificar as configurações existentes.

A substituição da configuração da sequência de dados é um processo de duas etapas:

1. Primeiro, você deve definir as substituições de configuração da sequência de dados no [página de configuração do fluxo de dados](../datastreams/configure.md).
2. Em seguida, você deve enviar as substituições para a Rede de borda por meio de um comando do SDK da Web ou usando a extensão de tag do SDK da Web.

Ver a sequência de dados [documentação de substituições de configuração](../datastreams/overrides.md) para obter instruções detalhadas sobre como substituir configurações de sequência de dados.

Como alternativa à transmissão de sobreposições por meio de um comando do SDK da Web, você pode configurar as sobreposições na tela de extensão de tag mostrada abaixo.

![Imagem que mostra as sobreposições de configuração da sequência de dados na página de extensão de tag do SDK da Web.](../assets/extension/overview/datastream-overrides.png)

## [!UICONTROL Configurações avançadas]

![](../assets/extension/overview/advanced-settings.png)

### [!UICONTROL Caminho base da borda]

Use esse campo se precisar alterar o caminho base usado para interagir com a Adobe Edge Network. Isso não deve exigir atualização, mas no caso de você participar de um beta ou alfa, o Adobe pode solicitar que você altere esse campo.

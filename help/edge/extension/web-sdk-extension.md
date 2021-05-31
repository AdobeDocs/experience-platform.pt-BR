---
title: Visão geral da extensão do SDK da Web da Adobe Experience Platform
description: Saiba mais sobre a extensão Adobe Experience Platform Web SDK para Adobe Experience Platform Launch
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 13%

---

# Visão geral da extensão do SDK da Web da Adobe Experience Platform

A extensão Adobe Experience Platform Web SDK envia dados para a Adobe Experience Cloud a partir de propriedades da Web por meio da rede de borda Adobe Experience Platform. A extensão permite fazer o stream de dados para a Plataforma, sincronizar identidades, processar sinais de consentimento do cliente e coletar dados de contexto automaticamente.

Este documento aborda como configurar a extensão na interface do usuário do Adobe Experience Platform Launch.

## Configurar a extensão

Se a extensão SDK da Web da plataforma já tiver sido instalada para uma propriedade, abra a propriedade na interface do usuário do Platform launch e selecione a guia **[!UICONTROL Extensões]**. No SDK da Web da plataforma, selecione **[!UICONTROL Configurar]**.

![](../images/extension/overview/configure.png)

Se ainda não tiver instalado a extensão, selecione a guia **[!UICONTROL Catalog]**. Na lista de extensões disponíveis, encontre a extensão SDK da Web da plataforma e selecione **[!UICONTROL Instalar]**.

![](../images/extension/overview/install.png)

Em ambos os casos, você chega à página de configuração do SDK da Web da plataforma. As seções abaixo explicam as opções de configuração da extensão.

![](../images/extension/overview/config-screen.png)

## Opções gerais de configuração

As opções de configuração na parte superior da página informam à Adobe Experience Platform onde rotear os dados e quais configurações usar no servidor.

### [!UICONTROL Nome]

A extensão Adobe Experience Platform Web SDK oferece suporte a várias instâncias na página. O nome é usado para enviar dados para várias organizações com uma única configuração de Platform launch.

O nome da extensão assume como padrão &quot;[!DNL alloy]&quot;. No entanto, é possível alterar o nome da instância para qualquer nome de objeto JavaScript válido.

### **[!UICONTROL ID da organização IMS]**

A [!UICONTROL IMS Organization ID] é a organização para a qual você deseja que os dados sejam enviados no Adobe. Na maioria das vezes, use o valor padrão preenchido automaticamente. Quando houver várias instâncias na página, preencha este campo com o valor da segunda organização para a qual deseja enviar dados.

### **[!UICONTROL Domínio de borda]**

O [!UICONTROL Domínio de borda] é o domínio do qual a extensão Adobe Experience Platform envia e recebe dados. A extensão requer o uso de um CNAME próprio para o tráfego de produção. O domínio padrão de terceiros funciona em ambientes de desenvolvimento, mas não é adequado para ambientes de produção. As instruções sobre como configurar um CNAME primário estão listadas [aqui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Datastreams]

Quando uma solicitação é enviada para a Rede de borda da Adobe Experience Platform, uma ID de armazenamento de dados é usada para fazer referência à configuração do lado do servidor. Você pode atualizar a configuração sem precisar fazer alterações de código em seu site.

Consulte o guia em [datastreams](../fundamentals/datastreams.md) para obter mais informações.


## [!UICONTROL Privacidade]

A seção [!UICONTROL Privacy] permite configurar como o SDK lida com sinais de consentimento do usuário em seu site. Especificamente, permite selecionar o nível padrão de consentimento que é presumido de um usuário se nenhuma outra preferência de consentimento explícita tiver sido fornecida. O nível de consentimento padrão não é salvo no perfil do usuário. O quadro a seguir detalha o que cada opção implica:

| [!UICONTROL Nível de consentimento padrão] | Descrição |
| --- | --- |
| [!UICONTROL Em] | Colete eventos que ocorrem antes que o usuário forneça as preferências de consentimento. |
| [!UICONTROL Out] | Descarte os eventos que ocorrem antes que o usuário forneça as preferências de consentimento. |
| [!UICONTROL Pending] | Enfileirar eventos que ocorrem antes que o usuário forneça as preferências de consentimento. Quando as preferências de consentimento são fornecidas, os eventos são coletados ou descartados, dependendo das preferências fornecidas. |
| [!UICONTROL Fornecido pelo elemento de dados] | O nível de consentimento padrão é determinado por um elemento de dados separado que você define. Ao usar essa opção, você deve especificar o elemento de dados usando o menu suspenso fornecido. |

Use Fora ou Pendente se precisar de consentimento explícito do usuário para suas operações comerciais.

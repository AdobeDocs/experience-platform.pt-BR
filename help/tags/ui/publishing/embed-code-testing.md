---
title: Testar códigos incorporados usando o Adobe Experience Platform Debugger
description: Saiba como usar o Experience Platform Debugger para testar localmente diferentes códigos incorporados para o Adobe Experience Platform em seu site.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 50%

---

# Testar códigos incorporados usando o Adobe Experience Platform Debugger

Quando você faz alterações em builds da biblioteca de tags na Adobe Experience Platform, elas devem ser testadas antes da implantação do build no ambiente de produção. Se não tiver um ambiente dedicado de preparo ou desenvolvimento para seu site, você poderá usar o Adobe Experience Platform Debugger para testar localmente diferentes códigos incorporados dentro do site.

## Pré-requisitos

Este tutorial requer entendimento prático do uso de ambientes e códigos incorporados para tags. Consulte a [visão geral de ambientes](./environments.md) para obter mais informações.

Este tutorial também requer que a extensão do navegador do Experience Platform Debugger esteja instalada. O Experience Platform Debugger está disponível para o navegador Chrome. Use o link a seguir para instalar a extensão antes de iniciar o tutorial:

* [Experience Platform Debugger para Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Abra o Experience Platform Debugger em seu site

Usando seu navegador preferido, navegue até seu site e abra a extensão Experience Platform Debugger. O site ao qual o Experience Platform Debugger está conectado no momento é exibido na parte inferior da janela. Se as tags estiverem em execução no site, ele será listado na guia [!UICONTROL Summary].

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Se o Experience Platform Debugger não se conectar inicialmente, talvez seja necessário recarregar a guia do navegador que está exibindo o site antes de tentar novamente.

## Substituir códigos incorporados

Depois que o Experience Platform Debugger se conectar ao seu site, selecione **[!UICONTROL Launch]** na navegação à esquerda. Aqui você pode ver informações sobre a build da biblioteca que está sendo executada no site, incluindo seu ambiente e extensões associadas. Aqui, selecione **[!UICONTROL Configuration]** para exibir controles para gerenciar códigos incorporados.

![](./images/embed-code-testing/launch-tab.png)

Em [!UICONTROL Page Embed Codes], o código incorporado que o site está usando é exibido. Selecione **[!UICONTROL Actions]** no lado direito do código incorporado e selecione **[!UICONTROL Replace]**.

![](./images/embed-code-testing/replace.png)

Uma janela pop-up é exibida, solicitando que você forneça um código incorporado para substituir o atual. Observe que a substituição do código incorporado usando o Experience Platform Debugger não altera o código incorporado implantado em seu site. Em vez disso, ele só substitui o código incorporado executado localmente para que você possa testar e depurar sua implementação.

Cole o código incorporado que deseja testar na caixa de texto fornecida e selecione **[!UICONTROL Apply]**.

![](./images/embed-code-testing/paste-code.png)

A guia **[!UICONTROL Configuration]** será exibida novamente, mostrando que o código incorporado ativo foi substituído pelo código fornecido. Agora você pode usar o navegador da Web para ver se o código incorporado que está testando está funcionando como esperado.

![](./images/embed-code-testing/code-replaced.png)

## Próximas etapas

Este tutorial abordou como alternar localmente códigos incorporados para fins de teste usando o Experience Platform Debugger. Consulte a [documentação do Experience Platform Debugger](../../../debugger/home.md) para obter mais informações sobre seus vários recursos.

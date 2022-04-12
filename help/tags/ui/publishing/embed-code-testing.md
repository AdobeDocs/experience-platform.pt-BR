---
title: Testar códigos incorporados usando o Adobe Experience Platform Debugger
description: Saiba como usar o Platform Debugger para testar localmente diferentes códigos incorporados para o Adobe Experience Platform em seu site.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: 71c63e0d0b993206cb3bb5de7f7fbd5e10c6f2e3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 96%

---

# Testar códigos incorporados usando o Adobe Experience Platform Debugger

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Quando você faz alterações em builds da biblioteca de tags na Adobe Experience Platform, elas devem ser testadas antes da implantação do build no ambiente de produção. Se não tiver um ambiente dedicado de preparo ou desenvolvimento para seu site, você poderá usar o Adobe Experience Platform Debugger para testar localmente diferentes códigos incorporados dentro do site.

## Pré-requisitos

Este tutorial requer entendimento prático do uso de ambientes e códigos integrados na interface da Coleção de dados. Consulte a [visão geral de ambientes](./environments.md) para obter mais informações.

Este tutorial também requer que a extensão do navegador do Platform Debugger esteja instalada. O Platform Debugger só está disponível para os navegadores Chrome e Firefox. Use um dos links a seguir para instalar a extensão antes de iniciar o tutorial:

* [Platform Debugger para Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [Platform Debugger para Firefox](https://addons.mozilla.org/pt-BR/firefox/addon/adobe-experience-platform-dbg/)

## Abrir o Platform Debugger no seu site

Usando seu navegador preferido, navegue até seu site e abra a extensão do Platform Debugger. O site ao qual o Platform Debugger está conectado no momento é exibido na parte inferior da janela. Se as tags estiverem em execução no site, ele será listado na guia [!UICONTROL Resumo].

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Se o Platform Debugger não se conectar inicialmente, talvez seja necessário recarregar a guia do navegador que está exibindo o site antes de tentar novamente.

## Substituir códigos incorporados

Depois que o Platform Debugger se conectar ao seu site, selecione **[!UICONTROL Launch]** na navegação à esquerda. Aqui você pode ver informações sobre a build da biblioteca que está sendo executada no site, incluindo seu ambiente e extensões associadas. Aqui, selecione **[!UICONTROL Configuração]** para exibir controles para gerenciar códigos incorporados.

![](./images/embed-code-testing/launch-tab.png)

Em [!UICONTROL Códigos incorporados de página], o código incorporado que seu site está usando atualmente é exibido. Selecione **[!UICONTROL Ações]** no lado direito do código incorporado e, em seguida, selecione **[!UICONTROL Substituir]**.

![](./images/embed-code-testing/replace.png)

Uma janela pop-up é exibida, solicitando que você forneça um código incorporado para substituir o atual. Observe que a substituição do código incorporado usando o Platform Debugger não altera o código incorporado implantado em seu site. Em vez disso, ele só substitui o código incorporado executado localmente para que você possa testar e depurar sua implementação.

Cole o código incorporado que deseja testar na caixa de texto fornecida e selecione **[!UICONTROL Aplicar]**.

![](./images/embed-code-testing/paste-code.png)

A guia **[!UICONTROL Configuração]** será exibida novamente, mostrando que o código incorporado ativo foi substituído pelo código fornecido Agora você pode usar o navegador da Web para ver se o código incorporado que está testando está funcionando como esperado.

![](./images/embed-code-testing/code-replaced.png)

## Próximas etapas

Este tutorial abordou como alternar localmente códigos incorporados para fins de teste usando o Platform Debugger. Consulte a [documentação do Platform Debugger](../../../debugger/home.md) para obter mais informações sobre seus vários recursos.

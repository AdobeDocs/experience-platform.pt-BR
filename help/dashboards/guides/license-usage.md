---
keywords: Experience Platform, interface do usuário, interface do usuário, personalização, painel de uso de licença, painel, uso de licença, direito, consumo
title: Painel de uso de licença
description: O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre o uso de licenças da sua organização.
topic-legacy: guide
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# (Beta) Painel de uso de licença {#license-usage-dashboard}

>[!IMPORTANT]
>
>A funcionalidade do painel descrita neste documento está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre o uso de licenças de sua organização, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com o painel de uso da licença na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral da interface do usuário da plataforma, visite o [Guia da interface do usuário do Experience Platform](../../landing/ui-guide.md).

## Dados do painel de uso da licença

O painel de uso da licença exibe um instantâneo dos dados relacionados à licença de sua organização para o Experience Platform. Os dados no painel são exibidos exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de uso de licença

Para navegar até o painel de uso da licença na interface do usuário da plataforma, selecione **[!UICONTROL License usage]** no painel esquerdo. Isso é aberto com a guia **[!UICONTROL Overview]** exibindo o painel.

![](../images/license-usage/dashboard-overview.png)

### Selecionar uma sandbox

Para escolher uma sandbox para exibir no painel, selecione [!UICONTROL Production] ou [!UICONTROL Development]. A sandbox selecionada é indicada pelo botão de opção ao lado do nome da sandbox.

>[!NOTE]
>
>O relatório de consumo de sandboxes é cumulativo para todas as sandboxes do mesmo tipo. Em outras palavras, selecionar [!UICONTROL Production] ou [!UICONTROL Development] fornece relatórios de consumo para todas as sandboxes de produção ou desenvolvimento, respectivamente.

![](../images/license-usage/select-sandbox.png)

### Selecionar um intervalo de datas

Depois de selecionar uma sandbox, você pode usar a lista suspensa intervalo de datas para selecionar o período de tempo a ser exibido no painel. Há três opções disponíveis: [!UICONTROL Last 30 days], [!UICONTROL Last 90 days] e [!UICONTROL Last 12 months]. Os últimos 30 dias são selecionados por padrão.

![](../images/license-usage/select-date-range.png)

## Widgets

O painel de uso da licença é composto de widgets, que exibem métricas somente leitura, fornecendo informações importantes sobre o uso da licença de sua organização. As métricas visíveis dependem do licenciamento específico de sua organização (consulte a seção [métricas disponíveis](#available-metrics) para obter detalhes).

Cada widget exibe gráficos de linha que comparam os números reais de sua organização ao total disponível com o licenciamento de sua organização e fornecem uma porcentagem do uso total.

![](../images/license-usage/widgets.png)

## Métricas disponíveis

No momento, há quatro métricas disponíveis no painel de uso da licença:

* [!UICONTROL Addressable Audience] (medido pelo número de perfis)
* [!UICONTROL Average profile richness]
* [!UICONTROL Total consumed storage]
* [!UICONTROL Data scanned per segmentation ratio]

A definição de cada uma dessas métricas varia de acordo com o licenciamento adquirido pela sua organização. Para obter definições detalhadas de cada métrica, consulte a documentação apropriada da Descrição do produto:

| Licença | Descrição do produto |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, serviços de aplicativos e serviços inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>PLATAFORMA DE DADOS DO CLIENTE RT:OD</li><li>PLATAFORMA DE DADOS DO CLIENTE RT:PRFL OD PARA 10M</li><li>PLATAFORMA DE DADOS DO CLIENTE RT:PRFL OD PARA 50 M</li></ul> | [Plataforma de dados do cliente em tempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:ATIVAÇÃO DE OD</li><li>AEP:OD ACTIVATION PRFL TO 10M</li><li>AEP:OD ACTIVATION PRFL DE ATÉ 50 M</li></ul> | [Adobe Experience Platform Ativation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELIGÊNCIA DE OD</li></ul> | [Inteligência Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## Próximas etapas

Após ler este documento, é possível localizar o painel de uso da licença e selecionar uma sandbox para exibir. Você também pode encontrar mais informações sobre as métricas disponíveis para a sua organização, com base no licenciamento que sua organização adquiriu.

Para saber mais sobre outros recursos disponíveis na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário da plataforma](../../landing/ui-guide.md).

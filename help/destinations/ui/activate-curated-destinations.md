---
title: Ativar públicos para destinos com curadoria com base em identificadores do LiveRamp
type: Tutorial
description: Saiba como ativar públicos do Adobe Experience Platform para destinos de TV e áudio conectados e outras integrações usando o LiveRamp Ramp ID.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Ativar públicos para destinos com curadoria com base em identificadores do LiveRamp

Use a integração do Adobe Real-Time CDP com o [!DNL LiveRamp] para ativar públicos-alvo para uma lista com curadoria de destinos que usam o [[!DNL [LiveRamp RampID]]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) para ativação, incluindo destinos de áudio e TV conectados, como os listados abaixo.

>[!IMPORTANT]
>
>Não é necessário assimilar ou trabalhar de alguma forma com LiveRamp RampIDs na interface do Experience Platform.
>
> Você pode exportar identidades do Real-Time CDP, como identificadores baseados em PII, identificadores conhecidos e IDs personalizadas, conforme descrito na [documentação oficial do LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). Essas identidades são correspondidas com [!DNL LiveRamp RampIDs] downstream adicional no processo de ativação.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

Este artigo explica o fluxo de trabalho necessário para ativar públicos-alvo do Real-Time CDP para os destinos listados acima, diretamente da interface do usuário do Real-Time CDP.

## Fluxo de trabalho de ativação {#workflow}

Você ativa públicos para destinos de TV e áudio conectados por meio de um processo de duas etapas e usando os destinos [LiveRamp - Integração](../catalog/advertising/liveramp-onboarding.md) e [LiveRamp - Distribuição](../catalog/advertising/liveramp-distribution.md), conforme mostrado na imagem abaixo.

![Diagrama que mostra o fluxo de trabalho para ativar públicos do Real-Time CDP para destinos preparados, por meio do LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Primeiro, exporte os públicos-alvo do Real-Time CDP para o destino [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md), como arquivos CSV.

Após exportar os públicos, ative-os usando o destino [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!TIP]
>
>Esse processo permite ativar os públicos para destinos como [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) e muito mais, diretamente da interface do usuário do Real-Time CDP, sem a necessidade de fazer logon na sua conta do [!DNL LiveRamp] para ativação.

### Tutorial em vídeo {#video}

Assista ao vídeo abaixo para obter uma explicação completa do fluxo de trabalho descrito nesta página.

>[!VIDEO](https://video.tv.adobe.com/v/3452662?captions=por_br)

### Etapa 1: enviar seus públicos do Experience Platform para o LiveRamp, por meio do destino [!DNL LiveRamp - Onboarding] {#onboarding}

A primeira coisa que você deve fazer para ativar seus públicos para destinos com curadoria com base em LiveRampIDs é **exportar seus públicos do Experience Platform para o[!DNL LiveRamp]**.

Você faz isso usando o destino **[!DNL LiveRamp - Onboarding]**.

![Imagem da interface do Experience Platform mostrando o LiveRamp - Cartão de destino de integração](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Para saber como configurar o destino [!DNL LiveRamp - Onboarding] e exportar seus públicos do Experience Platform, leia a documentação de destino [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md).

>[!IMPORTANT]
>
>Ao exportar arquivos para o destino [!DNL LiveRamp - Onboarding], o Experience Platform gera um arquivo CSV para cada [ID da política de mesclagem](../../profile/merge-policies/overview.md). Consulte a documentação de destino do [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) para obter informações detalhadas sobre como validar a exportação de dados para o LiveRamp.


Depois de exportar os públicos para o LiveRamp com êxito, continue para a [etapa 2](#distribution).

>[!TIP]
>
>Antes de migrar para a [etapa 2](#distribution), [valide](../catalog/advertising/liveramp-onboarding.md#exported-data) que seus públicos-alvo foram exportados com êxito para o LiveRamp. Consulte a documentação sobre [monitoramento de fluxos de dados de destino](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e leia sobre os detalhes de monitoramento específicos para [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Etapa 2: ative os públicos integrados para destinos de TV e áudio conectados, por meio do destino [!DNL LiveRamp - Distribution] {#distribution}

Depois que você [validou](../catalog/advertising/liveramp-onboarding.md#exported-data) que seus públicos-alvo foram exportados com êxito para o LiveRamp, é hora de ativar os públicos-alvo para seus destinos preferidos, como [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) e muito mais.

Você ativa os públicos (exportados em [etapa 1](#onboarding)) usando o destino **[!DNL LiveRamp - Distribution]**.

![Imagem da interface do Experience Platform mostrando o LiveRamp - Cartão de destino de distribuição](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Para saber como configurar o destino **[!DNL LiveRamp - Distribution]** e ativar os públicos exportados na [etapa 1](#onboarding), leia a documentação de destino [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!IMPORTANT]
>
>Na etapa **seleção de público** do destino **[!DNL LiveRamp - Distribution]**, você deve selecionar os *mesmos públicos* que você exportou para o destino [LiveRamp - Integração](../catalog/advertising/liveramp-onboarding.md) na [etapa 1](#onboarding).

Ao configurar o destino **[!DNL LiveRamp - Distribution]**, você deve criar uma conexão dedicada para cada destino downstream que deseja usar (Roku, Disney e assim por diante).

>[!TIP]
>
>Ao nomear seu destino, a Adobe recomenda este formato: `LiveRamp - Downstream Destination Name`. Este padrão de nomenclatura ajuda a identificar rapidamente seus destinos na guia [Procurar](../ui/destinations-workspace.md#browse) do espaço de trabalho de destinos.
><br>
>Exemplo: `LiveRamp - Roku`.

![Captura de tela da interface do usuário do Experience Platform mostrando vários destinos do LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Para validar a exportação bem-sucedida dos seus públicos-alvo para o destino [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md), consulte a documentação em [fluxos de dados de destino de monitoramento](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e leia sobre os detalhes de monitoramento específicos para [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Para validar a ativação bem-sucedida dos públicos-alvo para a plataforma de publicidade escolhida (como Roku, Disney e outros), faça logon na conta da plataforma de destino e verifique as métricas de ativação.

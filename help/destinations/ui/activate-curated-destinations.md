---
title: Ativar públicos para destinos com curadoria com base em identificadores do LiveRamp
type: Tutorial
description: Saiba como ativar públicos do Adobe Experience Platform para destinos de TV e áudio conectados e outras integrações usando o LiveRamp Ramp ID.
source-git-commit: 25cda72508860b57bfa9ad0a729d0329d0f6bd1f
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---


# Ativar públicos para destinos com curadoria com base em identificadores do LiveRamp

Use a integração do Adobe Real-Time CDP com [!DNL LiveRamp] para ativar públicos-alvo para uma lista selecionada de destinos que usam [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) para ativação, incluindo destinos de TV e áudio conectados, como os listados abaixo.

>[!IMPORTANT]
>
>Você não precisa assimilar ou trabalhar de alguma forma com LiveRamp RampIDs na interface do Experience Platform.
>
> Você pode exportar identidades do Real-Time CDP, como identificadores baseados em PII, identificadores conhecidos e IDs personalizadas, conforme descrito no [Documentação do LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). Essas identidades são então combinadas com [!DNL LiveRamp RampIDs] mais downstream no processo de ativação.


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

Ative públicos para destinos de áudio e TV conectados por meio de um processo de duas etapas e usando o [LiveRamp - Integração](../catalog/advertising/liveramp-onboarding.md) e a variável [LiveRamp - Distribuição](../catalog/advertising/liveramp-distribution.md) destinos, conforme mostrado na imagem abaixo.

![Diagrama que mostra o fluxo de trabalho para ativar públicos do Real-Time CDP para destinos preparados, por meio do LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Primeiro, exporte os públicos-alvo do Real-Time CDP para o [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) destino, como arquivos CSV.

Após exportar os públicos, ative-os usando o [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) destino.

>[!TIP]
>
>Esse processo permite ativar os públicos para destinos como [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)e muito mais, diretamente da interface do usuário do Real-Time CDP, sem a necessidade de fazer logon no [!DNL LiveRamp] conta para ativação.

### Etapa 1: enviar seus públicos-alvo do Experience Platform para o LiveRamp, por meio do [!DNL LiveRamp - Onboarding] destino {#onboarding}

A primeira coisa que você deve fazer para ativar seus públicos para destinos com curadoria com base em LiveRamp RampIDs é: **exportar os públicos do Experience Platform para o[!DNL LiveRamp]**.

Para fazer isso, use o **[!DNL LiveRamp - Onboarding]** destino.

![Imagem da interface do Experience Platform mostrando o LiveRamp - Cartão de destino de integração](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Para saber como configurar o [!DNL LiveRamp - Onboarding] destino e exporte seus públicos do Experience Platform, leia o [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) documentação de destino.

>[!IMPORTANT]
>
>Ao exportar arquivos para o [!DNL LiveRamp - Onboarding] destino, a Platform gera um arquivo CSV para cada [ID da política de mesclagem](../../profile/merge-policies/overview.md). Consulte a [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) documentação de destino para obter informações detalhadas sobre como validar sua exportação de dados para o LiveRamp.


Depois de exportar os públicos-alvo para o LiveRamp com êxito, continue para [etapa 2](#distribution).

>[!TIP]
>
>Antes de mover para [etapa 2](#distribution), [validar](../catalog/advertising/liveramp-onboarding.md#exported-data) que seus públicos-alvo foram exportados com sucesso para o LiveRamp. Consulte a documentação em [monitoramento de fluxos de dados de destino](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e leia sobre os detalhes de monitoramento específicos do [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Etapa 2: ative os públicos integrados para destinos de TV e áudio conectados, por meio da [!DNL LiveRamp - Distribution] destino {#distribution}

Depois de ter [validado](../catalog/advertising/liveramp-onboarding.md#exported-data) que seus públicos-alvo foram exportados com sucesso para o LiveRamp, é hora de ativar os públicos-alvo para seus destinos preferidos, como [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)e muito mais.

Você ativa os públicos-alvo (exportados no [etapa 1](#onboarding)) usando o **[!DNL LiveRamp - Distribution]** destino.

![Imagem da interface do Experience Platform mostrando o LiveRamp - Cartão de destino de distribuição](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Para saber como configurar o **[!DNL LiveRamp - Distribution]** destino e ativar os públicos-alvo exportados no [etapa 1](#onboarding), leia o [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) documentação de destino.

>[!IMPORTANT]
>
>No **seleção de público** etapa do **[!DNL LiveRamp - Distribution]** destino, você deve selecionar o *exatamente os mesmos públicos* que você exportou para o [LiveRamp - Integração](../catalog/advertising/liveramp-onboarding.md) destino em [etapa 1](#onboarding).

Ao configurar o **[!DNL LiveRamp - Distribution]** , você deve criar uma conexão dedicada para cada destino downstream que deseja usar (Roku, Disney e assim por diante).

>[!TIP]
>
>Ao nomear seu destino, o Adobe recomenda seguir este formato: `LiveRamp - Downstream Destination Name`. Esse padrão de nomenclatura ajuda a identificar rapidamente os destinos na [Procurar](../ui/destinations-workspace.md#browse) do espaço de trabalho de destinos.
><br>
>Exemplo: `LiveRamp - Roku`.

![Captura de tela da interface do usuário da plataforma mostrando vários destinos do LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Para validar o sucesso da exportação de seus públicos-alvo para a [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) destino, consulte a documentação em [monitoramento de fluxos de dados de destino](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) e leia sobre os detalhes de monitoramento específicos do [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Para validar a ativação bem-sucedida dos públicos-alvo para a plataforma de publicidade escolhida (como Roku, Disney e outros), faça logon na conta da plataforma de destino e verifique as métricas de ativação.

---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: Visão geral dos destinos
seo-title: Visão geral dos destinos
description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Plataforma de dados do cliente em tempo real. Você pode usar Destinos na Plataforma de dados do cliente em tempo real do Adobe para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, anúncios direcionados e muitos outros casos de uso.
seo-description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Plataforma de dados do cliente em tempo real. Você pode usar Destinos na Plataforma de dados do cliente em tempo real do Adobe para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, anúncios direcionados e muitos outros casos de uso.
translation-type: tm+mt
source-git-commit: 54df4778a025811504801306120bda78e04281c1
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# [!DNL Destinations]visão geral{#overview}

![Banner de visão geral de destinos](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**[!DNL Destinations]** são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Plataforma de dados do cliente em tempo real. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

## Destinos e fontes {#destinations-and-sources}

Uma das principais funcionalidades da CDP em tempo real é assimilar seus dados primários e ativá-los de acordo com suas necessidades comerciais. Use fontes para assimilar dados em CDP em tempo real e destinos para exportar dados de CDP em tempo real.

## Etapas de destinos {#steps}

* Escolha em um catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) autoatendimento de todos os destinos disponíveis no CDP em tempo real.
* Use **[!UICONTROL Destinos]** para [ativar](/help/rtcdp/destinations/activate-destinations.md) e enviar perfis ou segmentos para plataformas de automação de marketing, plataformas de publicidade digital e muito mais.
* Agende exportações de dados para seus destinos preferenciais em horários regulares.

## Controles {#controls}

Os controles no espaço de trabalho [](/help/rtcdp/destinations/destinations-workspace.md) Destinos permitem:

* Navegue pelo catálogo de plataformas de destino onde você pode ativar seus dados;
* Criar, editar, ativar e desativar fluxos de dados para os destinos no catálogo;
* Criar uma conta em um local de armazenamento ou vincular o CDP em tempo real à conta na plataforma de destino;
* Selecionar quais segmentos devem ser ativados para destinos;
* Selecione quais campos [do Modelo de Dados de](../../xdm/home.md) Experiência (XDM) serão exportados ao ativar segmentos para destinos de marketing de email.

## Destination types and categories {#types-and-categories}

Para obter informações detalhadas, consulte os tipos de [destino e a visão geral](/help/rtcdp/destinations/destination-types.md)do categoria.

## Destinos e Controles de acesso {#access-controls}

A funcionalidade de destinos em CDP em tempo real funciona com permissões de controle de acesso Adobe Experience Platform. Dependendo do nível de permissão do usuário, você pode visualização, gerenciar e ativar destinos. Para obter informações sobre as permissões individuais, consulte [Controle de acesso no Adobe Experience Platform](../../access-control/home.md) e role até a parte inferior da página.

Para obter mais informações sobre controles de acesso, consulte o guia [do usuário do](../../access-control/ui/overview.md)Controle de acesso.

## [!DNL Data Governance] restrições na ativação de dados para destinos {#data-governance}

O controle de dados é aplicado para destinos de CDP em tempo real por meio de:

* *Casos* de uso de marketing que podem ser selecionados no fluxo de trabalho de criação de destinos;
* *Políticas* de uso de dados que restringem a ativação de determinados rótulos de uso para destinos com determinados casos de uso de marketing.

Consulte a documentação CDP em tempo real [!DNL Data Governance] para obter mais informações sobre casos [de uso de](/help/rtcdp/privacy/data-governance-overview.md#destinations) marketing e [resolver violações](/help/rtcdp/privacy/data-governance-overview.md#enforcement)de política de dados.

Para obter mais informações sobre a seleção de casos de uso de marketing no fluxo de trabalho de criação de destino, consulte as seguintes páginas para os diferentes tipos de destino no CDP em tempo real:

* [Destinos de publicidade - Google Ad Manager ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [Destinos de publicidade - Google Ads](/help/rtcdp/destinations/google-ads-destination.md)
* [Destinos de publicidade - Google Display &amp; Video 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [Destinos de armazenamentos na nuvem](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [Destinos de marketing de email](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Destinos da rede social](/help/rtcdp/destinations/social-network-destinations-workflow.md)

Para obter mais informações sobre violações da política de dados no fluxo de trabalho da ativação de segmentos, consulte a etapa 7 em [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md).
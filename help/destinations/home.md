---
keywords: destinos;adobe experiência plataforma;plataforma;visão geral de destinos;ativar dados;ativar;
title: Visão geral dos destinos
seo-title: Visão geral dos destinos
description: Saiba como ativar os dados da Adobe Experience Platform para destinos para campanhas de marketing entre canais, emails, anúncios direcionados e muito mais.
seo-description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Adobe Experience Platform. Você pode usar Destinos no Adobe Experience Platform para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
translation-type: tm+mt
source-git-commit: fc0813b457f039c0f0fa965df2d1100170424d23
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---


# [!DNL Destinations]visão geral{#overview}

![Banner de visão geral de destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

## Destinos e origens {#destinations-and-sources}

Uma das principais funcionalidades da Plataforma é assimilar seus dados primários e ativá-los para atender às suas necessidades comerciais. Use fontes para assimilar dados na Plataforma e destinos para exportar dados da Plataforma.

## Etapas de destinos {#steps}

* Escolha a partir de um [catálogo de autoatendimento](./catalog/overview.md) de todos os destinos disponíveis na Plataforma.
* Use **[!UICONTROL Destinos]** para [ativar](./ui/activate-destinations.md) e envie perfis ou segmentos para plataformas de automação de marketing, plataformas de publicidade digital e muito mais.
* Agende exportações de dados para seus destinos preferenciais em horários regulares.

## Controles {#controls}

Os controles no espaço de trabalho [Destinos](./ui/destinations-workspace.md) permitem:

* Navegue pelo catálogo de plataformas de destino onde você pode ativar seus dados;
* Criar, editar, ativar e desativar fluxos de dados para os destinos no catálogo;
* Criar uma conta em um local de armazenamento ou vincular Plataforma à conta na plataforma de destino;
* Selecionar quais segmentos devem ser ativados para destinos;
* Selecione os campos [Modelo de Dados de Experiência (XDM)](../xdm/home.md) a exportar ao ativar segmentos para destinos de marketing de email.

## Tipos de destino e categorias {#types-and-categories}

Para obter informações detalhadas, consulte os [tipos de destino e a visão geral do categoria](./destination-types.md).

## Destinos e controles de acesso {#access-controls}

A funcionalidade de destinos no Platform funciona com permissões de controle de acesso Adobe Experience Platform. Dependendo do nível de permissão do usuário, você pode visualização, gerenciar e ativar destinos. Para obter informações sobre as permissões individuais, consulte [Controle de acesso no Adobe Experience Platform](../access-control/home.md) e role até a parte inferior da página.

Para obter mais informações sobre controles de acesso, consulte o [guia do usuário do Controle de acesso](../access-control/ui/overview.md).

## [!DNL Data Governance] restrições na ativação de dados para destinos  {#data-governance}

O controle de dados é aplicado para destinos da plataforma por meio de:

* *Casos de uso de marketing* que você pode selecionar no fluxo de trabalho de criação de destinos;
* *As* políticas de uso de dados que restringem a ativação de determinados rótulos de uso para destinos com determinados casos de uso de marketing.

Consulte [!DNL Data Governance] na documentação da plataforma para obter mais informações sobre [casos de uso de marketing](../data-governance/policies/overview.md) e [resolução de violações de política de dados](../data-governance/enforcement/auto-enforcement.md).

Para obter mais informações sobre a seleção de casos de uso de marketing no fluxo de trabalho de criação de destino, consulte as seguintes páginas para os diferentes tipos de destino na Plataforma:

* [Destinos de publicidade - Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [Destinos de publicidade - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinos de publicidade - Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [Destinos de armazenamentos na nuvem](./catalog/cloud-storage/workflow.md)
* [Destinos de marketing de email](./catalog/email-marketing/overview.md)
* [Destinos da rede social](./catalog/social/workflow.md)

Para obter mais informações sobre violações da política de dados no fluxo de trabalho da ativação de segmentos, consulte a etapa Revisar em [Ativar perfis e segmentos para um destino](./ui/activate-destinations.md#review).
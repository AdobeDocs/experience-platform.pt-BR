---
keywords: destinos; adobe experience platform; plataforma; visão geral de destinos; ativar dados; ativar;
title: Visão geral dos destinos
description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar Destinos na Adobe Experience Platform para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 944f307ecb4cf174c9f9818ded17546057f445e4
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# Visão geral do [!DNL Destinations] {#overview}

![Banner de visão geral dos destinos](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinos e fontes {#destinations-and-sources}

Uma das funcionalidades principais da Platform é assimilar seus dados primários e ativá-los para as necessidades de sua empresa. Use [fontes](../sources/home.md) para assimilar dados na plataforma e destinos para exportar dados da plataforma.

## Etapas de destinos {#steps}

* Escolha entre um [catálogo de autoatendimento](./catalog/overview.md) de todos os destinos disponíveis na Platform.
* Use destinos para enviar perfis ou segmentos para plataformas de automação de marketing, plataformas de publicidade digital e muito mais.
* Programe exportações de dados para seus destinos preferidos em momentos regulares.

## Controles {#controls}

Os controles no [Área de trabalho Destinos](./ui/destinations-workspace.md) permite:

* Navegue pelo catálogo de plataformas de destino, onde você pode ativar seus dados;
* Criar, editar, ativar e desativar fluxos de dados para os destinos no catálogo;
* Crie uma conta em um local de armazenamento ou vincule a Plataforma à conta na plataforma de destino;
* Selecione quais segmentos devem ser ativados para destinos;
* Selecione qual [Campos do Experience Data Model (XDM)](../xdm/home.md) para exportar ao ativar segmentos para destinos de marketing por email.

## Tipos e categorias de destino {#types-and-categories}

Para obter informações detalhadas, consulte o [visão geral de tipos e categorias de destino](./destination-types.md).

## Destinos e controles de acesso {#access-controls}

A funcionalidade Destinos no Platform funciona com permissões de controle de acesso do Adobe Experience Platform. Dependendo do nível de permissão do usuário, você pode visualizar, gerenciar e ativar destinos. Para obter informações sobre permissões individuais, consulte [Controle de acesso no Adobe Experience Platform](../access-control/home.md) e role para baixo até a parte inferior da página.

A tabela a seguir descreve as combinações de permissões e permissões necessárias para executar determinadas ações em destinos:

| Nível de permissão | Descrição |
| ---- | ----|
| **[!UICONTROL Gerenciar destinos]** | Para se conectar a destinos, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** | Para ativar segmentos para destinos, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). |

{style=&quot;table-layout:auto&quot;}

Para obter mais informações sobre controles de acesso, consulte [Guia do usuário de controle de acesso](../access-control/ui/overview.md).

### Controle de acesso com base em atributos para destinos {#attribute-based-access}

O controle de acesso baseado em atributos no Adobe Experience Platform permite que os administradores controlem o acesso a objetos e/ou recursos específicos com base em atributos.

Com o controle de acesso baseado em atributos, você pode aplicar configurações de mapeamento a campos aos quais tem permissões. Além disso, não será possível exportar dados para um destino se você não tiver acesso a todos os campos no conjunto de dados.

Para obter mais informações sobre como os destinos funcionam com controles de acesso baseados em atributos, leia a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md#destinations).

## Restrições de governança de dados na ativação de dados para destinos {#data-governance}

O controle de dados é empregado para destinos da plataforma por meio de:

* *Ações de marketing* que você pode selecionar no workflow criar destinos ;
* *Políticas de uso de dados* que restringem a ativação de dados contendo determinados rótulos de uso a destinos com determinadas ações de marketing.

Consulte a documentação Governança de dados na plataforma para obter mais informações sobre [ações de marketing](../data-governance/policies/overview.md) e [resolução de violações da política de dados](../data-governance/enforcement/auto-enforcement.md).

Para obter mais informações sobre a seleção de ações de marketing no workflow criar destino, consulte as seguintes páginas para os diferentes tipos de destino na Platform:

* [Destinos de publicidade - Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [Destinos de publicidade - Anúncios Google](./catalog/advertising/google-ads-destination.md)
* [Destinos de publicidade - Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [Destinos de armazenamento na nuvem](./catalog/cloud-storage/overview.md)
* [Destinos de marketing por email](./catalog/email-marketing/overview.md)
* [Destinos sociais](./catalog/social/overview.md)

Para obter mais informações sobre violações da política de dados no fluxo de trabalho de ativação de segmento, consulte o **[!UICONTROL Revisão]** nos seguintes guias:

* [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](./ui/activate-segment-streaming-destinations.md#review)
* [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](./ui/activate-streaming-profile-destinations.md#review)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](./ui/activate-batch-profile-destinations.md#review)

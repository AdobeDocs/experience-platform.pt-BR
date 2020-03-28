---
title: Visão geral dos destinos
seo-title: Visão geral dos destinos
description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Plataforma de dados do cliente em tempo real. Você pode usar Destinos na Plataforma de dados do cliente em tempo real da Adobe para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, anúncios direcionados e muitos outros casos de uso.
seo-description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados da Plataforma de dados do cliente em tempo real. Você pode usar Destinos na Plataforma de dados do cliente em tempo real da Adobe para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, anúncios direcionados e muitos outros casos de uso.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Visão geral dos destinos

![Banner de visão geral de destinos](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**Os destinos** são integrações pré-criadas com plataformas de destino que permitem a ativação contínua dos dados da Plataforma de dados do cliente em tempo real. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, publicidade direcionada e muitos outros casos de uso.

## Destinos e fontes

Uma das principais funcionalidades da CDP em tempo real é assimilar seus dados primários e ativá-los de acordo com suas necessidades comerciais. Use fontes para assimilar dados em CDP em tempo real e destinos para exportar dados de CDP em tempo real.

## Etapas de destinos

* Escolha em um catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) autoatendimento de todos os destinos disponíveis no CDP em tempo real.
* Use **[!UICONTROL Destinations]** para [ativar](/help/rtcdp/destinations/activate-destinations.md) e enviar perfis ou segmentos para plataformas de automação de marketing, plataformas de publicidade digital e muito mais.
* Agende exportações de dados para seus destinos preferenciais em horários regulares.

## Controles

Os controles no espaço de trabalho [](/help/rtcdp/destinations/destinations-workspace.md) Destinos permitem:

* Navegue pelo catálogo de plataformas de destino onde você pode ativar seus dados;
* Criar, editar, ativar e desativar fluxos de dados para os destinos no catálogo;
* Criar uma conta em um local de armazenamento ou vincular o CDP em tempo real à conta na plataforma de destino;
* Selecionar quais segmentos devem ser ativados para destinos;
* Selecione quais campos [do Modelo de Dados de](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/xdm_system/xdm_system_in_experience_platform.md) Experiência (XDM) serão exportados ao ativar segmentos para destinos de marketing de email.

## Tipos de destino e categorias - visão geral do vídeo

No CDP em tempo real da Adobe, há dois tipos de destinos, Exportar Perfis e Exportar segmentos. O vídeo abaixo descreve os dois tipos de destinos.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Destinos de exportação do Perfil

Os destinos de exportação de Perfil geram um arquivo que contém perfis e/ou atributos. Esses destinos usam dados brutos, geralmente com endereço de email como a chave primária.

### Destinos de exportação do segmento

Os destinos de exportação do segmento enviam os perfis e os segmentos para os quais eles se qualificaram. Esses destinos usam IDs de segmento ou IDs de usuário.

### categorias de destino

Os destinos no catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) Destinos são agrupados por categoria de destino (**Publicidade**, armazenamento **da** Cloud ou marketing **de** email). Para obter mais informações sobre cada um deles, consulte o catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)Destinos.

## Destinos e Controles de acesso

A funcionalidade de destinos em CDP em tempo real funciona com permissões de controle de acesso da plataforma Adobe Experience. Dependendo do nível de permissão do usuário, você pode visualização, gerenciar e ativar destinos. Para obter informações sobre as permissões individuais, consulte [Controle de acesso na Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) e role até a parte inferior da página.

Para obter mais informações sobre controles de acesso, consulte o guia [do usuário do](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md)Controle de acesso.
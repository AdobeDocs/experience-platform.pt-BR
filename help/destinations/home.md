---
title: Visão geral dos destinos
description: Os destinos são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar Destinos na Adobe Experience Platform para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 6dd6190f1b006ffb3346eea6dc917ce52e0aa1c6
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 4%

---

# Visão geral do [!DNL Destinations] {#overview}

![Banner da visão geral dos destinos.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## Destinos e origens {#destinations-and-sources}

Uma das funcionalidades principais da Platform é assimilar seus dados primários e ativá-los para atender às suas necessidades comerciais. Use [fontes](../sources/home.md) para assimilar dados na Platform e destinos para exportar dados da Platform.

## Etapas de destinos {#steps}

* Escolha em um [catálogo de autoatendimento](./catalog/overview.md) de todos os destinos disponíveis na Platform.
* Use destinos para enviar públicos ou conjuntos de dados para plataformas de automação de marketing, plataformas de publicidade digital e muito mais.
* Agende exportações de dados para seus destinos preferidos regularmente.

## Controles {#controls}

Os controles no [espaço de trabalho de destinos](./ui/destinations-workspace.md) permitem:

* Navegue pelo catálogo de plataformas de destino onde você pode ativar seus dados;
* Criar, editar, ativar e desativar fluxos de dados para os destinos no catálogo;
* Criar uma conta em um local de armazenamento ou vincular a Platform à conta na plataforma de destino;
* Selecione quais públicos ou conjuntos de dados devem ser ativados para destinos;
* Selecione quais [campos do Experience Data Model (XDM)](../xdm/home.md) serão exportados quando os públicos-alvo forem ativados para determinados destinos, como destinos de marketing por email, plataformas CRM, locais de armazenamento na nuvem e muito mais.
* Ative diferentes tipos de perfis e públicos para destinos - pessoas, contas e clientes potenciais.

## Tipos e categorias de destino {#types-and-categories}

Com o Experience Platform, você pode ativar dados para vários tipos de destinos para atender aos casos de uso de ativação. Os destinos variam de integrações baseadas em API a integrações com sistemas de recepção de arquivos, destinos de pesquisa de perfil e muito mais. Para obter informações detalhadas sobre todos os destinos disponíveis, leia a [visão geral sobre tipos e categorias de destino](./destination-types.md).

## Destinos criados pelo Adobe e por parceiros {#adobe-and-partner-built-destinations}

Alguns dos conectores no catálogo de destinos de Experience Platform são criados e mantidos pelo Adobe, enquanto outros são criados e mantidos por empresas parceiras usando o [Destination SDK](/help/destinations/destination-sdk/overview.md). Uma observação na parte superior da página de documentação para cada conector criado pelo parceiro chama se um destino é criado e mantido pelo parceiro. Por exemplo, o [conector Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) é criado pelo Adobe, enquanto o [conector TikTok](/help/destinations/catalog/social/tiktok.md) é criado e mantido pela equipe do TikTok.

Para conectores criados e mantidos pelo parceiro, isso significa que os problemas com o conector podem precisar ser resolvidos pela equipe do parceiro (método de contato fornecido na observação na página de documentação). No caso de problemas com conectores criados e mantidos pelo Adobe, entre em contato com o representante da Adobe ou com o Atendimento ao cliente.

## Destinos e controles de acesso {#access-controls}

A funcionalidade de destinos na Platform funciona com permissões de controle de acesso do Adobe Experience Platform. Dependendo do nível de permissão do seu usuário, você pode visualizar, gerenciar e ativar destinos. Para obter informações sobre as permissões individuais, vá para [controle de acesso no Adobe Experience Platform](../access-control/home.md) e role para baixo até a tabela na parte inferior da página.

A tabela a seguir descreve as permissões e as combinações de permissões necessárias para executar determinadas ações nos destinos.

| Nível de permissão | Descrição |
| ---- | ---- |
| **[!UICONTROL Exibir Destinos]** | Para acessar a guia de destinos na interface do usuário do Experience Platform, você precisa da **[!UICONTROL permissão de controle de acesso](/help/access-control/home.md#permissions) para [Exibir Destinos]**. |
| **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Gerenciar Destinos]** | Para se conectar a destinos, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** | Para ativar públicos para destinos e habilitar a [etapa de mapeamento](ui/activate-batch-profile-destinations.md#mapping) do fluxo de trabalho, você precisa das **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar segmentos sem mapeamento]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** | Para adicionar ou remover públicos-alvo de fluxos de dados existentes sem ter acesso à [etapa de mapeamento](ui/activate-batch-profile-destinations.md#mapping) do fluxo de trabalho, você precisa das **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Segmentos sem Mapeamento]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Gerenciar e Ativar Destinos do Conjunto de Dados]** | Para exportar conjuntos de dados para destinos, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar e Ativar Destinos de Conjuntos de Dados]** [permissões de controle de acesso](/help/access-control/home.md#permissions). |
| **[!UICONTROL Exibir Gráfico De Identidade]** | Para exportar *identidades* para destinos, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

O diagrama abaixo exibe visualmente quais permissões são necessárias, dependendo das operações que você deseja executar nos destinos.

![Diagrama que mostra as permissões necessárias para executar determinadas ações nos destinos.](/help/destinations/assets/overview/permissions-diagram.png)

Para obter mais informações sobre controles de acesso, consulte o [Guia do usuário de controle de acesso](../access-control/ui/overview.md).

### Controle de acesso baseado em atributos para destinos {#attribute-based-access}

O controle de acesso baseado em atributos no Adobe Experience Platform permite que os administradores controlem o acesso a objetos e/ou recursos específicos com base em atributos.

Com o controle de acesso baseado em atributos, é possível aplicar configurações de mapeamento a campos aos quais você tem permissões. Além disso, não é possível exportar dados para um destino se você não tiver acesso a todos os campos no conjunto de dados.

Para obter mais informações sobre como os destinos funcionam com os controles de acesso baseados em atributos, leia a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md#destinations).

## Monitoramento de destinos {#destinations-monitoring}

Depois de estabelecer uma conexão com um destino e concluir o fluxo de trabalho de ativação, é possível monitorar as exportações de dados para o sistema de recebimento. Leia o [guia sobre monitoramento de fluxos de dados para destinos na interface](/help/dataflows/ui/monitor-destinations.md) para obter mais informações.

![Exemplo da página de monitoramento de destinos.](./assets/overview/monitoring-page-example.png)

Você também pode validar se os dados estão chegando com êxito ao seu destino. A maioria das páginas de documentação de destino no catálogo tem uma *seção Validar exportação de dados*, que indica como você pode verificar na plataforma de destino se os dados estão sendo trazidos com êxito do Experience Platform. Veja um exemplo desta seção para o [destino do Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md#exported-data).

## Restrições de governança de dados na ativação de dados para destinos {#data-governance}

A governança de dados é imposta para destinos da Platform por meio de:

* *Ações de marketing* que você pode selecionar no fluxo de trabalho criar destinos;
* *Políticas de uso de dados* que restringem a ativação de dados contendo determinados rótulos de uso para destinos com determinadas ações de marketing.

Consulte a Documentação de Governança de dados na plataforma para obter mais informações sobre [ações de marketing](../data-governance/policies/overview.md) e [resolução de violações de política de dados](../data-governance/enforcement/auto-enforcement.md).

Para obter mais informações sobre como selecionar ações de marketing no fluxo de trabalho de criação de destino, consulte as seguintes páginas para os diferentes tipos de destino na Platform:

* [Destinos do Advertising - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Destinos do Advertising - Google Ads](./catalog/advertising/google-ads-destination.md)
* [Destinos do Advertising - Google Display &amp; Video 360](./catalog/advertising/google-dv360.md)
* [Destinos de armazenamento na nuvem](./catalog/cloud-storage/overview.md)
* [Destinos de marketing por email](./catalog/email-marketing/overview.md)
* [Destinos sociais](./catalog/social/overview.md)

Para obter mais informações sobre violações de política de dados no fluxo de trabalho de ativação de público, consulte a etapa **[!UICONTROL Revisão]** dos guias a seguir:

* [Ativar dados do público-alvo para streaming de públicos-alvo exportar destinos](./ui/activate-segment-streaming-destinations.md#review)
* [Ativar dados do público-alvo para destinos de exportação de perfil de transmissão](./ui/activate-streaming-profile-destinations.md#review)
* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](./ui/activate-batch-profile-destinations.md#review)

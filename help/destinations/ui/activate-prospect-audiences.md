---
title: Ativar públicos-alvo potenciais para destinos
type: Tutorial
description: Saiba como ativar públicos-alvo potenciais para destinos
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 14%

---

# Ativar públicos-alvo potenciais

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o pacote Real-Time CDP Prime e Ultimate. Entre em contato com o representante da Adobe para obter mais informações.

Este artigo explica o fluxo de trabalho necessário para exportar [públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) do Adobe Experience Platform para o seu destino preferido.

## Destinos compatíveis {#supported-destinations}

Vá para **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** e selecione a guia **[!UICONTROL Catalog]**. Use o filtro **[!UICONTROL Data types]** e selecione **[!UICONTROL Prospects]** para ver os destinos que oferecem suporte à ativação de públicos-alvo em potencial. Atualmente, a exportação de públicos-alvo potenciais está disponível somente para destinos de armazenamento em nuvem.

![Destinos que oferecem suporte a públicos-alvo em potencial.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Pré-requisitos {#prerequisites}

* Você deve primeiro assimilar [perfis de clientes potenciais](/help/profile/ui/prospect-profile.md) e criar [públicos-alvo de clientes potenciais](/help/segmentation/types/prospect-audiences.md) antes de ativá-los em destinos downstream.
* Para ativar públicos-alvo de prospecto para destinos, você deve ter se conectado com êxito a um destino. Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar. Leia o tutorial da interface do usuário em [conexão com destinos](./connect-destination.md) para obter mais informações.

### Permissões necessárias {#permissions}

Para ativar públicos-alvo de clientes potenciais, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Activate Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para garantir que você tenha as permissões necessárias para ativar públicos-alvo de prospecto, navegue pelo catálogo de destinos. Se um destino tiver um controle **[!UICONTROL Activate]**, você terá as permissões apropriadas.

## Selecione seu destino {#select-destination}

Siga as instruções para selecionar um destino em que você possa exportar seus conjuntos de dados:

1. Vá para **[!UICONTROL Connections > Destinations]** e selecione a guia **[!UICONTROL Catalog]**.

   ![Guia de catálogo de destino com controle de catálogo realçado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Selecione **[!UICONTROL Activate]** no cartão correspondente ao destino para o qual você deseja exportar conjuntos de dados.

>[!TIP]
>
>Os destinos que podem exportar públicos-alvo de perfil são indicados com um ícone no canto superior direito do cartão, semelhante ao destino destacado abaixo, ou você pode usar o filtro de tipo de dados para exibir apenas destinos que podem exportar públicos-alvo potenciais, como [mostrado mais alto na página](#supported-destinations).

![Página de destino do Amazon S3 que pode exportar públicos-alvo de perfil realçada.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Selecione **[!UICONTROL Data type Prospects]**, seguido da conexão de destino para a qual você deseja exportar conjuntos de dados e selecione **[!UICONTROL Next]**.

>[!TIP]
> 
>Se quiser configurar um novo destino para ativar públicos-alvo de clientes potenciais, selecione **[!UICONTROL Configure new destination]** para acionar o fluxo de trabalho [Conectar ao destino](/help/destinations/ui/connect-destination.md).

![Fluxo de trabalho de ativação de destino com controle de Clientes Potenciais realçado.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Prossiga para a próxima seção para [selecionar os públicos do seu perfil](#select-profile-audiences) para exportação.

## Selecione os públicos-alvo de clientes potenciais {#select-prospect-audiences}

Use as caixas de seleção à esquerda dos nomes dos públicos-alvo de clientes potenciais para selecionar os públicos que deseja exportar para o destino e selecione **[!UICONTROL Next]**. Observe que somente os públicos-alvo potenciais são mostrados nessa visualização e nenhum outro público-alvo é exibido.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa Selecionar públicos-alvo, na qual você pode selecionar quais públicos-alvo potenciais serão exportados.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Programação e próximas etapas

No restante do fluxo de trabalho de ativação para exportar públicos-alvo de prospecto, leia o tutorial sobre a ativação de dados para destinos baseados em arquivo. Continue na [etapa de exportação de público-alvo de agendamento](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Observe que na etapa de agendamento, o fluxo de trabalho para ativar públicos-alvo potenciais permite apenas [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Não há suporte para exportações de arquivos incrementais.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* [Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Use o suporte a dados de terceiros da Real-Time CDP para [expandir sua base de perfis com perfis de clientes potenciais de parceiros de dados e interaja com eles para adquirir ou alcançar novos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Aproveite o reconhecimento auxiliado pelo parceiro para personalizar experiências no site](/help/rtcdp/partner-data/onsite-personalization.md) durante a visita sem que o usuário autentique ou tenha um histórico anterior com sua marca.

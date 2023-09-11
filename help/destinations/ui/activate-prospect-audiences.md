---
title: Ativar públicos-alvo potenciais para destinos
type: Tutorial
description: Saiba como ativar públicos-alvo potenciais para destinos
source-git-commit: 384faa13154386ef2578da4c20ab47f171aefeda
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 12%

---


# Ativar públicos-alvo potenciais

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o pacote Real-Time CDP Prime e Ultimate. Entre em contato com o representante da Adobe para obter mais informações.

Este artigo explica o workflow necessário para exportar [públicos-alvo potenciais](/help/segmentation/ui/prospect-audience.md) do Adobe Experience Platform para o destino de sua preferência.

## Destinos compatíveis {#supported-destinations}

Ir para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia. Use o **[!UICONTROL Tipos de dados]** filtrar e selecionar **[!UICONTROL Clientes potenciais]** para ver os destinos que oferecem suporte à ativação de públicos-alvo de prospecto. Atualmente, a exportação de públicos-alvo potenciais está disponível somente para destinos de armazenamento em nuvem.

![Destinos que oferecem suporte a exportações de conjunto de dados](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## Pré-requisitos {#prerequisites}

* Você deve primeiro assimilar [perfis de cliente potencial](/help/profile/ui/prospect-profile.md) e criar [públicos-alvo potenciais](/help/segmentation/ui/prospect-audience.md) antes de poder ativá-los para destinos downstream.
* Para ativar públicos-alvo de prospecto para destinos, você deve ter se conectado com êxito a um destino. Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar. Leia o tutorial da interface do usuário no [conexão com destinos](./connect-destination.md) para obter mais informações.

### Permissões necessárias {#permissions}

Para ativar públicos-alvo potenciais, você precisa da **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para garantir que você tenha as permissões necessárias para ativar públicos-alvo de prospecto, navegue pelo catálogo de destinos. Se um destino tiver um **[!UICONTROL Ativar]** , você terá as permissões apropriadas.

## Selecione seu destino {#select-destination}

Siga as instruções para selecionar um destino em que você possa exportar seus conjuntos de dados:

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Guia Catálogo de destino com Controle de catálogo realçado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. Selecionar **[!UICONTROL Ativar]** no cartão correspondente ao destino para o qual você deseja exportar conjuntos de dados.

>[!TIP]
>
>Os destinos que podem exportar públicos-alvo de perfil são indicados com um ícone no canto superior direito do cartão, semelhante ao destino destacado abaixo, ou você pode usar o filtro de tipo de dados para exibir apenas destinos que podem exportar públicos-alvo potenciais, como [mostrado mais alto na página](#supported-destinations).

![Página de destino do Amazon S3 que pode exportar públicos-alvo de perfil realçada.](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. Selecionar **[!UICONTROL Tipo de dados Prospects]**, seguido pela conexão de destino para a qual você deseja exportar conjuntos de dados, e selecione **[!UICONTROL Próxima]**.

>[!TIP]
> 
>Se quiser configurar um novo destino para ativar públicos-alvo de prospecto, selecione **[!UICONTROL Configurar novo destino]** para acionar o [Conectar ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho.

![Fluxo de trabalho de ativação de destino com controle de clientes potenciais realçado.](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. Prossiga para a próxima seção até [selecionar os públicos do seu perfil](#select-profile-audiences) para exportação.

## Selecione os públicos-alvo de clientes potenciais {#select-prospect-audiences}

Use as caixas de seleção à esquerda dos nomes dos públicos-alvo potenciais para selecionar os públicos-alvo que deseja exportar para o destino e selecione **[!UICONTROL Próxima]**. Observe que somente os públicos-alvo potenciais são mostrados nessa visualização e nenhum outro público-alvo é exibido.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa Selecionar públicos-alvo, onde é possível selecionar quais públicos-alvo potenciais serão exportados.](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## Programação e próximas etapas

No restante do fluxo de trabalho de ativação para exportar públicos-alvo de prospecto, leia o tutorial sobre a ativação de dados para destinos baseados em arquivo. Continue na [agendar etapa de exportação de público](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>Observe que na etapa de agendamento, o fluxo de trabalho para ativar públicos-alvo potenciais permite apenas [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). Não há suporte para exportações de arquivos incrementais.

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* [Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Use o suporte a dados de terceiros da Real-Time CDP para [expandir sua base de perfis com prospectos de parceiros de dados e interaja com eles para adquirir ou alcançar novos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Aproveite o reconhecimento auxiliado pelo parceiro para personalizar experiências no local](/help/rtcdp/partner-data/onsite-personalization.md) durante a visita sem que o usuário autentique ou tenha um histórico anterior com sua marca.
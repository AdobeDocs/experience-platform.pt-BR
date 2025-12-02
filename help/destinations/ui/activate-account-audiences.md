---
title: Ativar públicos-alvo da conta para destinos
type: Tutorial
description: Saiba como ativar públicos-alvo da conta para destinos
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Ativar públicos-alvo da conta

>[!AVAILABILITY]
>
>A funcionalidade para ativar públicos da conta para destinos está disponível para empresas que compram as edições [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) do Real-Time Customer Data Platform.

Este artigo explica o fluxo de trabalho necessário para exportar [públicos-alvo da conta](/help/segmentation/types/account-audiences.md) do Adobe Experience Platform para o seu destino preferido.

## Destinos compatíveis {#supported-destinations}

Vá para **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** e selecione a guia **[!UICONTROL Catalog]**. Use o filtro **[!UICONTROL Data types]** e selecione **[!UICONTROL Accounts]** para ver os destinos que oferecem suporte à ativação de públicos-alvo de contas. Atualmente, a exportação de públicos-alvo de conta está disponível somente para determinados destinos de armazenamento em nuvem ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Armazenamento Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Zona de Aterrissagem de Dados](/help/destinations/catalog/cloud-storage/data-landing-zone.md) e [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) e o [Demandbase](/help/destinations/catalog/advertising/demandbase.md) e [(Empresas) LinkedIn Corresponderam públicos-alvo](/help/destinations/catalog/social/linkedin-b2b.md) de streaming.

![Destinos que oferecem suporte a públicos-alvo da conta.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Visão geral do vídeo

Assista ao vídeo abaixo para obter uma visão geral da criação e ativação de públicos-alvo de conta, e os casos de uso compatíveis ao ativar públicos-alvo de conta.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Pré-requisitos {#prerequisites}

* Você deve primeiro assimilar [perfis de conta](/help/rtcdp/accounts/account-profile-overview.md) e criar [públicos-alvo de conta](/help/segmentation/types/account-audiences.md) antes de ativá-los para destinos downstream.
* Para ativar públicos-alvo da conta para destinos, você deve ter se conectado com êxito a um destino. Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar. Leia o tutorial da interface do usuário em [conexão com destinos](./connect-destination.md) para obter mais informações.

### Permissões necessárias {#permissions}

Para ativar públicos da conta, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Activate Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para garantir que você tenha as permissões necessárias para ativar públicos-alvo da conta, navegue pelo catálogo de destinos. Se um destino tiver um controle **[!UICONTROL Activate]**, você terá as permissões apropriadas.

## Selecione seu destino {#select-destination}

Siga as instruções para selecionar um destino em que você possa exportar seus conjuntos de dados:

1. Vá para **[!UICONTROL Connections > Destinations]** e selecione a guia **[!UICONTROL Catalog]**.

   ![Guia de catálogo de destino com controle de catálogo realçado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecione **[!UICONTROL Activate]** no cartão correspondente ao destino para o qual você deseja exportar conjuntos de dados.

>[!TIP]
>
>Os destinos que podem exportar públicos da conta são indicados com um ícone no canto superior direito do cartão, semelhante ao destino destacado abaixo, ou você pode usar o filtro de tipo de dados para exibir apenas os destinos que podem exportar públicos da conta, como [mostrado mais alto na página](#supported-destinations).

![Página de destino do Demandbase que pode exportar públicos-alvo de perfil destacados.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Selecione **[!UICONTROL Data type Accounts]**, seguido da conexão de destino para a qual você deseja exportar conjuntos de dados e selecione **[!UICONTROL Next]**.

>[!TIP]
> 
>Se quiser configurar um novo destino para ativar públicos-alvo da conta, selecione **[!UICONTROL Configure new destination]** para acionar o fluxo de trabalho [Conectar ao destino](/help/destinations/ui/connect-destination.md) e [selecionar contas como tipo de dados](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Fluxo de trabalho de ativação de destino com controle de contas realçado.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Prossiga para a próxima seção para [selecionar os públicos-alvo da sua conta](#select-profile-audiences) para exportação.

## Selecione os públicos da sua conta {#select-account-audiences}

Use as caixas de seleção à esquerda dos nomes dos públicos-alvo da conta para selecionar os públicos-alvo que deseja exportar para o destino e selecione **[!UICONTROL Next]**. Observe que somente *públicos-alvo da conta* são mostrados nesta exibição, e nenhum outro tipo de público-alvo é exibido.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa Selecionar públicos-alvo, na qual você pode selecionar os públicos-alvo da conta a serem exportados.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Programação e próximas etapas

No restante do fluxo de trabalho de ativação para exportar públicos da conta, leia o tutorial sobre a ativação de dados para destinos baseados em arquivo. Continue na [etapa de exportação de público-alvo de agendamento](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Se você estiver ativando públicos da conta para o destino **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, leia o tutorial sobre ativação de destinos de streaming. Continue a partir da [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Observe que na etapa de agendamento ao exportar públicos-alvo da conta para destinos de armazenamento na nuvem, o fluxo de trabalho para ativar públicos-alvo da conta permite exportar apenas [arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _em um agendamento diário_. Não há suporte para exportações por hora. Observe também que **[!UICONTROL After audience evaluation]** é o único tipo de avaliação com suporte.

## Chamadas importantes e limitações conhecidas {#important-callouts-known-limitations}

Observe as importantes chamadas a seguir e as limitações conhecidas da versão de disponibilidade geral da funcionalidade para ativar públicos-alvo da conta.

### Pares de mapeamento necessários na etapa de mapeamento ao ativar públicos da conta para o destino **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Ao ativar públicos-alvo da conta para o destino **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, observe que os dois pares de mapeamento a seguir são obrigatórios para exportar dados com êxito:

![Campos obrigatórios de mapeamento do LinkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo de origem | Campo de destino |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecione este campo no modo de exibição **[!UICONTROL Select Identity namespace]** ao selecionar o **[!UICONTROL Target Field]**). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar os públicos-alvo da conta para os destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar os públicos-alvo da conta para destinos."){width="100" zoomable="yes"} |

### Imposição de governança de dados {#data-governance-enforcement}

O consentimento é aplicado no nível da pessoa ou do perfil para *públicos-alvo de clientes e prospetos*. Portanto, no momento, a [avaliação de política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) não tem suporte ao ativar públicos-alvo de conta para destinos. Na etapa de revisão do fluxo de trabalho de ativação, você pode ver um controle esmaecido para **[!UICONTROL View applicable consent policies]**.

![Etapa de revisão do fluxo de trabalho ativar públicos-alvo de conta com o controle de imposição de consentimento esmaecido.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Há suporte para outros mecanismos de governança de dados no Real-Time CDP, como [verificações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) e [controle de acesso baseado em atributos](/help/destinations/home.md#attribute-based-access).

---
title: Ativar públicos-alvo da conta para destinos
type: Tutorial
description: Saiba como ativar públicos-alvo da conta para destinos
badgeB2B: label="Edição B2B" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: f07eb12b4625bce117e1fe524727c00b7188aa5e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# Ativar públicos-alvo da conta

>[!AVAILABILITY]
>
>A funcionalidade para ativar públicos-alvo da conta para destinos está disponível para empresas que compram a [B2B](/help/rtcdp/overview.md#rtcdp-b2b) e [Negócio para pessoa](/help/rtcdp/overview.md#rtcdp-b2b) Real-time Customer Data Platform.

Este artigo explica o workflow necessário para exportar [públicos-alvo da conta](/help/segmentation/ui/account-audiences.md) do Adobe Experience Platform para o destino de sua preferência.

## Destinos compatíveis {#supported-destinations}

Ir para **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia. Use o **[!UICONTROL Tipos de dados]** filtrar e selecionar **[!UICONTROL Contas]** para ver os destinos que oferecem suporte à ativação de públicos-alvo da conta. Atualmente, a exportação de públicos-alvo da conta está disponível somente para determinados destinos de armazenamento em nuvem ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Ger 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Armazenamento Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), e [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) e o [(Empresas) Públicos-alvo correspondentes do LinkedIn](/help/destinations/catalog/social/linkedin.md) destino.

![Destinos que oferecem suporte a públicos-alvo da conta.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Pré-requisitos {#prerequisites}

* Você deve primeiro assimilar [perfis de conta](/help/rtcdp/accounts/account-profile-overview.md) e criar [públicos-alvo da conta](/help/segmentation/ui/account-audiences.md) antes de poder ativá-los para destinos downstream.
* Para ativar públicos-alvo da conta para destinos, você deve ter se conectado com êxito a um destino. Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar. Leia o tutorial da interface do usuário no [conexão com destinos](./connect-destination.md) para obter mais informações.

### Permissões necessárias {#permissions}

Para ativar públicos-alvo da conta, é necessário **[!UICONTROL Exibir destinos]** e **[!UICONTROL Ativar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para garantir que você tenha as permissões necessárias para ativar públicos-alvo da conta, navegue pelo catálogo de destinos. Se um destino tiver um **[!UICONTROL Ativar]** , você terá as permissões apropriadas.

## Selecione seu destino {#select-destination}

Siga as instruções para selecionar um destino em que você possa exportar seus conjuntos de dados:

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Guia Catálogo de destino com Controle de catálogo realçado.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar]** no cartão correspondente ao destino para o qual você deseja exportar conjuntos de dados.

>[!TIP]
>
>Os destinos que podem exportar públicos da conta são indicados com um ícone no canto superior direito do cartão, semelhante ao destino destacado abaixo, ou você pode usar o filtro de tipo de dados para exibir apenas os destinos que podem exportar públicos da conta, como [mostrado mais alto na página](#supported-destinations).

![Página de destino do Amazon S3 que pode exportar públicos-alvo de perfil realçada.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Selecionar **[!UICONTROL Contas do tipo de dados]**, seguido pela conexão de destino para a qual você deseja exportar conjuntos de dados, e selecione **[!UICONTROL Próxima]**.

>[!TIP]
> 
>Se quiser configurar um novo destino para ativar públicos-alvo da conta, selecione **[!UICONTROL Configurar novo destino]** para acionar o [Conectar ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho e [selecionar contas como tipo de dados](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Fluxo de trabalho de ativação de destino com controle de contas realçado.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Prossiga para a próxima seção até [selecione os públicos da sua conta](#select-profile-audiences) para exportação.

## Selecione os públicos da sua conta {#select-account-audiences}

Use as caixas de seleção à esquerda dos nomes dos públicos-alvo da conta para selecionar os públicos-alvo que deseja exportar para o destino e selecione **[!UICONTROL Próxima]**. Observe que somente *públicos-alvo da conta* são mostrados nessa visualização e nenhum outro tipo de público-alvo é exibido.

![Fluxo de trabalho de exportação do conjunto de dados mostrando a etapa Selecionar públicos-alvo, onde é possível selecionar quais públicos-alvo da conta serão exportados.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Programação e próximas etapas

No restante do fluxo de trabalho de ativação para exportar públicos da conta, leia o tutorial sobre a ativação de dados para destinos baseados em arquivo. Continue na [agendar etapa de exportação de público](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Se você estiver ativando públicos-alvo da conta para a variável **[!UICONTROL (Empresas) Públicos-alvo correspondentes do LinkedIn]** destino, leia o tutorial sobre ativação de destinos de transmissão. Continue na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Observe que na etapa de agendamento ao exportar públicos-alvo da conta para destinos de armazenamento na nuvem, o fluxo de trabalho para ativar públicos-alvo da conta permite apenas exportar [arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _em uma programação diária_. Não há suporte para exportações por hora. Observe também que **[!UICONTROL Após a avaliação do público-alvo]** é o único tipo de avaliação compatível.

## Chamadas importantes e limitações conhecidas {#important-callouts-known-limitations}

Observe as importantes chamadas a seguir e as limitações conhecidas da versão de disponibilidade geral da funcionalidade para ativar públicos-alvo da conta.

### Pares de mapeamento necessários na etapa de mapeamento ao ativar públicos-alvo da conta para o **[!UICONTROL (Empresas) Públicos-alvo correspondentes do LinkedIn]** destino {#required-mappings}

Ao ativar públicos-alvo da conta para a variável **[!UICONTROL (Empresas) Públicos-alvo correspondentes do LinkedIn]** destino, observe que os dois pares de mapeamento a seguir são obrigatórios para exportar dados com êxito:

![Campos obrigatórios de mapeamento do linkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo de origem | Campo de destino |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecione este campo no campo **[!UICONTROL Selecionar namespace de identidade]** exibir, ao selecionar o **[!UICONTROL Campo de destino]**). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar os públicos-alvo da conta para os destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar os públicos-alvo da conta para os destinos."){width="100" zoomable="yes"} |

### Imposição de governança de dados {#data-governance-enforcement}

O consentimento é aplicado no nível da pessoa ou do perfil para *públicos-alvo de clientes e clientes potenciais*. Por conseguinte,  [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) No momento, o não é compatível com a ativação de públicos-alvo da conta para destinos. Na etapa de revisão do fluxo de trabalho de ativação, é possível ver um controle esmaecido para **[!UICONTROL Exibir políticas de consentimento aplicáveis]**.

![Revise a etapa do fluxo de trabalho ativar públicos-alvo da conta com o controle de imposição de consentimento esmaecido.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Outros mecanismos de governança de dados no Real-Time CDP, como o [verificações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) e [controle de acesso baseado em atributos](/help/destinations/home.md#attribute-based-access) são compatíveis.

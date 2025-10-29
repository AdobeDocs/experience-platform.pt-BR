---
title: (Empresas) LinkedIn connection
description: Use esse destino para ativar os públicos-alvo da conta para os casos de uso do Account-Based Marketing (ABM). Ative perfis para suas campanhas do LinkedIn para direcionamento de público, personalização e supressão, com base em emails com hash.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 4%

---

# (Empresas) Conexão de públicos-alvo de correspondência do LinkedIn {#companies-linkedin}

>[!AVAILABILITY]
>
>A funcionalidade para ativar públicos-alvo da conta para o destino do LinkedIn (Empresas) está disponível para empresas que compram as edições [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) do Real-Time Customer Data Platform.

Use este destino para ativar seus [públicos-alvo da conta](/help/segmentation/types/account-audiences.md) para casos de uso do Account-Based Marketing (ABM). Anuncie para perfis e funções relevantes em suas contas do target por meio do **[!UICONTROL (Companies) LinkedIn]** destino B2B. Visite a documentação do LinkedIn para [saber mais sobre o direcionamento de conta](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) na plataforma do LinkedIn.

>[!TIP]
>
>Para casos de uso de nível individual (ou de empresa para consumidor), a Adobe recomenda o uso do [Público-alvo correspondente do LinkedIn](/help/destinations/catalog/social/linkedin.md).

![Destino da conta do LinkedIn exibido na interface do Experience Platform.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | X | Públicos [importados](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-and-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|--------------|-----------|---------------------------|
| Tipo de exportação | Exportação de público | Todos os membros do público serão exportados com identificadores-chave como nome, número de telefone e muito mais. |
| Frequência | Transmissão | Conexões baseadas em API &quot;sempre ativas&quot;. As atualizações são enviadas para downstream imediatamente após as alterações de perfil. |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Verifique os pré-requisitos abaixo para exportar públicos-alvo da conta para o LinkedIn:

### Pré-requisitos da conta do LinkedIn {#LinkedIn-account-prerequisites}

Antes de usar o destino [!UICONTROL (Companies) LinkedIn Matched Audience], verifique se a sua conta [!DNL LinkedIn Campaign Manager] tem o nível de permissão [!DNL Creative Manager] ou superior.

Para saber como editar suas permissões de usuário do [!DNL LinkedIn Campaign Manager], consulte [Adicionar, Editar, e Remover Permissões de Usuário em Contas do Advertising](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

1. Localize o destino [!DNL (Companies) LinkedIn Matched Audiences] no catálogo de destino e selecione **[!UICONTROL Set Up]**.
2. Selecione **[!UICONTROL Connect to destination]**.
   ![Autenticar para o LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Insira suas credenciais do LinkedIn e selecione **Fazer logon**.

Depois de concluir o processo de logon com o LinkedIn, você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Account ID]**: Seu [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID na sua conta do [!DNL LinkedIn Campaign Manager].

Agora você está pronto para ativar os públicos-alvo da conta para o LinkedIn.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar os públicos-alvo da conta para os destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar os públicos-alvo da conta para destinos."){width="100" zoomable="yes"}

Leia [Ativar públicos-alvo da conta](/help/destinations/ui/activate-account-audiences.md) para obter instruções sobre como ativar públicos-alvo da conta para este destino.

## Pares de mapeamento necessários na etapa de mapeamento ao ativar públicos da conta para o destino **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Ao ativar públicos-alvo da conta para o destino **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, observe que os dois pares de mapeamento a seguir são obrigatórios para exportar dados com êxito:

![Campos obrigatórios de mapeamento do LinkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo de origem | Campo de destino |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (selecione este campo no modo de exibição **[!UICONTROL Select Identity namespace]** ao selecionar o **[!UICONTROL Target Field]**). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar os públicos-alvo da conta para os destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar os públicos-alvo da conta para destinos."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Dados exportados {#exported-data}

Uma ativação bem-sucedida significa que um público-alvo personalizado [!DNL LinkedIn] é criado programaticamente em [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). A associação de público é ajustada conforme os usuários são qualificados ou desqualificados para os públicos ativados.

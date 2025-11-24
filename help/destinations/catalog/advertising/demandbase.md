---
title: Conexão Demandbase
description: Use esse destino para ativar os públicos-alvo da conta para os casos de uso do Account-Based Marketing (ABM). Anuncie para personas e funções relevantes em suas contas do target por meio do Demand Side Platform B2B (DSP) da DemandBase. As contas do Target também podem ser enriquecidas com dados de terceiros do Demandbase para outros casos de uso downstream em marketing e vendas.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: cc05ca282cdfd012366e3deccddcae92a29fef1c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 4%

---

# Conexão Demandbase {#demandbase}

>[!AVAILABILITY]
>
>A funcionalidade para ativar públicos-alvo para o destino do Demandbase está disponível para empresas que compram as edições [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) do Real-Time Customer Data Platform.

Ative perfis para suas campanhas do Demandbase para direcionamento de público, personalização e supressão, com base em [públicos-alvo de conta](/help/segmentation/types/account-audiences.md).

## Caso de uso {#use-case}

Use esse destino para ativar os públicos-alvo da conta para os casos de uso do Account-Based Marketing (ABM). Anuncie para personas e funções relevantes em suas contas do target por meio do Demand Side Platform B2B (DSP) da DemandBase. As contas do Target também podem ser enriquecidas com dados de terceiros do Demandbase para outros casos de uso downstream em marketing e vendas.

Por exemplo, aproveite o DSP de tecnologia de anúncios do Demandbase para direcionar personas ou funções específicas em contas-chave para a geração de leads topo da funnel ou para criar e expandir grupos de compras. Use o destino do Demandbase para explorar outros casos de uso para direcionar suas contas com eficiência.

Com essa integração, você também pode personalizar a experiência do site usando a pesquisa de informações da conta em tempo real para otimizar o engajamento.

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

Para exportar públicos-alvo de conta para o Demandbase, é necessário o seguinte:

1. Uma conta do Demandbase.
2. Um token de API do Demandbase. Você pode gerar um token de API com seu usuário no Demandbase. Para gerar um token, navegue até [Meu perfil > Token de API](https://web.demandbase.com/o/ad/at) depois de fazer logon na sua conta do Demandbase.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

![Adicionar token de portador](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Bearer token]**: Preencha o token do portador para autenticar no destino. Exiba [pré-requisitos](#prerequisites) para obter informações sobre como obter o token.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Adicionar informações sobre a conexão de destino](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Entity type]**: Selecione **[!UICONTROL Account]** como o tipo de entidade.

Agora você está pronto para ativar seus públicos no Demandbase.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar públicos-alvo da conta](/help/destinations/ui/activate-account-audiences.md) para obter instruções sobre como ativar públicos-alvo da conta para este destino.

### Mapeamentos obrigatórios {#mandatory-mappings}

Ao ativar públicos para o destino [!DNL Demandbase], você deve configurar os seguintes mapeamentos de campo obrigatórios na etapa de mapeamento:

| Campo de origem | Campo de destino | Descrição |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | O nome da conta |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | O domínio de email da organização da conta |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | O identificador principal da conta |

![Mapeamentos do Demandbase](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Esses mapeamentos são necessários para que o destino funcione corretamente e devem ser configurados antes de você poder continuar com o fluxo de trabalho de ativação.

## Observações adicionais e chamadas de retorno importantes {#additional-notes}

* **Nomeação do público-alvo**: se um público da conta com o mesmo nome tiver sido ativado anteriormente no Demandbase, você não poderá ativá-lo novamente por meio de um fluxo de dados diferente para o destino do Demandbase.
* **Medidas de proteção da API do Demandbase**: se você tiver exportado públicos para o Demandbase e as exportações forem bem-sucedidas no Experience Platform, mas nem todos os dados atingirem o Demandbase, você poderá ter encontrado uma limitação de API no Demandbase. Entre em contato com eles para obter esclarecimentos.
* **Exclusão de lista**: as listas de contas são exclusivas; portanto, não é possível recriar uma nova lista com um nome já em uso. Quando você remover contas de uma lista, elas não estarão mais disponíveis, mas não serão excluídas.
* **Tempo de ativação**: o carregamento de dados no Demandbase está sujeito a processamento noturno.

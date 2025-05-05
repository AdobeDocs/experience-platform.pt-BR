---
title: Conexão Demandbase
description: Use esse destino para ativar os públicos-alvo da conta para os casos de uso do Account-Based Marketing (ABM). Anuncie para personas e funções relevantes em suas contas do target por meio do Demand Side Platform B2B (DSP) da DemandBase. As contas do Target também podem ser enriquecidas com dados de terceiros do Demandbase para outros casos de uso downstream em marketing e vendas.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions newtab=true"
badgeB2P: label="Edição B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 08c2c7f5080f0e6afb7be53aad9f88ba0fccf923
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 4%

---

# Conexão Demandbase {#demandbase}

>[!AVAILABILITY]
>
>&#x200B;>A funcionalidade para ativar públicos-alvo para o destino do Demandbase está disponível para empresas que compram as edições [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) do Real-Time Customer Data Platform.

Ative perfis para suas campanhas do Demandbase para direcionamento de público, personalização e supressão, com base em [públicos-alvo de conta](/help/segmentation/types/account-audiences.md).

## Caso de uso {#use-case}

Use esse destino para ativar os públicos-alvo da conta para os casos de uso do Account-Based Marketing (ABM). Anuncie para personas e funções relevantes em suas contas do target por meio do Demand Side Platform B2B (DSP) da DemandBase. As contas do Target também podem ser enriquecidas com dados de terceiros do Demandbase para outros casos de uso downstream em marketing e vendas.

Por exemplo, aproveite o DSP de tecnologia de anúncios do Demandbase para direcionar perfis ou funções específicas em contas-chave para a geração de leads topo de funil ou para criar e expandir grupos de compras. Use o destino do Demandbase para explorar outros casos de uso para direcionar suas contas com eficiência.

Com essa integração, você também pode personalizar a experiência do site usando a pesquisa de informações da conta em tempo real para otimizar o engajamento.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
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
>Para se conectar ao destino, você precisa da **[!UICONTROL Permissão de controle de acesso]** e **[!UICONTROL Gerenciar Destinos]** [Permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

![Adicionar token de portador](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Token do portador]**: preencha o token do portador para autenticar no destino. Exiba [pré-requisitos](#prerequisites) para obter informações sobre como obter o token.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Adicionar informações sobre a conexão de destino](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Tipo de entidade]**: selecione **[!UICONTROL Conta]** como o tipo de entidade.

Agora você está pronto para ativar seus públicos no Demandbase.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar públicos-alvo da conta](/help/destinations/ui/activate-account-audiences.md) para obter instruções sobre como ativar públicos-alvo da conta para este destino.

## Observações adicionais e chamadas de retorno importantes {#additional-notes}

* Se um público-alvo da conta com o mesmo nome tiver sido ativado anteriormente no Demandbase, não será possível ativá-lo novamente por meio de um fluxo de dados diferente para o destino do Demandbase.
* Se você tiver exportado públicos para o Demandbase e as exportações forem bem-sucedidas no Experience Platform, mas nem todos os dados chegarem ao Demandbase, você pode ter encontrado a limitação de API no Demandbase. Entre em contato com eles para obter esclarecimentos.

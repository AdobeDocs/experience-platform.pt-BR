---
title: Conexão Bombora ABM Audiences
description: Ative perfis para suas campanhas do Bombora para direcionamento de público, personalização e supressão, com base nos públicos da conta.
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 049112b29b593daa69a11302e828dc968d7abae3
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 3%

---

# Conexão Bombora ABM Audiences {#bombora}

>[!AVAILABILITY]
>
>A funcionalidade para ativar públicos-alvo da conta para o destino Bombora ABM Audiences está disponível para empresas que compram as edições [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) do Real-Time Customer Data Platform.

Ative perfis para suas campanhas do Bombora para direcionamento de público, personalização e supressão, com base em [públicos-alvo de conta](/help/segmentation/types/account-audiences.md).

## Casos de uso {#use-case}

Para ajudá-lo a entender melhor como e quando você deve usar o destino Bombora, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Integração do DSP {#dsp-integration}

Como comerciante B2B, você pode criar uma lista de contas na Real-time CDP, identificando empresas que mostram alta intenção para seus produtos, em seguida, usar esse destino para ativar essa lista na Bombora.

Por meio da integração da Bombora com DSPs, você pode executar campanhas de publicidade direcionadas usando dados da Bombora. Isso garante que seu investimento em anúncios se concentre em empresas com maior probabilidade de conversão.

### Account-Based Marketing {#abm}

Como profissional de marketing B2B, você pode criar uma lista de contas com base no CRM e em sinais de marketing. Em seguida, você pode usar esse destino para ativar essa lista em Bombora, onde os controles sensíveis à ABM ajudam você a direcionar tomadores de decisão a essas empresas.

### Ativação de marketing baseado em conta multicanal {#multi-channel-abm}

Como profissional de marketing B2B, você pode criar uma lista de contas na Real-time CDP, identificando empresas de alta intenção. Em seguida, você pode usar esse destino para ativar a lista em Bombora para executar campanhas direcionadas em vários canais.

Nas redes sociais pagas, você pode enviar anúncios personalizados para profissionais em contas de público alvo em plataformas como [!DNL LinkedIn] e [!DNL Facebook]. Usando plataformas de anúncios nativas, você pode garantir que o conteúdo chegue aos tomadores de decisão relevantes.

Você também pode estender campanhas para TV avançada, fornecendo anúncios para contas principais.

Essa abordagem de vários canais garante mensagens consistentes entre plataformas, maximizando as taxas de engajamento e conversão.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sim | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Todas as outras origens de público-alvo | Sim | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li> carregar audiências personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV,</li><li> públicos-alvo semelhantes, </li><li> públicos federados, </li><li> públicos-alvo gerados em outros aplicativos da Experience Platform, como o Adobe Journey Optimizer, </li><li> e muito mais. </li></ul> |

{style="table-layout:auto"}

Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake do Adobe Experience Platform. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}


## Identidades suportadas {#supported-identities}

O Bombora exige o mapeamento da identidade do target descrita na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição |
|---|---|
| `primaryId` | O Bombora requer o mapeamento dessa identidade de destino para que a integração funcione corretamente. Você pode mapear qualquer campo de origem para essa identidade. Esse mapeamento é obrigatório, mas não exporta dados para Bombora. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-and-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino [!DNL Bombora]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Para exportar públicos-alvo de conta para Bombora, você precisa das informações a seguir.

1. Uma conta do Bombora. Se você não tiver uma, poderá solicitar uma conta do Bombora usando o [formulário de solicitação de ativação de público-alvo do Bombora](https://customers.bombora.com/artcdp/audience-activation-request).
2. Um Bombora **[!UICONTROL client ID]** e **[!UICONTROL client secret]**.
3. Os dados enviados para o Bombora devem ser de conjuntos de dados **habilitados para perfil**, portanto, o conjunto de dados deve ser incluído no Perfil. Verifique se os seus conjuntos de dados estão [habilitados para o Perfil](/help/catalog/datasets/enable-for-profile.md) antes de ativar os públicos para esse destino.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

![Adicionar token de portador](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL Client ID]**: Insira sua ID de cliente [!DNL Bombora].
* **[!UICONTROL Client secret]**: Insira seu segredo de cliente [!DNL Bombora].

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Adicionar informações sobre a conexão de destino](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.

Agora você está pronto para ativar seus públicos dentro Bombora.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar públicos-alvo da conta](/help/destinations/ui/activate-account-audiences.md) para obter instruções sobre como ativar públicos-alvo da conta para este destino.

### Mapeamentos obrigatórios {#mapping}

O destino do Bombora requer que você configure os seguintes mapeamentos para uma ativação de dados bem-sucedida.

| Campo de origem | Campo de destino | Descrição |
|---------|----------|---------|
| Qualquer valor | `Identity: primaryId` | Esse mapeamento é obrigatório para a Experience Platform estabelecer uma conexão com Bombora. Esse valor não é exportado para Bombora, mas é necessário para a configuração de destino. Você pode selecionar qualquer atributo para o campo de origem. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora usa endereços de site ou domínio para criar uma lista de contas. |

![Adicionar mapeamentos obrigatórios](../..//assets/catalog/advertising/bombora/mappings.png)

## Comportamento de sincronização de público {#sync-behavior}

Após a ativação inicial do público, as atualizações subsequentes do público no Experience Platform são sincronizadas de forma incremental com o Bombora. Os seguintes comportamentos se aplicam:

* **Conta adicionada ao público-alvo**: quando uma conta é adicionada ao público-alvo no Experience Platform, ela é automaticamente adicionada ao público-alvo correspondente no Bombora.
* **Conta removida ou não se qualifica mais**: quando uma conta não se qualifica mais para o público-alvo ou é removida do público-alvo no Experience Platform, ela é removida do público-alvo correspondente no Bombora.
* **Conta ou perfil excluído**: quando uma conta ou perfil é excluído da Experience Platform e essa conta não se qualifica mais para o público-alvo, ele é removido do público correspondente em Bombora.

### Comportamento de exclusão e desconexão de público-alvo {#deletion-disconnect}

Excluir um público no Experience Platform ou remover um público de um fluxo de dados de ativação do Bombora remove o público da sua conta do Bombora.

## Observações adicionais e chamadas de retorno importantes {#additional-notes}

Se um público-alvo da conta com o mesmo nome foi ativado anteriormente para o Bombora, você receberá um erro se tentar ativá-lo novamente por meio de um fluxo de dados diferente para o destino do Bombora.

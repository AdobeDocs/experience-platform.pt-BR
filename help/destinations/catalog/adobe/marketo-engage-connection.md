---
title: Conexão Marketo Engage
description: O Marketo Engage é a única solução completa de gerenciamento de experiência do cliente (CXM) para marketing, publicidade, análises e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais de CRM e do envolvimento do cliente para o marketing baseado em conta e a atribuição de receita.
exl-id: e02b6c65-b59e-41ff-8d33-f8fecfd87773
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 2%

---

# Conexão com o Marketo Engage

## Visão geral {#overview}

O [!DNL Marketo Engage] é a única solução CXM (gerenciamento de experiência do cliente) completa para marketing, publicidade, análises e comércio. Ele permite automatizar e gerenciar atividades do gerenciamento de clientes potenciais de CRM e do envolvimento do cliente para o marketing baseado em conta e a atribuição de receita.

Use esse destino para a sincronização em tempo real de dados de público-alvo e atributos de perfil entre o Adobe Experience Platform e o Marketo Engage.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Marketo Engage], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Casos de uso de sincronização de público-alvo {#audience-sync-use-cases}

**Reconectar somente clientes em potencial conhecidos**

A equipe de marketing deseja executar uma campanha de retorno direcionada a clientes potenciais que não se envolveram em mais de 90 dias, mas já existem no Marketo.

Eles podem ativar os públicos para o Marketo Engage e usar o tipo de sincronização **[!UICONTROL Audience Only]**.

### Casos de uso de sincronização de público-alvo e perfil {#audience-profile-sync-use-cases}

**Reconectar clientes em potencial conhecidos e atualizar clientes em potencial**

A equipe de marketing deseja iniciar uma campanha de reengajamento para contatos existentes do Marketo que demonstraram interesse com base nas visitas ao site. Eles também desejam atualizar as informações de clientes potenciais (como preferências, informações demográficas), mas não criar novas pessoas no Marketo.

Eles podem ativar os públicos para o Marketo Engage e usar o tipo de sincronização **[!UICONTROL Audience and Profile]** combinado com a ação **[!UICONTROL Update existing persons only]** para garantir que eles segmentem apenas os públicos que já existem no Marketo.

**Reengajar e expandir alcance com sincronização completa de perfil**

A equipe de marketing deseja ativar um público-alvo de interesse do produto para uma nova campanha. Embora muitos dos perfis já existam no Marketo, alguns são novos e só estão presentes no Real-Time CDP. Para as pessoas existentes, eles querem ter certeza de que estão atualizando essas pessoas no Marketo, mas também criar novos perfis.

Eles podem ativar seus públicos no Marketo Engage e usar o tipo de sincronização **[!UICONTROL Audience and Profile]** combinado com a ação **[!UICONTROL Update existing and create new persons]** para garantir que eles segmentem clientes potenciais existentes do Marketo e criem novos para os novos públicos exportados do Real-Time CDP.

## Pré-requisitos {#prerequisites}

* O usuário que configura o destino deve ter a permissão [Editar Pessoa](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) em sua instância e partição do Marketo.
* Somente instâncias do Marketo Engage na mesma organização da Adobe Real-Time CDP estarão disponíveis ao configurar esse destino.
* Somente as instâncias do Marketo Engage que têm seus usuários gerenciados no Adobe Admin Console podem utilizar esse destino.

## Identidades suportadas {#supported-identities}

[!DNL Marketo Engage] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| `DedupeField` | O campo usado para identificar e corresponder clientes potenciais existentes no Marketo. | Durante a etapa [mapping](#mapping), mapeie qualquer campo de origem (como `Email` ou outros identificadores personalizados) que você deseja usar como campo de desduplicação para esta identidade de destino. Para obter melhores resultados, escolha um campo que esteja disponível e seja exclusivo de forma consistente em todos os perfis do cliente. Não há suporte para `ECID` como campo de desduplicação. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino. As duas tabelas abaixo indicam a quais públicos este conector dá suporte, por _origem do público-alvo_ e _tipos de perfil incluídos no público-alvo_:

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Todas as outras origens de público-alvo | ✓ | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li> carregar audiências personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV,</li><li> públicos-alvo semelhantes, </li><li> públicos federados, </li><li> públicos-alvo gerados em outros aplicativos da Experience Platform, como o Adobe Journey Optimizer, </li><li> e muito mais. </li></ul> <br> |

{style="table-layout:auto"}

Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake do Adobe Experience Platform. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público com os identificadores (email, ECID) usados no destino [!DNL Marketo Engage]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Comportamento de correspondência de lead {#lead-matching}

Entender como a correspondência de clientes potenciais do Marketo funciona ajuda você a escolher a configuração correta para seu caso de uso. O comportamento correspondente depende das configurações de **[!UICONTROL Sync Type]** e **[!UICONTROL Person Action]** selecionadas.

O Marketo usa o **[!UICONTROL Marketo deduplication field]** selecionado para corresponder perfis do Experience Platform com clientes potenciais existentes da Marketo. O processo de correspondência pesquisa todas as partições na instância do Marketo para encontrar leads existentes. Consulte a tabela abaixo para entender como os clientes em potencial são criados e atualizados na instância do Marketo, dependendo da configuração selecionada.

| Tipo de sincronização | Ação de pessoa | Comportamento de correspondência |
|-----------|---------------|-------------------|
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Atualiza clientes potenciais existentes com novos dados de perfil</li><li>Cria novos clientes em potencial na partição selecionada para perfis sem correspondência</li></ul> |
| **[!UICONTROL Profile only]** | **[!UICONTROL Update existing persons only]** | <ul><li>Atualiza clientes potenciais existentes com novos dados de perfil</li><li>Nenhum cliente potencial novo criado para perfis sem correspondência</li></ul> |
| **[!UICONTROL Audience only]** | N/D | <ul><li>Adiciona clientes em potencial existentes a listas de público-alvo</li><li>Nenhum cliente potencial novo criado para perfis sem correspondência</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing and create new persons]** | <ul><li>Atualiza clientes potenciais existentes com novos dados de perfil</li><li>Adiciona clientes em potencial existentes a listas de público-alvo</li><li>Cria novos clientes em potencial na partição selecionada para perfis sem correspondência</li><li>Adiciona novos leads às listas de público-alvo</li></ul> |
| **[!UICONTROL Audience and profile]** | **[!UICONTROL Update existing persons only]** | <ul><li>Atualiza clientes potenciais existentes com novos dados de perfil</li><li>Adiciona clientes em potencial existentes a listas de público-alvo</li><li>Nenhum cliente potencial novo criado para perfis sem correspondência</li></ul> |

{style="table-layout:auto"}

### Considerações importantes

* **Seleção de campo de eliminação de duplicação**: escolha um campo que esteja consistentemente disponível e exclusivo em seus perfis de cliente (por exemplo: endereço de email, ID do cliente)
* **Manipulação de partição**: ao criar novos clientes potenciais, eles serão colocados na partição selecionada (ou na partição **[!UICONTROL Default]** se você não tiver selecionado uma partição)
* **Tratamento de duplicados**: se vários clientes potenciais do Marketo corresponderem ao mesmo perfil, somente o cliente potencial atualizado mais recentemente será atualizado
* **Correspondência entre partições**: o sistema pesquisa em todas as partições para localizar clientes potenciais existentes, independentemente da partição selecionada para novos clientes potenciais

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>* Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
>
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Connect to destination]**.

![Captura de tela mostrando como autenticar no destino](../../assets/catalog/adobe/marketo-engage-connection/connect-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela de exemplo mostrando como preencher detalhes para o seu destino](../../assets/catalog/adobe/marketo-engage-connection/destination-details.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Munchkin ID]**: Selecione o [!DNL Marketo Munchkin ID] que deseja usar para este destino.
* **[!UICONTROL Workspace ID]**: selecione sua ID de espaço de trabalho do Marketo.
* **[!UICONTROL Sync type]**: Selecione o tipo de sincronização que deseja usar para este destino:
   * **[!UICONTROL Audience and profile]**: selecione esta opção quando quiser adicionar membros de público-alvo a listas do Marketo e manter suas informações de perfil atualizadas.
   * **[!UICONTROL Profile only]**: selecione esta opção quando quiser manter os perfis de clientes potenciais do Marketo atualizados com as informações mais recentes do Experience Platform.
   * **[!UICONTROL Audience only]**: selecione esta opção quando quiser adicionar membros de público-alvo a listas do Marketo sem atualizar suas informações de perfil.
* **[!UICONTROL Partition]**: *A seleção de partição está disponível somente ao escolher **[!UICONTROL Profile only]**ou **[!UICONTROL Audience and profile]**tipos de sincronização*. Selecione uma ID de partição do Marketo associada ao espaço de trabalho escolhido. Isso permite especificar qual partição de cliente potencial no Marketo receberá os dados exportados. Se você não escolher uma partição específica, seus dados serão enviados para a partição **[!UICONTROL Default]** no Marketo.
* **[!UICONTROL Marketo deduplication field]**: selecione o campo de desduplicação do Marketo que deseja usar ao atualizar clientes potenciais existentes do Marketo. Este seletor mostra os campos marcados como campos de desduplicação no Marketo. Se quiser que um campo específico do Marketo seja exibido como um campo de desduplicação, você deve marcar o campo como um [campo pesquisável](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/lead-database/lead-database) no Marketo.

  >[!NOTE]
  >
  >Marketo `Lead ID` e Experience Cloud IDs (`ECID`) não têm suporte para desduplicação.

* **[!UICONTROL Person Action]**: Selecione a ação do Marketo que deseja executar ao exportar dados.
   * **[!UICONTROL Update existing and create new persons]**: selecione esta opção para atualizar clientes potenciais existentes do Marketo e criar novos clientes potenciais para os membros do público que ainda não estão no Marketo. Novos clientes em potencial serão criados na partição selecionada. Se você não selecionou uma partição, novos clientes em potencial serão criados na partição **[!UICONTROL Default]**.
   * **[!UICONTROL Update existing persons only]**: selecione esta opção quando quiser apenas atualizar clientes potenciais existentes do Marketo sem criar novos. Se vários clientes em potencial corresponderem ao mesmo perfil, somente o cliente em potencial do Marketo atualizado mais recentemente será atualizado com seus dados do Experience Platform.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Mapeamentos necessários {#required-mappings}

Durante a etapa de mapeamento, mapeie qualquer campo de origem (como `email` ou outros identificadores personalizados) que você deseja usar como campo de desduplicação para a identidade de destino `DedupeField`. Para obter melhores resultados, escolha um campo que esteja disponível e seja exclusivo de forma consistente em todos os perfis do cliente.

Para que o Marketo crie clientes em potencial com sucesso, você também deve mapear os seguintes atributos de destino necessários:

* `firstName`: O nome do cliente potencial
* `lastName`: O sobrenome do cliente potencial
* `email`: O endereço de email do cliente potencial

Se você estiver usando `email` como campo de desduplicação, também deverá mapear os atributos `firstName` e `lastName` conforme mostrado na imagem abaixo.

![Captura de tela mostrando o mapeamento necessário ao usar Email como campo de desduplicação](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email-dedupe.png)

Se você estiver usando um campo de desduplicação diferente, mapeie manualmente todos os três atributos necessários (`firstName`, `lastName`, `email`) conforme mostrado na imagem abaixo.

![Captura de tela mostrando o mapeamento necessário ao não usar Email como campo de desduplicação](../../assets/catalog/adobe/marketo-engage-connection/required-mapping-email.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Depois de exportar os públicos para o Marketo Engage, faça logon na conta do Marketo para verificar se os públicos-alvo foram ativados conforme esperado. Verifique as partições e os espaços de trabalho dos clientes potenciais relevantes no Marketo para confirmar se os dados do público-alvo aparecem corretamente e se as ações desejadas (como atualizar ou criar pessoas) foram executadas.

Se não vir os dados esperados, revise as configurações de mapeamento e exportação no Adobe Experience Platform e tente exportar novamente.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

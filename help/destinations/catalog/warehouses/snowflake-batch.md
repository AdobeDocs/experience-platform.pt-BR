---
title: Conexão em lote do Snowflake
description: Crie um compartilhamento de dados em tempo real do Snowflake para receber atualizações diárias de públicos diretamente como tabelas compartilhadas na sua conta.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 6959ccd0-ba30-4750-a7de-d0a709292ef7
source-git-commit: 59df2c6a0fb5d9dbdd10b52d82fb6b94f5083c3a
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 4%

---

# Conexão em lote do Snowflake {#snowflake-destination}

>[!AVAILABILITY]
>
>Este conector de destino está em disponibilidade limitada e só está disponível para clientes do Real-Time CDP Ultimate provisionados na [região VA7](/help/landing/multi-cloud.md#azure-regions).

## Visão geral {#overview}

Use esse destino para enviar dados de público-alvo para tabelas dinâmicas na sua conta do Snowflake. As tabelas dinâmicas fornecem acesso aos dados sem exigir cópias físicas dos dados.

Leia as seções a seguir para entender como o destino do Snowflake funciona e como os dados são transferidos entre o Adobe e o Snowflake.

### Como funciona o compartilhamento de dados do Snowflake {#data-sharing}

Esse destino usa um compartilhamento de dados do [!DNL Snowflake], o que significa que nenhum dado é fisicamente exportado ou transferido para sua própria instância do Snowflake. Em vez disso, o Adobe concede acesso somente leitura a uma tabela ativa hospedada no ambiente Snowflake do Adobe. Você pode consultar essa tabela compartilhada diretamente da sua conta da Snowflake, mas não é o proprietário da tabela e não pode modificá-la ou mantê-la além do período de retenção especificado. O Adobe gerencia totalmente o ciclo de vida e a estrutura da tabela compartilhada.

Na primeira vez depois de configurar um fluxo de dados do Adobe para sua conta da Snowflake, você será solicitado a aceitar a lista privada do Adobe.

![Captura de tela mostrando a tela de aceitação da lista privada do Snowflake](../../assets/catalog/cloud-storage/snowflake-batch/snowflake-accept-listing.png)

### Retenção de dados e TTL (Time-to-Live) {#ttl}

Todos os dados compartilhados por meio dessa integração têm um TTL (Time-to-Live) fixo de sete dias. Sete dias após a última exportação, a tabela dinâmica expira automaticamente e se torna inacessível, independentemente de o fluxo de dados ainda estar ativo. Se você precisar reter os dados por mais de sete dias, copie o conteúdo em uma tabela de sua propriedade na própria instância do Snowflake antes que o TTL expire.

>[!IMPORTANT]
>
>A exclusão de um fluxo de dados no Experience Platform resultará no desaparecimento da tabela dinâmica da sua conta do Snowflake.

### Comportamento de atualização do público {#audience-update-behavior}

Se o público-alvo for avaliado no [modo de lote](../../../segmentation/methods/batch-segmentation.md), os dados na tabela compartilhada serão atualizados a cada 24 horas. Isso significa que pode haver um atraso de até 24 horas entre as alterações na associação de público-alvo e quando essas alterações são refletidas na tabela compartilhada.

### Lógica de compartilhamento de dados em lote {#batch-data-sharing}

Quando um fluxo de dados é executado para um público-alvo pela primeira vez, ele executa um preenchimento retroativo e compartilha todos os perfis qualificados no momento. Após esse preenchimento retroativo inicial, o destino fornece instantâneos periódicos da associação completa do público-alvo. Cada instantâneo substitui os dados anteriores na tabela compartilhada, garantindo que você sempre veja a exibição completa mais recente do público-alvo sem dados históricos.

## Compartilhamento de dados em lote versus transmissão {#batch-vs-streaming}

A Experience Platform fornece dois tipos de destinos do Snowflake: [Streaming do Snowflake](snowflake.md) e [Lote do Snowflake](snowflake-batch.md).

Embora ambos os destinos forneçam acesso aos seus dados no Snowflake de maneira zero, há algumas práticas recomendadas em termos de casos de uso para cada conector.

A tabela abaixo ajudará você a decidir qual conector usar, descrevendo os cenários em que cada método de compartilhamento de dados é mais apropriado.

|  | Escolha o [Lote do Snowflake](snowflake-batch.md) quando precisar | Escolha [Streaming do Snowflake](snowflake.md) quando precisar |
|--------|-------------------|----------------------|
| **Frequência de atualização** | Instantâneos periódicos | Atualizações contínuas em tempo real |
| **Apresentação de dados** | Instantâneo completo do público-alvo que substitui os dados anteriores | Atualizações incrementais com base em alterações de perfil |
| **Foco no caso de uso** | Cargas de trabalho analíticas/de ML onde a latência não é crítica | Cenários de ação imediata que exigem atualizações em tempo real |
| **Gerenciamento de dados** | Sempre ver instantâneo concluído mais recente | Atualizações incrementais com base em alterações de associação de público |
| **Exemplos de cenários** | Relatórios de negócios, análise de dados, treinamento de modelo de ML | Supressão da campanha de marketing, personalização em tempo real |

Para obter mais informações sobre compartilhamento de dados de transmissão, consulte a documentação da [Conexão de transmissão do Snowflake](snowflake.md).

## Casos de uso {#use-cases}

O compartilhamento de dados em lote é ideal para cenários em que você precisa de um instantâneo completo do seu público-alvo e em que não são necessárias atualizações em tempo real, como:

* **Cargas de trabalho analíticas**: ao executar tarefas de análise de dados, relatórios ou business intelligence que exigem uma exibição completa da associação de público-alvo
* **Fluxos de trabalho de aprendizado de máquina**: Para modelos de aprendizado de máquina ou execução de análises preditivas que se beneficiam de instantâneos completos de público-alvo
* **Data warehouse**: quando é necessário manter uma cópia atual dos dados do público-alvo em sua própria instância do Snowflake
* **Relatórios periódicos**: para relatórios comerciais regulares nos quais você precisa do estado do público-alvo mais recente sem o rastreamento de alterações históricas
* **Processos ETL**: quando você precisa transformar ou processar dados de público-alvo em lotes

O compartilhamento de dados em lote simplifica o gerenciamento de dados fornecendo instantâneos completos, eliminando a necessidade de gerenciar atualizações incrementais ou mesclar alterações manualmente.

## Pré-requisitos {#prerequisites}

Antes de configurar a conexão do Snowflake, verifique se os seguintes pré-requisitos estão sendo atendidos:

* Você tem acesso a uma conta [!DNL Snowflake].
* Sua conta do Snowflake tem inscrições em listas privadas. Você ou alguém em sua empresa que tenha privilégios de administrador de conta no Snowflake pode configurar isso.

Leia a [[!DNL Snowflake] documentação](https://docs.snowflake.com/en/collaboration/consumer-listings-access#access-a-private-listing) para obter mais informações sobre as permissões necessárias.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino. As duas tabelas abaixo indicam a quais públicos este conector dá suporte, por _origem do público-alvo_ e _tipos de perfil incluídos no público-alvo_:

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Todas as outras origens de público-alvo | ✓ | Esta categoria inclui todas as origens de público-alvo fora dos públicos-alvo gerados pelo [!DNL Segmentation Service]. Leia sobre as [várias origens do público-alvo](/help/segmentation/ui/audience-portal.md#customize). Alguns exemplos incluem: <ul><li> carregar audiências personalizadas [importadas](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV,</li><li> públicos-alvo semelhantes, </li><li> públicos federados, </li><li> públicos-alvo gerados em outros aplicativos da Experience Platform, como o Adobe Journey Optimizer, </li><li> e muito mais. </li></ul> |

{style="table-layout:auto"}

Públicos-alvo compatíveis por tipo de dados de público-alvo:

| Tipo de dados de público | Suportado | Descrição | Casos de uso |
|--------------------|-----------|-------------|-----------|
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | ✓ | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake do Adobe Experience Platform. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino [!DNL Snowflake]. |
| Frequência de exportação | **[!UICONTROL Batch]** | Esse destino fornece instantâneos periódicos da associação completa do público-alvo por meio do compartilhamento de dados do Snowflake. Cada instantâneo substitui os dados anteriores, garantindo que você sempre tenha a visualização completa mais recente do público-alvo. |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Connect to destination]** e forneça um nome de conta e, opcionalmente, uma descrição de conta.

![Captura de tela de exemplo mostrando como autenticar no destino](../../assets/catalog/cloud-storage/snowflake-batch/authenticate-destination.png)

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_batch_accountID"
>title="Insira sua ID da conta do Snowflake"
>abstract="Se sua conta estiver vinculada a uma organização, use este formato: `OrganizationName.AccountName`<br><br> Se sua conta não estiver vinculada a uma organização, use este formato:`AccountName`"

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela de exemplo mostrando como preencher detalhes para o seu destino](../../assets/catalog/cloud-storage/snowflake-batch/configure-destination-details.png)

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Snowflake Account ID]**: sua ID de conta da Snowflake. Use o seguinte formato de ID de conta, dependendo se sua conta está vinculada a uma organização:
   * Se sua conta estiver vinculada a uma organização:`OrganizationName.AccountName`.
   * Se sua conta não estiver vinculada a uma organização:`AccountName`.
* **[!UICONTROL Account acknowledgment]**: Ative a confirmação da ID de conta da Snowflake para confirmar se a ID de conta está correta e se pertence a você.

>[!IMPORTANT]
>
> Caracteres especiais usados no nome de destino e no nome da sandbox do Experience Platform são convertidos automaticamente em sublinhados (`_`) no Snowflake. Para evitar confusão, não use caracteres especiais no destino e no nome da sandbox.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar dados de público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear atributos {#map}

Você pode exportar identidades e atributos de perfil para esse destino.

![Imagem da interface do usuário do Experience Platform mostrando a tela de mapeamento para o destino do Snowflake.](../../assets/catalog/cloud-storage/snowflake-batch/mapping.png)

Você pode usar o [controle de campos calculados](../../ui/data-transformations-calculated-fields.md) para exportar e executar operações em matrizes.

Os atributos de destino são criados automaticamente no Snowflake usando o nome do atributo fornecido no campo **[!UICONTROL Attribute name]**.

## Dados exportados / Validar exportação de dados {#exported-data}

Os dados são transferidos para sua conta do Snowflake por meio de uma tabela dinâmica. Verifique sua conta do Snowflake para verificar se os dados foram exportados corretamente.

### Estrutura de dados {#data-structure}

A tabela dinâmica contém as seguintes colunas:

* **TS**: uma coluna de carimbo de data/hora que representa quando cada linha foi atualizada pela última vez
* **Atributos de mapeamento**: todos os atributos de mapeamento selecionados durante o fluxo de trabalho de ativação são representados como um cabeçalho de coluna no Snowflake
* **Associação de público-alvo**: a associação a qualquer público mapeado para o fluxo de dados é indicada por meio de uma entrada `active` na célula correspondente

![Captura de tela mostrando a interface do Snowflake com dados da tabela dinâmica](../../assets/catalog/cloud-storage/snowflake-batch/data-validation.png)

## Limitações conhecidas {#known-limitations}

### Restrição de política de mesclagem padrão {#default-merge-policy-restriction}

Atualmente, somente os públicos-alvo mapeados para a política de mesclagem padrão podem ser exportados.

### Disponibilidade regional {#regional-availability}

O destino em lote [!DNL Snowflake] está disponível no momento apenas para clientes do Real-Time CDP provisionados na região do Experience Platform VA7.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

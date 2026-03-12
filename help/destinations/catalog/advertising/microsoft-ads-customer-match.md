---
keywords: publicidade, microsoft ads, correspondência com o cliente,
title: Conexão de correspondência do cliente do Microsoft Ads
description: Use o destino da Correspondência do cliente do Microsoft Ads para corresponder os clientes por endereço de email e reengajar com eles na Microsoft Advertising Network, incluindo anúncios de pesquisa e público-alvo.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 4d405ffb-f600-463b-a215-44e806b6d139
source-git-commit: 82f412676c89d7d14116be9328ab7fa438e10fc0
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 3%

---

# [!DNL Microsoft Ads Customer Match] conexão {#microsoft-ads-customer-match-destination}

>[!AVAILABILITY]
>
>Este conector de destino está atualmente com disponibilidade limitada. Para obter acesso, entre em contato com um representante da Adobe.

## Visão geral {#overview}

Use o destino [!DNL Microsoft Ads Customer Match] para corresponder clientes por endereço de email e reengajar com eles no [!DNL Microsoft Advertising Network], incluindo anúncios de Pesquisa e Público-alvo. Vincule sua conta do [!DNL Microsoft Advertising] à Real-Time CDP para automatizar a criação e o gerenciamento de listas de correspondência de clientes diretamente da Experience Platform.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando usar o destino [!DNL Microsoft Ads Customer Match], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

### Caso de uso #1

Uma marca de comércio eletrônico deseja alcançar clientes existentes por meio de [!DNL Microsoft Search] e [!DNL Microsoft Audience Network] para personalizar ofertas com base em suas compras anteriores e histórico de navegação. A marca pode assimilar endereços de email de seu próprio CRM na Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para [!DNL Microsoft Ads Customer Match] para serem usados em anúncios de pesquisa e público, otimizando seus gastos com publicidade.

### Caso de uso #2

Uma empresa de tecnologia lançou um novo produto. Para promover esse novo produto, eles buscam gerar conscientização entre os clientes que compraram produtos relacionados anteriormente. Eles carregam endereços de email do banco de dados do CRM na Experience Platform, usando os endereços de email como identificadores. Os públicos-alvo são criados com base nos clientes que possuem produtos relacionados. Esses públicos-alvo são enviados para [!DNL Microsoft Ads Customer Match], para que a empresa possa direcionar os clientes atuais e clientes semelhantes no [!DNL Microsoft Advertising Network].

## Identidades suportadas {#supported-identities}

[!DNL Microsoft Ads Customer Match] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| `email` | Endereços de email de texto sem formatação | A conexão [!DNL Microsoft Ads Customer Match] dá suporte somente a endereços de email de texto sem formatação. O Experience Platform coloca automaticamente os endereços de email em hash na exportação para corresponder aos requisitos da Microsoft. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

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

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público com os identificadores (endereços de email) usados no destino [!DNL Microsoft Ads Customer Match]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Para enviar dados de público-alvo para [!DNL Microsoft Ads], você precisa ter uma conta [!DNL Microsoft Advertising] ativa. Para obter detalhes sobre como criar uma conta, consulte a [documentação do Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/53090/0).

### Aceitar os termos e condições de correspondência do cliente {#accept-customer-match-terms}

Antes de ativar públicos por meio desse destino, primeiro crie manualmente uma lista de correspondências do cliente na sua conta [!DNL Microsoft Advertising]. Essa criação manual inicial é necessária para aceitar os termos e condições de correspondência do cliente, o que permite que os públicos-alvo enviados pelo Experience Platform sejam criados automaticamente. A falha na conclusão desta etapa pode resultar em erros ao ativar os públicos-alvo.

### Configuração da conta {#account-configuration}

Ao configurar o destino, você deve fornecer as seguintes informações:

* [!UICONTROL Customer ID]: sua ID de cliente (CID) do [!DNL Microsoft Ads], em formato inteiro. Consulte a [documentação do Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obter instruções sobre como encontrar a ID do cliente.
* [!UICONTROL Customer Account ID]: sua ID de conta de cliente do [!DNL Microsoft Ads]. Consulte a [documentação do Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obter instruções sobre como encontrar a ID da conta do cliente.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Preencher detalhes do destino {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_id"
>title="Customer ID"
>abstract="Sua ID de cliente do Microsoft Advertising, também conhecida como ID da conta do gerente. Esse é o identificador de nível superior no Microsoft Advertising que pode ter várias contas de anunciante (IDs de conta do cliente) nele."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Encontrar a ID do cliente"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_customer_account_id"
>title="ID da conta do cliente"
>abstract="Sua ID de conta de cliente do Microsoft Advertising, também conhecida como ID de conta do anunciante. Isso identifica uma conta de anunciante específica na ID do cliente."
>additional-url="https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids" text="Encontrar a ID da conta do cliente"

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_membership_duration"
>title="Duração da associação"
>abstract="O número de dias que um usuário permanece na lista de correspondência do cliente. Os valores aceitos estão entre 1 e 390 dias."

>[!CONTEXTUALHELP]
>id="platform_destinations_microsoft_ads_cm_list_availability"
>title="Disponibilidade da Lista de Correspondência do Cliente"
>abstract="Escolha se a lista de correspondência do cliente está disponível para uma única conta de anunciante ou para todas as contas na conta de gerente. Selecione Customer ID para disponibilizar a lista em todas as contas de anunciante na ID do cliente. Selecione ID da Conta do Cliente para restringir a lista à ID da Conta do Cliente específica."
>additional-url="https://help.ads.microsoft.com/apex/index/3/en/56727" text="Saiba mais sobre o compartilhamento da lista de públicos-alvo no Microsoft Advertising"

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Customer ID]**: Sua ID de cliente (CID) do [!DNL Microsoft Ads]. Consulte a [documentação do Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obter instruções sobre como encontrar a ID do cliente.
* **[!UICONTROL Customer Account ID]**: Sua ID de Conta de Cliente do [!DNL Microsoft Ads]. Consulte a [documentação do Microsoft Advertising](https://learn.microsoft.com/en-us/advertising/guides/get-started?view=bingads-13#get-ids) para obter instruções sobre como encontrar a ID da conta do cliente.
* **[!UICONTROL Membership Duration]**: o número de dias que um usuário permanece na lista de correspondência do cliente. Os valores aceitos estão entre 1 e 390 dias.
* **[!UICONTROL Customer Match List Availability]**: Selecione a disponibilidade da lista de correspondência do cliente. No [!DNL Microsoft Advertising], uma ID do cliente pode ter várias IDs de conta do cliente (contas de anunciante) sob ela. Selecione **[!UICONTROL Customer ID (all advertising accounts)]** para disponibilizar a lista em todas as contas de anunciante em sua ID de cliente, ou **[!UICONTROL Customer Account ID (single advertising account)]** para restringir a lista à ID de Conta de Cliente específica fornecida acima. Consulte a [documentação do Microsoft Advertising](https://help.ads.microsoft.com/apex/index/3/en/56727) para obter mais detalhes.

![Imagem da interface do usuário da plataforma mostrando os campos de detalhes de destino para o destino da Correspondência do cliente do Microsoft Ads.](../../assets/catalog/advertising/microsoft-ads-customer-match/destination-details.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades* para destinos, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Mapeamento {#mapping}

Na etapa **[!UICONTROL Mapping]**, mapeie a identidade de email dos perfis de origem para a identidade de destino em [!DNL Microsoft Ads Customer Match].

* **Campo do Source**: selecione `IdentityMap: Email` como campo de origem para mapear identidades de email de seus perfis. Como alternativa, você pode selecionar um atributo XDM, como `personalEmail.address`, como o campo de origem.
* **Campo de destino**: selecione `Identity: email` como campo de destino.

>[!IMPORTANT]
>
>Você deve usar campos de origem sem hash (texto simples). Não use identidades de origem com hash prévio, como `Emails (SHA256, lowercased)`. O Experience Platform coloca os endereços de email na exportação em hash automaticamente para corresponder aos requisitos do Microsoft.

![Imagem da interface do usuário mostrando a etapa de mapeamento com o email do IdentityMap mapeado ao email de identidade.](../../assets/catalog/advertising/microsoft-ads-customer-match/mapping.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Microsoft Ads Customer Match], verifique sua conta [!DNL Microsoft Advertising]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na sua conta como listas de correspondência do cliente.

## Recursos adicionais {#additional-resources}

Consulte a [Central de Ajuda do Microsoft Advertising](https://help.ads.microsoft.com/) para obter mais informações.

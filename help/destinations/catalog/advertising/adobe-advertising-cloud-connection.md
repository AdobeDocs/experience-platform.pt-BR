---
title: Conexão com o Adobe Advertising DSP
description: Saiba como compartilhar públicos primários autenticados e não autenticados com o Adobe Advertising Cloud Demand-Side Platform (DSP) usando vários tipos de identidade.
feature: Destinations
source-git-commit: 5513e95637c1016caeb6abe699e1807cc234ed40
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 2%

---


# Conexão com o Adobe Advertising DSP

## Visão geral {#overview}

O destino do Adobe Advertising Cloud Demand-Side Platform (DSP) permite que os usuários compartilhem públicos primários autenticados e não autenticados com uma conta do DSP ou um anunciante específico em uma conta.

Esse destino permite que os clientes compartilhem públicos-alvo primários com uma ou todas essas IDs:

* ID de email com hash, que é convertida em um [!DNL LiveRamp RampID] ou [!DNL Unified ID 2.0] (UID2.0) para direcionamento no DSP

* Cookies de terceiros da Experience Cloud ID (ECID) e Adobe Advertising

* IDs de anúncios móveis (MAIDs):

   * [!DNL Google] GAIDs (Advertising IDs) para [!DNL Android] dispositivos

   * Identificadores para anunciantes (IDFAs) para [!DNL Apple iOS] dispositivos

Esta conexão substitui a [conexão herdada do Adobe Advertising Cloud DSP](adobe-advertising-cloud-connection-legacy.md), que dá suporte somente a endereços de email com hash.

>[!IMPORTANT]
>
>Esta página foi criada pela equipe [!DNL DSP] do Adobe Advertising. Para qualquer consulta ou solicitação de atualização, entre em contato com o suporte da Advertising Cloud diretamente em `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Esse destino permite que os anunciantes alcancem seu público-alvo em navegadores com e sem cookies.

Os anunciantes têm a opção de compartilhar segmentos com identificadores primários autenticados (como [!DNL RampID] e [!DNL UID2.0]) ou como IDs não autenticadas (como cookies e MAIDs).

## Pré-requisitos {#prerequisites}

* Para [!DNL RampID activation], [!DNL DSP] configurações no nível da conta e no nível da campanha para habilitar o compartilhamento de público-alvo com [!DNL LiveRamp RampID], que converte os dados do cliente em [!DNL RampIDs] para criar segmentos direcionáveis. A equipe de conta da Adobe executará essa configuração. [!DNL RampID] está disponível por meio de uma parceria entre [!DNL DSP] e [!DNL LiveRamp], e você não precisa de sua própria associação [!DNL LiveRamp] para usá-la.

* IDs de público-alvo:

   * Para [!DNL RampID] e [!DNL UID2.0], os perfis devem conter IDs de email com hash.

   * Para cookies, configure um processo de sincronização de cookies com [!DNL Web SDK] fluxos de dados ou o [!DNL Experience Cloud ID Service]. Consulte [Configurar sincronização de ID para compartilhar cookies](#cookie-sync) abaixo.

   * Para perfis com MAIDs:

      * Para cada GAID, inclua o valor `GAID` em uma coluna IdentityMap.

      * Para cada IDFA, inclua o valor `IDFA` em uma coluna IdentityMap.

* A ID da organização da Experience Cloud para a conta da Experience Platform. Você pode encontrar sua ID na página de perfil do usuário do Adobe Real-Time Customer Data Platform (Real-Time CDP).

* Uma [fonte do Real-Time CDP no DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=pt-BR) para receber públicos-alvo para ativação de campanha. Sua equipe de conta da Adobe criará a fonte usando sua ID de organização da Experience Cloud.

* A chave de origem da conta ou anunciante [!DNL DSP], que é gerada quando uma origem do Real-Time CDP [é criada em  [!DNL DSP]](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=pt-BR). A equipe de conta do [!DNL DSP] compartilhará essa chave com você. Você o usará no Experience Platform para criar uma conexão de destino com o destino do Advertising Cloud DSP, conforme explicado abaixo.

### Configurar sincronização de ID para compartilhar cookies {#cookie-sync}

A sincronização de ID é um pré-requisito para compartilhar cookies de terceiros. Configure um processo de sincronização de cookie com [!DNL Web SDK] fluxos de dados ou o [!DNL Experience Cloud ID Service]. Para obter mais contexto sobre o tratamento de identidade para cookies de terceiros, consulte [Destinos do Advertising que dependem de integrações de cookies de terceiros](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Habilitar sincronização de ID de terceiros com[!DNL Web SDK]**

Se você estiver usando o [!DNL Experience Platform Web SDK], habilite a sincronização de ID de terceiros na sua sequência de dados configurando a opção [!UICONTROL Third Party ID Sync] nas configurações avançadas. Para obter instruções, consulte [Configurar opções avançadas](/help/datastreams/configure.md#advanced-options) na documentação dos fluxos de dados.

**Habilitar sincronização de ID de terceiros com o[!DNL Experience Cloud ID Service]**

Se você estiver usando [!DNL Experience Platform] tags com o [!DNL Experience Cloud ID Service], configure a sincronização de ID de terceiros usando a [extensão do Serviço da Experience Cloud ID](/help/tags/extensions/client/id-service/overview.md). Isso permite que o cookie do Adobe Advertising correspondente para a ECID fornecida esteja disponível quando você ativar o público-alvo no Real-Time CDP.

## Identidades suportadas {#supported-identities}

O destino da Adobe Advertising Cloud DSP é compatível com a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | Endereços de email com hash com o algoritmo SHA256 | O Experience Platform é compatível com texto simples e endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o Experience Platform coloque os dados em hash automaticamente na ativação. |
| `ECID` | Cookie próprio para Experience Cloud | Obrigatório para criar segmentos baseados em cookies. |
| `Everesttech cookie` | Cookie de terceiros do Adobe Advertising | Obrigatório para criar segmentos baseados em cookies. |
| `GAID` | ID do dispositivo [!DNL Android] | Necessário para direcionar [!DNL Android] dispositivos. |
| `IDFA` | ID do dispositivo [!DNL iOS] | Necessário para direcionar [!DNL iOS] dispositivos. |

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
| -------------------- | --------- | ----------- | --------- |
| [Públicos-alvo](/help/segmentation/types/people-audiences.md) | Sim | Com base nos perfis de clientes, permitindo direcionar grupos específicos de pessoas para campanhas de marketing. | Compradores frequentes, abandonadores de carrinho |
| [Públicos-alvo da conta](/help/segmentation/types/account-audiences.md) | Não | Direcione indivíduos em organizações específicas para estratégias de marketing baseadas em conta. | Marketing B2B |
| [Públicos-alvo potenciais](/help/segmentation/types/prospect-audiences.md) | Não | Direcione indivíduos que ainda não são clientes, mas compartilham características com seu público-alvo. | Prospecção com dados de terceiros |
| [Exportações do conjunto de dados](/help/catalog/datasets/overview.md) | Não | Coleções de dados estruturados armazenados no Data Lake do Adobe Experience Platform. | Relatórios, fluxos de trabalho de ciência de dados |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela a seguir para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
| ---- | ---- | ----- |
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores escolhidos. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado no Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions) para o Experience Platform. Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar ao destino, siga as instruções para [criar uma conexão de destino](/help/destinations/ui/connect-destination.md) usando a interface do usuário do Experience Platform. No workflow de configuração de destino, preencha os campos listados nas subseções abaixo.

### Autenticar para o destino {#authenticate}

Para se conectar ao destino, forneça o seguinte parâmetro na seção [!UICONTROL Connection type] e selecione **[!UICONTROL Connect to destination]**:

* **[!UICONTROL Account or Advertiser Key]**: Este [!UICONTROL Source Key] é gerado quando uma [origem do Real-Time CDP é criada na interface do usuário do DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html?lang=pt-BR). A equipe de conta da Adobe compartilhará essa chave com você após criar a fonte.

![Captura de tela da seção Tipo de conexão mostrando o campo Conta ou Chave do Anunciante.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.

![Captura de tela dos campos de detalhes de destino mostrando as entradas Nome e Descrição.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
>
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar identidades, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Mapear atributos e identidades {#map}

Você pode escolher as IDs para enviar ao Adobe Advertising DSP. Por padrão, os identificadores de cookies são selecionados para o anunciante. Você também pode optar por adicionar [!UICONTROL Hashed Email], [!UICONTROL IDFA] e [!UICONTROL GAID].

Para obter instruções, consulte [Mapear atributos e identidades](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

![Captura de tela da seção de mapeamento de identidade mostrando identificadores de cookies, email com hash, IDFA e opções de GAID.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

## Validar exportação de dados {#exported-data}

Para verificar se os dados do público-alvo foram compartilhados com a Advertising Cloud, verifique o seguinte:

* O fluxo de dados no destino [!DNL Real-Time CDP] foi bem-sucedido.

* No DSP, o público-alvo está disponível quando você cria ou edita um público-alvo de **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** ou na seção **[!UICONTROL Audience Targeting]** das configurações de posicionamento. O público deve estar visível na guia [!UICONTROL Adobe Segments], na pasta [!UICONTROL Real-Time CDP].

![Públicos-alvo do Real-Time CDP nas configurações de público-alvo do DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).

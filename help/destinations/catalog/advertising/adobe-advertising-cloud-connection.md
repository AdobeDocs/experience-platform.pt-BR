---
title: Conexão DSP da Adobe Advertising Cloud
description: A Adobe Advertising Cloud DSP é um destino integrado para o Adobe Real-Time Customer Data Platform, permitindo compartilhar públicos autenticados primários com anunciantes e usuários aprovados para ativação de campanha.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Conexão DSP da Adobe Advertising Cloud

## Visão geral {#overview}

O destino da Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) permite compartilhar públicos-alvo primários autenticados com anunciantes e usuários aprovados para ativação de campanha com o DSP. Para saber mais sobre a integração do Real-Time CDP com o DSP, consulte [Sobre a ativação de públicos autenticados de fontes de público-alvo](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Esta página foi criada pela equipe do DSP. Para qualquer consulta ou solicitação de atualização, entre em contato com o suporte da Advertising Cloud diretamente em `adcloud_support@adobe.com`.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do Advertising Cloud DSP, veja a seguir exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso de anúncio de marca

Uma retailer online deseja redirecionar seus clientes de alto valor por meio de uma campanha de exibição sem usar cookies para o direcionamento. O retailer compartilha um público-alvo que consiste nas IDs de email com hash de seus clientes de alto valor da conta do Adobe Real-Time Customer Data Platform (Real-Time CDP) para a conta do DSP. Em seguida, o DSP converte as IDs de email com hash para o [!DNL RampIDs] autenticado por meio de uma parceria entre o DSP e o LiveRamp. O [!DNL RampIDs] resultante pode ser usado em uma campanha de exibição para direcionar o público-alvo.

### Caso de uso de agência

Uma agência de mídia com uma conta do DSP está executando uma campanha de redirecionamento em nome de seu cliente, uma marca líder no setor de hotelaria e turismo. A marca quer redirecionar todos os seus convidados no último ano com uma nova oferta promocional. A marca hospeda todas as informações do convidado em [!DNL Real-Time CDP]. A marca pode compartilhar um público que consiste nas IDs de email com hash de seus convidados da conta [!DNL Real-Time CDP] para a conta DSP da agência de mídia para redirecionar os convidados por meio de uma campanha de mídia.

## Pré-requisitos {#prerequisites}

* Configurações de nível de conta e nível de campanha do DSP para habilitar o compartilhamento de público com [!DNL LiveRamp RampID], que converterá os dados do cliente em [!DNL RampIDs] para criar segmentos direcionáveis. A equipe de conta da DSP executará essa configuração. O [!DNL RampID] está disponível por meio de uma parceria entre a DSP e o [!DNL LiveRamp], e você não precisa de sua própria associação do [!DNL LiveRamp] para usá-lo.
* A ID da organização da Experience Cloud para a conta da Experience Platform. Você pode encontrar sua ID na página de perfil do usuário [!DNL Real-Time CDP].
* Uma [[!DNL Real-Time CDP] origem no DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) para receber públicos-alvo para ativação de campanha. A equipe de conta da DSP criará a origem usando a Experience Cloud ID da organização.
* A chave de origem para a conta ou anunciante do DSP, que é gerada quando uma [[!DNL Real-Time CDP] origem é criada no DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Sua equipe de conta da DSP compartilhará essa chave com você. Você o usará no Experience Platform para criar uma conexão de destino com o destino do Advertising Cloud DSP, conforme [explicado abaixo](#authenticate).
* Dados do cliente que consistem em emails ou emails com hash.

## Identidades suportadas {#supported-identities}

O destino da Adobe Advertising Cloud DSP é compatível com a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Experience Platform é compatível com texto simples e endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o Experience Platform coloque os dados em hash automaticamente na ativação. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela a seguir para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores (email ou email com hash) usados no destino da Advertising Cloud DSP. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado no Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions) para o Experience Platform. Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar ao destino, siga as instruções para [criar uma conexão de destino](/help/destinations/ui/connect-destination.md) usando a interface do usuário do Experience Platform. No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para se conectar ao destino, forneça o seguinte parâmetro na seção [!UICONTROL Connection type] e selecione **[!UICONTROL Connect to destination]**.:

* **[!UICONTROL Account or Advertiser Key]**: Este [!UICONTROL Source Key] é gerado quando uma [[!DNL Real-Time CDP] origem é criada na interface do usuário do DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). A equipe de conta da DSP compartilhará essa chave com você após criar a fonte.

![Campo de tipo de conexão](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.

![Campos de detalhes do destino](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Validar exportação de dados {#exported-data}

Para verificar se o público-alvo dos dados foi compartilhado com a Advertising Cloud, verifique o seguinte:

* O fluxo de dados no destino [!DNL Real-Time CDP] foi bem-sucedido.

* No DSP, o público-alvo está disponível quando você cria ou edita um público-alvo de [!UICONTROL Audiences] > [!UICONTROL All Audiences] ou na seção [!UICONTROL Audience Targeting] das configurações de posicionamento. O público deve estar visível na guia [!UICONTROL Adobe Segments], na pasta [!UICONTROL Real-Time CDP].

![Públicos-alvo do Real-Time CDP nas configurações de público-alvo do DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).

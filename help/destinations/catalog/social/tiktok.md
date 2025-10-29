---
title: Conexão com o TikTok
description: Crie públicos-alvo personalizados no TikTok com seus dados para direcionar com suas campanhas de publicidade. Esses públicos-alvo podem ser de pessoas que visitaram o site ou interagiram com o conteúdo. Transfira com rapidez e segurança o público-alvo desejado do Adobe Experience Platform para o TikTok usando a integração em tempo real da Adobe com o TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 3%

---

# Conexão com o TikTok

## Visão geral {#overview}

Crie públicos-alvo personalizados no TikTok com seus dados para direcionar com suas campanhas de publicidade. Esses públicos-alvo podem ser de pessoas que visitaram o site ou interagiram com o conteúdo. Transfira com rapidez e segurança o público-alvo desejado do Adobe Experience Platform para o TikTok usando a integração em tempo real da Adobe com o TikTok Ads Manager. Visite o [centro de ajuda empresarial da TikTok](https://ads.tiktok.com/help/article/audiences) para obter mais informações.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela equipe do TikTok. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino do TikTok, este é um exemplo de caso de uso para clientes do Adobe Experience Platform.

### Caso de uso {#use-case-1}

Uma marca de vestuário esportivo quer alcançar clientes existentes por meio de suas contas de mídia social. A marca de vestuário pode assimilar endereços de email de seu próprio CRM para o Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar esses públicos para o TikTok para exibir anúncios nos feeds de redes sociais de seus clientes.

## Pré-requisitos {#prerequisites}

Você precisa ter acesso de [!DNL Admin] ou [!DNL Operator] à conta do TikTok Ads Manager para a qual deseja enviar públicos-alvo. Mais instruções podem ser encontradas na [Central de Ajuda da TikTok](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Antes de enviar dados para sua conta do TikTok Ads Manager, será necessário conceder permissão ao Adobe Experience Platform para acessar sua Conta de anúncio para `Audience Management`. Esta permissão pode ser fornecida ao [inserir sua ID do Ads Manager](#authenticate) na interface do usuário do Experience Platform e conceder a permissão após ser redirecionado para sua Conta do TikTok Ads Manager.

## Identidades suportadas {#supported-identities}

O TikTok é compatível com a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. Os valores de texto sem formatação e GAID com hash SHA256 são compatíveis com o Adobe Experience Platform. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. Os valores de texto sem formatação e IDFA com hash SHA256 são compatíveis com o Adobe Experience Platform. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| Número de telefone | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform e devem estar no formato E.164. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| Email | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |
| [!DNL Federated Audience Composition] | ✓ | Públicos importados para o Experience Platform por meio da [Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino do TikTok. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, você será redirecionado para fazer logon em sua conta do [!DNL TikTok Ads Manager] e autorizar a Adobe a gerenciar públicos-alvo em seu nome.

![Seleção de permissão do TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Imagem da interface do TikTok para permissões de seleção")

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Detalhes da conexão de destino](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Imagem da interface do usuário do Experience Platform, mostrando os detalhes da conexão de destino a serem preenchidos")

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL TikTok Ads Manager ID]**: Seu [!DNL TikTok Ads Manager ID]. Você pode encontrar isso na sua conta [!DNL TikTok Ads manager].

![ID do TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Imagem da interface do usuário do TikTok Ads Manager, mostrando como obter a ID do TikTok Ads Manager")

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Mapear identidades {#map}

Veja abaixo um exemplo do mapeamento de identidade correto ao exportar públicos para o TikTok Ads Manager.

Selecionar campos de origem:

* Selecione um identificador (Por exemplo:` Email_LC_SHA256`) como identidade de origem que identifica exclusivamente um perfil no Adobe Experience Platform e [!DNL TikTok Ads Manager].

Selecionar campos de destino:

* Selecione o namespace do email como identidade de destino.

![Mapeamento de identidade](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Imagem da interface do usuário do Experience Platform, mapeamento de identidades")

## Dados exportados {#exported-data}

Verifique sua conta do [!DNL TikTok Ads Manager] (em **Assets > Públicos-alvo**) para saber se o público-alvo da Experience Platform foi exportado com êxito. O público será preenchido como um tipo de público: `Partner Audience`.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Consulte a [página da Central de ajuda da TikTok](https://ads.tiktok.com/help/article/audiences) para obter informações adicionais.

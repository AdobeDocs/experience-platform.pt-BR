---
keywords: conexão linkedin;conexão linkedin;destinos linkedin;linkedin;
title: Conexão de públicos correspondentes do Linkedin
description: Ative perfis para suas campanhas do LinkedIn para direcionamento de público, personalização e supressão, com base em emails com hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 6b3b830f822cc02c78d6f593c0a949d3e19ada37
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 3%

---

# [!DNL LinkedIn Matched Audiences] conexão

## Visão geral {#overview}

Ative perfis para suas campanhas do [!DNL LinkedIn] para direcionamento de público, personalização e supressão, com base em emails com hash e IDs de dispositivos móveis.

![Destino do LinkedIn na interface do Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ajudá-lo a entender melhor como e quando usar o destino [!DNL LinkedIn Matched Audiences], veja um caso de uso que os clientes da Adobe Experience Platform podem resolver usando esse recurso.

Uma empresa de software organiza uma conferência e deseja manter contato com os participantes, além de mostrar ofertas personalizadas com base no status de participação na conferência. A empresa pode assimilar endereços de email ou IDs de dispositivos móveis de seus próprios [!DNL CRM] na Adobe Experience Platform. Em seguida, eles podem criar públicos-alvo a partir de seus próprios dados offline e enviá-los para a plataforma social [!DNL LinkedIn], otimizando seus gastos com publicidade.

## Identidades suportadas {#supported-identities}

[!DNL LinkedIn Matched Audiences] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
>
>A partir de setembro de 2025, não será mais possível mapear [!DNL IDFA] como identidade de destino, pois [!DNL IDFA] não é mais suportado pelo destino [!DNL LinkedIn Matched Audiences]. Consulte a [!DNL LinkedIn Matched Audiences]documentação[ da integração de ](https://learn.microsoft.com/en-us/linkedin/marketing/matched-audiences/create-and-manage-segment-users?view=li-lms-2025-07&tabs=http#idtypes) para obter mais detalhes. Essa alteração se deve aos requisitos do LinkedIn e não está relacionada a nenhuma atualização de serviço de destino do Experience Platform.


| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Siga as instruções na seção [Requisitos de correspondência de ID](#id-matching-requirements-id-matching-requirements) e use os namespaces apropriados para emails com texto sem formatação e hash, respectivamente. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone e outros) usados no destino [!DNL LinkedIn Matched Audiences]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos da conta do LinkedIn {#LinkedIn-account-prerequisites}

Antes de poder usar o destino [!UICONTROL Público-alvo correspondente do LinkedIn], verifique se a sua conta [!DNL LinkedIn Campaign Manager] tem o nível de permissão [!DNL Creative Manager] ou superior.

Para saber como editar suas permissões de usuário do [!DNL LinkedIn Campaign Manager], consulte [Adicionar, Editar, e Remover Permissões de Usuário em Contas do Advertising](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

## Requisitos de correspondência de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] exige que nenhuma informação pessoal identificável (PII) seja enviada em branco. Portanto, os públicos ativados para [!DNL LinkedIn Matched Audiences] podem ser digitados de *identificadores com hash*, como endereços de email ou IDs de dispositivos móveis.

Dependendo do tipo de IDs que você assimila no Adobe Experience Platform, é necessário seguir os requisitos correspondentes.

## Requisitos de hash de email {#email-hashing-requirements}

Você pode aplicar hash a endereços de email antes de assimilá-los no Adobe Experience Platform, ou usar endereços de email em limpar no Experience Platform, e aplicar hash a [!DNL Experience Platform] neles na ativação.

Para saber mais sobre a assimilação de endereços de email no Experience Platform, consulte a [visão geral da assimilação em lote](/help/ingestion/batch-ingestion/overview.md) e a [visão geral da assimilação de streaming](/help/ingestion/streaming-ingestion/overview.md).

Se você optar por criar o hash dos endereços de email, não se esqueça de atender aos seguintes requisitos:

* Cortar todos os espaços à esquerda e à direita da cadeia de caracteres de email. Por exemplo: `johndoe@example.com`, não `<space>johndoe@example.com<space>`;
* Ao aplicar hash às cadeias de caracteres de email, certifique-se de aplicar hash à cadeia de caracteres em minúsculas;
   * Exemplo: `example@email.com`, não `EXAMPLE@EMAIL.COM`;
* Verifique se a cadeia de caracteres com hash está em minúsculas
   * Exemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, não `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Não salve a corda.

>[!NOTE]
>
>O hash automático de dados de namespaces sem hash é criado por [!DNL Experience Platform] após a ativação.
>> Os dados de origem do atributo não são automaticamente transformados em hash.
> 
> Durante a etapa [Mapeamento de Identidade](../../ui/activate-segment-streaming-destinations.md#mapping), quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação.
> 
> A opção **[!UICONTROL Aplicar transformação]** é exibida somente quando você seleciona atributos como campos de origem. Ela não é exibida ao escolher namespaces.

![Transformação de mapeamento de identidade](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

O vídeo abaixo também demonstra as etapas para configurar um destino do [!DNL LinkedIn Matched Audiences] e ativar públicos-alvo.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>A interface do usuário do Experience Platform é atualizada com frequência e pode ter sido alterada desde a gravação deste vídeo. Para obter as informações mais atualizadas, consulte o [tutorial de configuração de destino](../../ui/connect-destination.md).

### Autenticar para o destino {#authenticate}

1. Localize o destino [!DNL LinkedIn Matched Audiences] no catálogo de destino e selecione **[!UICONTROL Configurar]**.
2. Selecione **[!UICONTROL Conectar ao destino]**.
   ![Autenticar para o LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Insira suas credenciais do LinkedIn e selecione **Fazer logon**.

### Atualizar credenciais de autenticação {#refresh-authentication-credentials}

Os tokens do LinkedIn expiram a cada 60 dias. É possível monitorar as datas de expiração do token a partir da coluna **[!UICONTROL Data de expiração da conta]** nas guias **[[!UICONTROL Contas]](../../ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Procurar]](../../ui/destinations-workspace.md#browse)**.

Quando o token expira, as exportações de dados para o destino param de funcionar. Para evitar essa situação, autentique novamente executando as seguintes etapas:

1. Navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Contas]**
2. (Opcional) Use os filtros disponíveis na página para exibir somente contas do LinkedIn.
   ![Filtrar para mostrar somente contas do LinkedIn](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-filters.png)
3. Selecione a conta que deseja atualizar, selecione as reticências e selecione **[!UICONTROL Editar detalhes]**.
   ![Selecionar controle de detalhes de Edição](/help/destinations/assets/catalog/social/linkedin/refresh-oauth-edit-details.png)
4. Na janela modal, selecione **[!UICONTROL Reconectar OAuth]** e autenticar novamente com suas credenciais do LinkedIn.
   ![Janela modal com opção Reconectar OAuth](/help/destinations/assets/catalog/social/linkedin/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Suas credenciais de autenticação são atualizadas e o tempo de expiração é redefinido para 60 dias.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID da conta"
>abstract="Sua ID da conta do Campaign Manager no LinkedIn. Você pode encontrar essa ID na conta do Campaign Manager do LinkedIn."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL ID da Conta]**: Seu [!DNL LinkedIn Campaign Manager Account ID]. Você pode encontrar essa ID na sua conta do [!DNL LinkedIn Campaign Manager].

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados {#exported-data}

Uma ativação bem-sucedida significa que um público-alvo personalizado [!DNL LinkedIn] é criado programaticamente em [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). A associação de público é ajustada conforme os usuários são qualificados ou desqualificados para os públicos ativados.

>[!TIP]
>
>A integração entre o Adobe Experience Platform e o [!DNL LinkedIn Matched Audiences] oferece suporte a preenchimentos retroativos de público-alvo histórico. Todas as qualificações históricas de público são enviadas para [!DNL LinkedIn] quando você ativa os públicos para o destino.

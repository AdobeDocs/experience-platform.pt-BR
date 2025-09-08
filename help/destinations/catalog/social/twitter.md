---
title: Conexão de públicos-alvo personalizados do Twitter
description: Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 5b529a1af62c2745c3226029de1a1ff508bddfc7
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 4%

---

# [!DNL Twitter Custom Audiences] conexão

## Visão geral {#overview}

>[!IMPORTANT]
>
>* A partir de 9 de setembro de 2025, você poderá ver dois cartões **[!DNL Twitter Custom Audiences]** lado a lado no catálogo de destinos. Isso se deve a uma atualização interna do serviço de destinos. O conector de destino **[!DNL Twitter Custom Audiences]** existente foi renomeado para **[!UICONTROL (obsoleto) Públicos-alvo personalizados do Twitter]** e um novo cartão com o nome **[!UICONTROL Públicos-alvo personalizados do Twitter]** está disponível para você.
>* Use a nova conexão **[!UICONTROL Públicos-alvo personalizados do Twitter]** no catálogo para novos fluxos de dados de ativação. Se você tiver fluxos de dados ativos para o destino **[!UICONTROL (obsoleto) de Públicos-alvo personalizados do Twitter]**, eles serão atualizados automaticamente; portanto, nenhuma ação é necessária.
>* Se você estiver criando fluxos de dados por meio da [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/), atualize o [!DNL flow spec ID] e o [!DNL connection spec ID] para os seguintes valores:
>   * ID da especificação de fluxo: `903da9e4-7cf5-442a-9498-a237e4f064f9`
>   * ID de especificação da conexão: `9eb18875-a095-4b89-854e-39b9e29ccd41`

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Antes de configurar o destino do [!DNL Twitter Custom Audiences], verifique os seguintes pré-requisitos do Twitter que você precisa atender.

1. Sua conta [!DNL Twitter Ads] deve ser qualificada para publicidade. As novas contas do [!DNL Twitter Ads] não estão qualificadas para publicidade nas primeiras 2 semanas após sua criação.
2. Sua conta de usuário do Twitter para a qual você autorizou o acesso no [!DNL Twitter Audience Manager] deve ter a permissão *[!DNL Partner Audience Manager]* habilitada.

## Identidades suportadas {#supported-identities}

[!DNL Twitter Custom Audiences] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| device_id | ID IDFA/AdID/Android | A Google Advertising ID (GAID) e a Apple ID para anunciantes (IDFA) são compatíveis com o Adobe Experience Platform. Mapeie esses namespaces e/ou atributos do esquema de origem de acordo na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino. |
| email | Endereço(s) de email do usuário | Mapeie seus endereços de email de texto sem formatação e seus endereços de email com hash SHA256 para este campo. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Aplicar transformação]** para que [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. Se você colocar seus endereços de email de clientes em hash antes de fazer upload para o Adobe Experience Platform, observe que essas identidades devem ser colocadas em hash usando SHA256, sem um salt. |

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
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público-alvo com os identificadores usados no destino de Públicos-alvo personalizados do Twitter. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Twitter Custom Audiences], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform como [!DNL List Custom Audiences] no Twitter.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

1. Localize o destino [!DNL Twitter Custom Audiences] no catálogo de destino e selecione **[!UICONTROL Configurar]**.
2. Selecione **[!UICONTROL Conectar ao destino]**.
   ![Autenticar para o LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Insira suas credenciais do Twitter e selecione **Fazer Logon**.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID da conta"
>abstract="Sua ID da conta do Twitter Ads. Pode ser encontrada nas configurações do Twitter Ads."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL ID da conta]**: sua ID da conta [!DNL Twitter Ads]. Isso pode ser encontrado nas configurações do [!DNL Twitter Ads].

>[!IMPORTANT]
>
>Não usar caracteres especiais (+ &amp; , % : ; @ / = ? $ \n) nos nomes de público, descrição e mapeamento de público. Se o nome do público-alvo do Experience Platform contiver esses caracteres, remova-os antes de mapear o público-alvo para um destino do Twitter.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Considerações de mapeamento {#mapping-considerations}

Ao mapear públicos para o Twitter, forneça nomes de mapeamento de públicos legíveis. Recomendamos usar o mesmo nome usado para os segmentos do Experience Platform.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Mais informações sobre [!DNL List Custom Audiences] no Twitter podem ser encontradas na [documentação do Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).

---
title: Conexão com a Lista de clientes do Pinterest
description: Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 1b35687350dbbcebfc86acc90852d86870292142
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] conexão

## Visão geral {#overview}

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

>[!IMPORTANT]
>
>Esse destino foi criado pela equipe do Pinterest. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em https://help.pinterest.com/en/contact.

## Pré-requisitos {#prerequisites}

* O usuário precisaria se autenticar em uma conta do Pinterest que tem acesso à conta do anunciante à qual deseja adicionar um público-alvo. Detalhes sobre o compartilhamento de contas de anunciante podem ser encontrados [aqui](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Especificamente, o usuário precisaria dos níveis de acesso de &quot;público-alvo&quot;.
* Detalhes sobre os formatos de identidade da lista de clientes podem ser encontrados [aqui](https://help.pinterest.com/en/business/article/audience-targeting).

## Identidades suportadas {#supported-identities}

O destino [!DNL Pinterest Customer List] dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR#getting-started).

Na [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino, mapeie as identidades desejadas para o campo de destino *pinterest_audience*. As identidades são diferenciadas e resolvidas após a assimilação de dados na Pinterest.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mapeie o namespace de identidade de origem *GAID* para o campo de identidade de destino *pinterest_audience*. |
| IDFA | [!DNL Apple ID for Advertisers] | Mapeie o namespace de identidade de origem *IDFA* para o campo de identidade de destino *pinterest_audience*. |
| EMAIL | Endereços de email (texto limpo ou hash com o algoritmo SHA256) | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. <br> Mapeie o namespace de identidade de origem *Email* ou *Email_LC_SHA256* para o campo de identidade de destino *pinterest_audience*. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no destino da Lista de clientes do Pinterest. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Pinterest Customer List], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL ID da conta do anúncio]**: sua ID de anunciante do Pinterest.

### Atualizar credenciais de autenticação {#refresh-authentication-credentials}

Os tokens do Pinterest expiram a cada 30 dias. É possível monitorar as datas de expiração do token a partir da coluna **[!UICONTROL Data de expiração da conta]** nas guias **[[!UICONTROL Contas]](../../ui/destinations-workspace.md#accounts)** ou **[[!UICONTROL Procurar]](../../ui/destinations-workspace.md#browse)**.

Quando o token expira, as exportações de dados para o destino param de funcionar. Para evitar essa situação, autentique novamente executando as seguintes etapas:

1. Navegue até **[!UICONTROL Destinos]** > **[!UICONTROL Contas]**
2. (Opcional) Use os filtros disponíveis na página para exibir somente contas do Pinterest.
   ![Filtrar para mostrar apenas contas do Pinterest](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-filters.png)
3. Selecione a conta que deseja atualizar, selecione as reticências e selecione **[!UICONTROL Editar detalhes]**.
   ![Selecionar controle de detalhes de Edição](/help/destinations/assets/catalog/advertising/pinterest-customer-list/refresh-oauth-edit-details.png)
4. Na janela modal, selecione **[!UICONTROL Reconectar OAuth]** e autenticar novamente com suas credenciais do Pinterest.
   ![Janela modal com opção Reconectar OAuth](/help/destinations/assets/catalog/advertising/pinterest-customer-list/reconnect-oauth-control.png)

>[!SUCCESS]
> 
>Suas credenciais de autenticação são atualizadas e o tempo de expiração é redefinido para 30 dias.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Consulte a [página da Central de ajuda da Pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obter informações adicionais.

+++ Exibir changelog


| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Novembro de 2023 | Atualização de funcionalidade e documentação | O destino do Pinterest no Real-Time CDP agora usa a API v5 do anunciante. |

{style="table-layout:auto"}


+++

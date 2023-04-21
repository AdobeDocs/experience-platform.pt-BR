---
title: Conexão de públicos-alvo personalizados do twitter
description: Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# [!DNL Twitter Custom Audiences] conexão

## Visão geral {#overview}

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Antes de configurar o [!DNL Twitter Custom Audiences] de destino, verifique os pré-requisitos do Twitter a seguir que você precisa atender.

1. Seu [!DNL Twitter Ads] deve ser elegível para publicidade. Novo [!DNL Twitter Ads] as contas não são elegíveis para publicidade nas primeiras 2 semanas após a sua criação.
2. Sua conta de usuário do Twitter para a qual você autorizou o acesso no [!DNL Twitter Audience Manager] deve ter o *[!DNL Partner Audience Manager]* permissão ativada.

## Identidades suportadas {#supported-identities}

[!DNL Twitter Custom Audiences] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| device_id | IDFA/AdID/Android ID | A Google Advertising ID (GAID) e a Apple ID for Advertisers (IDFA) são compatíveis com o Adobe Experience Platform. Mapeie esses namespaces e/ou atributos do esquema de origem de acordo com a variável [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino. |
| email | Endereço(s) de email do usuário | Mapeie seus endereços de email de texto simples e seus endereços de email com hash SHA256 para este campo. Quando o campo de origem contém atributos com hash, verifique a **[!UICONTROL Aplicar transformação]** , para ter [!DNL Platform] fazer o hash automático dos dados na ativação. Caso envie hash nos endereços de email do cliente antes de carregá-los no Adobe Experience Platform, observe que essas identidades devem ser transformadas em hash usando SHA256, sem sal. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores usados no destino Públicos-alvo personalizados do Twitter. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Twitter Custom Audiences] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform as [!DNL List Custom Audiences] no Twitter.

## Ligar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

1. Encontre a [!DNL Twitter Custom Audiences] no catálogo de destino e selecione **[!UICONTROL Configurar]**.
2. Selecionar **[!UICONTROL Ligar ao destino]**.
   ![Autenticar para o LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Insira suas credenciais do Twitter e selecione **Fazer logon**.

### Preencha os detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID da conta"
>abstract="Sua ID da conta do Twitter Ads. Pode ser encontrada nas configurações do Twitter Ads."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Twitter Ads] ID da conta. Isso pode ser encontrado no [!DNL Twitter Ads] configurações.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Ao mapear segmentos de público-alvo para o Twitter, atenda aos seguintes requisitos de nomenclatura de segmento:

1. Forneça nomes de mapeamento de segmentos legíveis ao ser humano. Recomendamos o uso do mesmo nome usado para os segmentos do Experience Platform.
2. Não use caracteres especiais (+ &amp; , % : ; @ / = ? $) em nomes de mapeamento de segmento e segmento. Se o nome do seu segmento de Experience Platform contém esses caracteres, remova-os antes de mapear o segmento para um destino Twitter.

Mais informações sobre [!DNL List Custom Audiences] no Twitter , é possível encontrar no [Documentação do twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).

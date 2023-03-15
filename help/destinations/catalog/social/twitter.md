---
title: Conexão com o twitter Custom Audiences
description: Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 2%

---

# [!DNL Twitter Custom Audiences] conexão

## Visão geral {#overview}

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando seus públicos-alvo criados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Antes de configurar seu [!DNL Twitter Custom Audiences] destino, revise os seguintes pré-requisitos do Twitter que você precisa atender.

1. Seu [!DNL Twitter Ads] deve ser elegível para publicidade. Novo [!DNL Twitter Ads] as contas do não estarão qualificadas para publicidade nas primeiras 2 semanas após sua criação.
2. Sua conta de usuário do Twitter para a qual você autorizou o acesso no [!DNL Twitter Audience Manager] deve ter a *[!DNL Partner Audience Manager]* permissão ativada.

## Identidades suportadas {#supported-identities}

[!DNL Twitter Custom Audiences] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| device_id | ID IDFA/AdID/Android | A Google Advertising ID (GAID) e a Apple ID para anunciantes (IDFA) são compatíveis com o Adobe Experience Platform. Mapeie esses namespaces e/ou atributos do esquema de origem de acordo com a [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do workflow de ativação de destino. |
| email | Endereço(s) de email do usuário | Mapeie seus endereços de email de texto sem formatação e seus endereços de email com hash SHA256 para este campo. Quando o campo de origem contiver atributos sem hash, verifique a **[!UICONTROL Aplicar transformação]** opção, para ter [!DNL Platform] coloque automaticamente os dados em hash na ativação. Se você colocar seus endereços de email de clientes em hash antes de fazer upload para o Adobe Experience Platform, observe que essas identidades devem ser colocadas em hash usando SHA256, sem um salt. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores usados no destino dos Públicos-alvo personalizados do Twitter. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Twitter Custom Audiences] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Direcione seus seguidores e clientes existentes no Twitter e crie campanhas de re-marketing relevantes ativando os públicos-alvo criados no Adobe Experience Platform como [!DNL List Custom Audiences] no Twitter.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

1. Localize o [!DNL Twitter Custom Audiences] no catálogo de destino e selecione **[!UICONTROL Configurar]**.
2. Selecionar **[!UICONTROL Conectar ao destino]**.
   ![Autenticar no LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Insira suas credenciais do Twitter e selecione **Fazer logon**.

### Preencher detalhes do destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID da Conta"
>abstract="A ID da sua conta do Twitter Ads. Isso pode ser encontrado nas configurações do Twitter Ads."

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Twitter Ads] ID da conta. Isso pode ser encontrado no seu [!DNL Twitter Ads] configurações.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=pt-BR).

## Recursos adicionais {#additional-resources}

Ao mapear segmentos de público-alvo para o Twitter, certifique-se de atender aos seguintes requisitos de nomenclatura de segmento:

1. Forneça nomes de mapeamento de segmento legíveis por humanos. Recomendamos usar o mesmo nome usado para os segmentos Experience Platform.
2. Não usar caracteres especiais (+ &amp; , % : ; @ / = ? $) nos nomes de segmento e mapeamento de segmento. Se o nome do segmento Experience Platform contiver esses caracteres, remova-os antes de mapear o segmento para um destino Twitter.

Mais informações sobre [!DNL List Custom Audiences] no Twitter pode ser encontrado na [Documentação do twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).

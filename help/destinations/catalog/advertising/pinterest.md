---
title: Conexão com a Lista de clientes do pinterest
description: Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] conexão

## Visão geral {#overview}

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

>[!IMPORTANT]
>
>Esse destino foi criado pela equipe do Pinterest. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em https://help.pinterest.com/en/contact.

## Pré-requisitos {#prerequisites}

* O usuário precisaria se autenticar em uma conta do Pinterest que tem acesso à conta do anunciante à qual deseja adicionar um público-alvo. É possível encontrar detalhes sobre o compartilhamento de contas de anunciante [aqui](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Especificamente, o usuário precisaria dos níveis de acesso de &quot;público-alvo&quot;.
* É possível encontrar detalhes sobre os formatos de identidade da lista de clientes [aqui](https://help.pinterest.com/en/business/article/audience-targeting).

## Identidades suportadas {#supported-identities}

A variável [!DNL Pinterest Customer List] o destino oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

No [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do workflow de ativação de destino, mapeie as identidades desejadas para o campo de destino *pinterest_audience*. As identidades são diferenciadas e resolvidas após a assimilação de dados na Pinterest.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mapeie o *GAID* namespace de identidade de origem para o campo de identidade de destino *pinterest_audience*. As identidades são diferenciadas e resolvidas após a assimilação de dados na Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mapeie o *IDFA* namespace de identidade de origem para o campo de identidade de destino *pinterest_audience*. As identidades são diferenciadas e resolvidas após a assimilação de dados na Pinterest. |
| EMAIL | Endereços de email (texto limpo ou hash com o algoritmo SHA256) | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. <br> Mapeie o *E-mail* ou *Email_LC_SHA256* namespace de identidade de origem para o campo de identidade de destino *pinterest_audience*. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino da Lista de clientes do Pinterest. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Pinterest Customer List] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante]**: a ID do anunciante do Pinterest.

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

Consulte a seção [Página Central de ajuda do pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obter informações adicionais.

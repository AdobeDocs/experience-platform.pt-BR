---
title: Conexão da Lista de clientes do pinterest
description: Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] conexão

## Visão geral {#overview}

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

>[!IMPORTANT]
>
>Esse destino foi criado pela equipe do Pinterest. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em https://help.pinterest.com/en/contact.

## Pré-requisitos {#prerequisites}

* O usuário precisaria se autenticar com uma conta do Pinterest que tenha acesso à conta do anunciante à qual deseja adicionar um público-alvo. Detalhes sobre o compartilhamento de contas de anunciante podem ser encontrados [here](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Especificamente, o usuário precisaria dos níveis de acesso de &quot;público-alvo&quot;.
* Detalhes sobre os formatos de identidade da lista de clientes podem ser encontrados [here](https://help.pinterest.com/en/business/article/audience-targeting).

## Identidades suportadas {#supported-identities}

O [!DNL Pinterest Customer List] O destino oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

No [etapa de mapeamento](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) do fluxo de trabalho de ativação de destino, mapeie as identidades desejadas para o campo de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Mapeie o *GAID* namespace da identidade de origem para o campo de identidade de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Mapeie o *IDFA* namespace da identidade de origem para o campo de identidade de destino *pinterest_audience*. As identidades são distintas e resolvidas após a assimilação de dados no Pinterest. |
| EMAIL | Endereços de email (texto limpo ou com hash com o algoritmo SHA256) | O Adobe Experience Platform oferece suporte para texto sem formatação e endereços de email com hash SHA256. <br> Mapeie o *Email* ou *Email_LC_SHA256* namespace da identidade de origem para o campo de identidade de destino *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados no destino da Lista de clientes do Pinterest. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Pinterest Customer List] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Crie públicos-alvo com base em suas listas de clientes, pessoas que visitaram seu site ou pessoas que já interagiram com seu conteúdo no Pinterest.

## Ligar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID do anunciante]**: Sua ID de anunciante da Pinterest.

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

Consulte a [Página da Central de ajuda do pinterest](https://help.pinterest.com/en/business/article/audience-targeting) para obter mais informações.

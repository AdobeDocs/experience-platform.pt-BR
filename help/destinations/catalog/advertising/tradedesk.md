---
keywords: publicidade; o serviço de comércio; suporte comercial de anúncios
title: A conexão com o Trade Desk
description: O Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de exibição, vídeo e inventário móvel.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 3%

---

# [!DNL The Trade Desk] conexão

## Visão geral {#overview}

[!DNL The Trade Desk] O destino ajuda a enviar dados de perfil para o [!DNL The Trade Desk].

[!DNL The Trade Desk] O é uma plataforma de autoatendimento para compradores de anúncios executarem campanhas digitais direcionadas ao público-alvo por meio de exibição, vídeo e fontes de inventário móvel.

Para enviar dados de perfil para o [!DNL Trade Desk], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, desejo poder usar segmentos criados [!DNL Trade Desk IDs] ou IDs de dispositivo para criar redirecionamento ou campanhas digitais direcionadas ao público-alvo.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| A ID do Trade Desk | ID do anunciante na plataforma do Trade Desk |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) para o destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com [!DNL The Trade Desk] e não ativou a variável [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL The Trade Desk] integrações no Audience Manager, as sincronizações de ID que você configurou continuam para a Platform.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Trade Desk] [!UICONTROL ID da conta].
* **[!UICONTROL Local do servidor]**: Pergunte ao seu [!DNL Trade Desk] representante de qual servidor regional você deve usar. Esses são os servidores regionais disponíveis que você pode escolher:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapura]**
   * **[!UICONTROL Tóquio]**
   * **[!UICONTROL América do Norte - Leste]**
   * **[!UICONTROL América do Norte - Oeste]**
   * **[!UICONTROL América Latina]**

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

No [Agendamento do segmento](../../ui/activate-segment-streaming-destinations.md#scheduling) , você deve mapear manualmente os segmentos para a ID correspondente ou o nome amigável na plataforma de destino.

Ao mapear segmentos, recomendamos que você use o nome de segmento da Plataforma ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID do segmento ou o nome no seu destino não precisam corresponder ao nome na sua conta da plataforma. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

Se estiver usando vários mapeamentos de dispositivo (IDs de cookie, [!DNL IDFA], [!DNL GAID]), certifique-se de usar o mesmo valor de mapeamento para todos os três mapeamentos. [!DNL The Trade Desk] O agregará todos em um único segmento, com um detalhamento em nível de dispositivo.

![ID de mapeamento de segmento](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL The Trade Desk] destino, verifique seu [!DNL Trade Desk] conta. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.

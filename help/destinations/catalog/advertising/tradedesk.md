---
keywords: publicidade; o serviço de comércio; suporte comercial de anúncios
title: A conexão com o Trade Desk
description: O Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de exibição, vídeo e inventário móvel.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 2%

---

# [!DNL The Trade Desk] conexão

## Visão geral {#overview}

[!DNL The Trade Desk] ajuda a enviar dados do perfil para o  [!DNL The Trade Desk].

[!DNL The Trade Desk] O é uma plataforma de autoatendimento para compradores de anúncios executarem campanhas digitais direcionadas ao público-alvo por meio de exibição, vídeo e fontes de inventário móvel.

Para enviar dados de perfil para [!DNL Trade Desk], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, desejo poder usar segmentos criados a partir de [!DNL Trade Desk IDs] ou IDs de dispositivo para criar redirecionamento ou campanhas digitais direcionadas ao público-alvo.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| A ID do Trade Desk | ID do anunciante na plataforma do Trade Desk |

## Tipo de exportação {#export-type}

**[!DNL Segment export]** - você está exportando todos os membros de um segmento (público-alvo) para o destino.

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com [!DNL The Trade Desk] e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL The Trade Desk] integrações no Audience Manager, as sincronizações de ID que você havia configurado continuam para a Platform.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Sua ID  [!DNL Trade Desk] [!UICONTROL de conta].
* **[!UICONTROL Local]** do servidor: Pergunte ao seu  [!DNL Trade Desk] representante qual servidor regional você deve usar. Esses são os servidores regionais disponíveis que você pode escolher:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapura]**
   * **[!UICONTROL Tóquio]**
   * **[!UICONTROL América do Norte - Leste]**
   * **[!UICONTROL América do Norte - Oeste]**
   * **[!UICONTROL América Latina]**

## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

Na etapa [Agendamento do segmento](../../ui/activate-segment-streaming-destinations.md#scheduling), você deve mapear manualmente os segmentos para a ID correspondente ou para o nome amigável na plataforma de destino.

Ao mapear segmentos, recomendamos que você use o nome de segmento da Plataforma ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID do segmento ou o nome no seu destino não precisam corresponder ao nome na sua conta da plataforma. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

Se estiver usando vários mapeamentos de dispositivo (IDs de cookie, [!DNL IDFA], [!DNL GAID]), certifique-se de usar o mesmo valor de mapeamento para todos os três mapeamentos. [!DNL The Trade Desk] O agregará todos em um único segmento, com um detalhamento em nível de dispositivo.

![ID de mapeamento de segmento](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL The Trade Desk], verifique sua conta [!DNL Trade Desk]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.

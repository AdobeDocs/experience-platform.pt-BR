---
keywords: 'publicidade; bing; '
title: Conexão do Microsoft Bing
description: Com o destino de conexão do Microsoft Bing, você pode executar redirecionamento e campanhas digitais direcionadas ao público-alvo em todo o Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# [!DNL Microsoft Bing] conexão {#bing-destination}

## Visão geral {#overview}

O destino [!DNL Microsoft Bing] ajuda a enviar os dados do perfil para [!DNL Microsoft Display Advertising].

Para enviar dados de perfil para [!DNL Microsoft Bing], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, eu desejo poder usar segmentos criados a partir de [!DNL Microsoft Advertising IDs] para direcionar usuários por meio de publicidade de exibição em [!DNL Microsoft Advertising] canais.

## Identidades suportadas {#supported-identities}

[!DNL Microsoft Bing] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| MAID | ID de publicidade da Microsoft |

## Tipo de exportação {#export-type}

**[!DNL Segment Export]** - você está exportando todos os membros de um segmento (público-alvo) para o  [!DNL Microsoft Bing] destino.

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com [!DNL Microsoft Bing] e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL Microsoft Bing] integrações no Audience Manager, as sincronizações de ID que você havia configurado continuam para a Platform.

Ao configurar o destino, você deve fornecer as seguintes informações:

* [!UICONTROL ID] da conta: este é seu  [!DNL Bing Ads CID], no formato inteiro.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID]** da conta: Seu  [!DNL Bing Ads CID].

## Ativar segmentos para este destino {#activate}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

Na etapa [Agendamento do segmento](../../ui/activate-destinations.md#segment-schedule), você deve mapear manualmente os segmentos para a ID correspondente ou para o nome amigável no destino.

Ao mapear segmentos, recomendamos que você use o nome do segmento [!DNL Platform] ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID do segmento ou o nome no seu destino não precisam corresponder àquela em sua conta [!DNL Platform]. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Microsoft Bing], verifique sua conta [!DNL Microsoft Bing Ads]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.

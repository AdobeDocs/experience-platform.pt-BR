---
keywords: publicidade; a trade desk; advertising trade desk
title: A conexão com a Trade Desk
description: A Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais direcionadas por público e redirecionamento em fontes de inventário para exibição, vídeo e dispositivos móveis.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 1c9725c108d55aea5d46b086fbe010ab4ba6cf45
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 1%

---

# [!DNL The Trade Desk] conexão

## Visão geral {#overview}

[!DNL The Trade Desk] O destino ajuda a enviar dados de perfil para o [!DNL The Trade Desk].

[!DNL The Trade Desk] O é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais direcionadas por público e redirecionamento em fontes de inventário para exibição, vídeo e dispositivos móveis.

Para enviar dados de perfil para [!DNL Trade Desk], você deve primeiro se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, quero poder usar públicos-alvo criados com o [!DNL Trade Desk IDs] ou IDs de dispositivo para criar campanhas digitais direcionadas por redirecionamento ou público-alvo.

## Identidades suportadas {#supported-identities}

[!DNL The Trade Desk] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| A ID da Trade Desk | ID do anunciante na plataforma Trade Desk |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Todos os destinos oferecem suporte à ativação de públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

Além disso, esse destino também suporta a ativação dos públicos-alvo descritos na tabela abaixo.

| Tipo de público | Descrição |
---------|----------|
| Uploads personalizados | Públicos-alvo assimilados em Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo para o destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o [!DNL The Trade Desk] e não ativaram o [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID de Experience Cloud no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Consultoria de Adobe ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já configurou o [!DNL The Trade Desk] integrações no Audience Manager, as sincronizações de ID configuradas para serem transferidas para a Platform.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Trade Desk] [!UICONTROL ID da conta].
* **[!UICONTROL Local do servidor]**: Pergunte ao seu [!DNL Trade Desk] representante que servidor regional você deve usar. Estes são os servidores regionais disponíveis que você pode escolher:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapura]**
   * **[!UICONTROL Tóquio]**
   * **[!UICONTROL Leste da América do Norte]**
   * **[!UICONTROL Oeste da América do Norte]**
   * **[!UICONTROL América Latina]**

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

No [Programação de público](../../ui/activate-segment-streaming-destinations.md#scheduling) etapa, mapeie manualmente os públicos-alvo à ID correspondente ou ao nome amigável na plataforma de destino.

Ao mapear segmentos, recomendamos usar o nome de público-alvo da Platform ou uma forma mais curta, para facilitar o uso. No entanto, a ID ou o nome do público-alvo no seu destino não precisa corresponder ao da sua conta da Platform. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

Se estiver usando vários mapeamentos de dispositivo (IDs de cookie, [!DNL IDFA], [!DNL GAID]), use o mesmo valor de mapeamento para todos os três mapeamentos. [!DNL The Trade Desk] A agregará todos eles em um único segmento, com um detalhamento no nível do dispositivo.

![ID do mapeamento de segmentos](../../assets/common/segment-mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com sucesso para o [!DNL The Trade Desk] destino, verifique seu [!DNL Trade Desk] conta. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

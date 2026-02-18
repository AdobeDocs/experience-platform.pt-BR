---
keywords: publicidade; a trade desk; advertising trade desk
title: A conexão com a Trade Desk
description: A Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais de redirecionamento e direcionadas por público-alvo em origens de inventário de exibição, vídeo e dispositivos móveis.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 2%

---

# [!DNL The Trade Desk] conexão

## Visão geral {#overview}

Use este conector de destino para enviar dados de perfil para [!DNL The Trade Desk]. Este conector envia dados para o ponto de extremidade primário [!DNL The Trade Desk]. A integração entre o Adobe Experience Platform e o [!DNL The Trade Desk] não oferece suporte à exportação de dados para o ponto de extremidade de terceiros [!DNL The Trade Desk].

O [!DNL The Trade Desk] é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais com direcionamento de público e redirecionamento em fontes de inventário para dispositivos móveis, vídeo e exibição.

Para enviar dados de perfil para [!DNL The Trade Desk], primeiro você deve se conectar ao destino, conforme descrito nas seções a seguir desta página.

## Casos de uso {#use-cases}

Como profissional de marketing, quero poder usar públicos-alvo criados a partir do [!DNL Trade Desk IDs] ou de IDs de dispositivo para criar campanhas digitais de redirecionamento ou direcionadas por público-alvo.

## Identidades suportadas {#supported-identities}

O [!DNL The Trade Desk] dá suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

Abaixo estão as identidades suportadas pelo destino [!DNL The Trade Desk]. Essas identidades podem ser usadas para ativar públicos para [!DNL The Trade Desk].

Todas as identidades na tabela abaixo são pré-configuradas e mapeadas automaticamente durante a ativação. Não é necessário configurar manualmente esses mapeamentos no fluxo de trabalho de ativação.

| Identidade do público alvo | Descrição | Considerações |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Ativado quando um GAID estiver presente no perfil. |
| IDFA | Apple ID para anunciantes | Ativado quando um IDFA está presente no perfil. |
| ECID | Experience Cloud ID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Leia o seguinte documento na [ECID](/help/identity-service/features/ecid.md) para obter mais informações. |
| [!DNL Tradedesk] | [!DNL TDID] na plataforma [!DNL The Trade Desk] | Ativado quando um perfil tiver uma ECID e houver um mapeamento de ECID para Trade Desk na Experience Platform. |

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
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo para o destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Os pré-requisitos dependem dos tipos de identidade que você planeja usar para a ativação do público-alvo:

**Somente para ativação da ID móvel**, não há pré-requisitos. Desde que você esteja coletando e gerenciando IDs (GAID e/ou IDFA) para seus clientes, é possível começar a ativar públicos para [!DNL The Trade Desk].

**Para o direcionamento baseado em cookies em[!DNL The Trade Desk]**, verifique se foi estabelecido um mapeamento entre a ECID e [!DNL Trade Desk ID]. Conclua as etapas abaixo para fazer isso:

1. **Habilitar a funcionalidade de sincronização de ID**: se esta for a primeira vez que você configura a ativação do [!DNL The Trade Desk ID] e não habilitou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/pt-br/docs/id-service/using/id-service-api/methods/idsync) no Serviço da Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), contate a Adobe Consulting ou o Atendimento ao Cliente para habilitar as sincronizações de ID.
   * Se você tiver configurado previamente as integrações do [!DNL The Trade Desk] no Audience Manager, as sincronizações de ID existentes serão automaticamente transferidas para o Experience Platform.

2. **Instrumentar suas páginas da Web**: implemente o código em suas páginas da Web para criar mapeamentos entre o [!DNL The Trade Desk ID] e a Adobe ECID. Isso permite que o Experience Platform associe IDs da Trade Desk aos perfis do cliente.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Account ID]**: Seu [!DNL The Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Pergunte ao representante do [!DNL The Trade Desk] qual servidor regional você deve usar. Abaixo estão os servidores regionais disponíveis que você pode escolher:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

Na etapa [Agenda de público-alvo](../../ui/activate-segment-streaming-destinations.md#scheduling), mapeie manualmente os públicos-alvo para a ID correspondente ou nome amigável na plataforma de destino.

Ao mapear públicos-alvo, a Adobe recomenda usar o nome do público-alvo do Experience Platform ou uma forma mais curta dele, para facilitar o uso. No entanto, a ID ou o nome do público-alvo no seu destino não precisa corresponder ao da sua conta do Experience Platform. Qualquer valor inserido no campo de mapeamento será refletido pelo destino.

### Mapeamentos pré-configurados {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Conjuntos de mapeamento pré-configurados"
>abstract="Pré-configuramos esses quatro conjuntos de mapeamento para você. Quando você ativa dados para a Trade Desk, os perfis qualificados para os públicos ativados não precisam necessariamente ter todas as quatro identidades presentes nos perfis, pois esse destino funcionará com qualquer uma das identidades de destino mostradas aqui. <br> Para direcionamento baseado em cookies e baseado na Trade Desk ID, é necessário ter a ECID presente no perfil e um mapeamento de sincronização de ID entre a Trade Desk ID e a ECID."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="Leia mais sobre os mapeamentos pré-configurados"

Os seguintes mapeamentos de identidade são **pré-configurados e preenchidos automaticamente** para você no fluxo de trabalho de ativação de público-alvo:

* GAID (Google Advertising ID)
* IDFA (Apple ID para anunciantes)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Captura de tela mostrando os mapeamentos obrigatórios](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

Esses mapeamentos estão esmaecidos e são somente leitura. Não é necessário configurar nada nesta etapa. Selecione **[!UICONTROL Next]** para continuar.

O Experience Platform verifica automaticamente todos os perfis que pertencem a públicos mapeados no fluxo de trabalho de ativação para todos os tipos de identidade compatíveis e ativa o perfil usando as identidades presentes.

### Requisitos de identidade por tipo de ativação

**Ativação de ID de dispositivo móvel (GAID/IDFA):** Perfis com apenas GAID ou IDFA são suficientes para ativação. Nenhuma identidade ou pré-requisito adicional é necessário.

**Direcionamento baseado em cookies ([!DNL Trade Desk ID]):** Requer ambos:

* ECID presente no perfil
* Um mapeamento de sincronização de ID entre o [!DNL Trade Desk ID] e a ECID (configurado conforme descrito na seção [pré-requisitos](#prerequisites))

**Comportamento de várias IDs:** Se um perfil contiver várias identidades com suporte, cada identidade será ativada separadamente para [!DNL The Trade Desk]. Isso garante o máximo de alcance e flexibilidade na ativação do público-alvo.

### Exemplos de ativação

* **Perfis de Mobile ID:** Perfis com GAID e/ou IDFA são ativados usando suas respectivas IDs de publicidade. Se um perfil contiver GAID e IDFA, cada ID será ativada separadamente.
* **Perfil baseado em cookies:** Um perfil com ECID e um mapeamento [!DNL Trade Desk ID] correspondente será ativado usando a Trade Desk ID para direcionamento baseado em cookies.
* **Perfil somente ECID:** Um perfil com apenas ECID e nenhum mapeamento [!DNL Trade Desk ID] **não será exportado**. A ECID sozinha é insuficiente para ativação.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL The Trade Desk], verifique sua conta [!DNL The Trade Desk]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

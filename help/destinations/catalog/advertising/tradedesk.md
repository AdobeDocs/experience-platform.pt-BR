---
keywords: publicidade; a trade desk; advertising trade desk
title: A conexão com a Trade Desk
description: A Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais de redirecionamento e direcionadas por público-alvo em origens de inventário de exibição, vídeo e dispositivos móveis.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 4472548fc5b5181cdf8ef8b1666d6e1fafbce588
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 2%

---

# [!DNL The Trade Desk] conexão

## Visão geral {#overview}


>[!IMPORTANT]
>
> Após a [atualização interna](../../../release-notes/2025/july-2025.md#destinations) para o serviço de destinos a partir de julho de 2025, você pode observar uma **queda no número de perfis ativados** em seus fluxos de dados para [!DNL The Trade Desk].
> Essa queda é causada pela melhor visibilidade do monitoramento. Perfis sem ECID agora são contados corretamente como descartados nas métricas de ativação. Consulte a seção [mapeamento obrigatório](#mandatory-mappings) nesta página para obter informações detalhadas.
>
>**O que mudou:**
>
>* O serviço de destinos agora relata corretamente quando perfis sem ECID são descartados da ativação.
>* **Importante:** Perfis sem ECID nunca chegaram a [!DNL The Trade Desk] mesmo antes desta atualização. A integração sempre exigiu a ECID. Essa atualização corrige um erro que anteriormente impedia que essas quedas ficassem visíveis em suas métricas.
>
>**O que é necessário fazer:**
>
>* Analise seus dados de público-alvo para confirmar se os perfis têm valores ECID válidos.
>* Monitore suas métricas de ativação para verificar as contagens esperadas de perfis. As contagens mais baixas refletem relatórios precisos, não uma alteração no comportamento de destino.

Use este conector de destino para enviar dados de perfil para [!DNL The Trade Desk]. Este conector envia dados para o ponto de extremidade primário [!DNL The Trade Desk]. A integração entre o Adobe Experience Platform e o [!DNL The Trade Desk] não oferece suporte à exportação de dados para o ponto de extremidade de terceiros [!DNL The Trade Desk].

O [!DNL The Trade Desk] é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais com direcionamento de público e redirecionamento em fontes de inventário para dispositivos móveis, vídeo e exibição.

Para enviar dados de perfil para [!DNL The Trade Desk], primeiro você deve se conectar ao destino, conforme descrito nas seções a seguir desta página.

## Casos de uso {#use-cases}

Como profissional de marketing, quero poder usar públicos-alvo criados a partir do [!DNL Trade Desk IDs] ou de IDs de dispositivo para criar campanhas digitais de redirecionamento ou direcionadas por público-alvo.

## Identidades suportadas {#supported-identities}

O [!DNL The Trade Desk] dá suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

Abaixo estão as identidades suportadas pelo destino [!DNL The Trade Desk]. Essas identidades podem ser usadas para ativar públicos para [!DNL The Trade Desk].

Todas as identidades na tabela abaixo são mapeamentos obrigatórios.

| Identidade do público alvo | Descrição | Considerações |
|---|---|---|
| [!DNL GAID] | GOOGLE ADVERTISING ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| [!DNL IDFA] | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| [!DNL ECID] | Experience Cloud ID | Essa identidade é obrigatória para que a integração funcione corretamente, mas não é usada para ativação de público-alvo. |
| [!DNL Tradedesk] | [!DNL TDID] na plataforma [!DNL The Trade Desk] | Use essa identidade ao ativar públicos com base na ID proprietária da Trade Desk. |

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

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o [!DNL The Trade Desk] e não habilitou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/pt-br/docs/id-service/using/id-service-api/methods/idsync) no Serviço da Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para habilitar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do [!DNL The Trade Desk] no Audience Manager, as sincronizações de ID configuradas serão transferidas para o Experience Platform.

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

### Mapeamentos obrigatórios {#mandatory-mappings}

Todas as identidades de destino descritas na seção [identidades com suporte](#supported-identities) devem ser mapeadas na etapa de mapeamento do fluxo de trabalho de ativação de público. Isso inclui:

* [!DNL GAID] (Google Advertising ID)
* [!DNL IDFA] (Apple ID para anunciantes)
* [!DNL ECID] (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Captura de tela mostrando os mapeamentos obrigatórios](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

O mapeamento de todas as identidades de destino garante que a ativação possa dividir e entregar perfis corretamente usando qualquer identidade presente. Isso não significa que todas as identidades devem estar presentes em cada perfil.

Para que a exportação para a Trade Desk tenha êxito, um perfil deve conter:

* [!DNL ECID] e
* pelo menos um de: [!DNL GAID], [!DNL IDFA] ou [!DNL The Trade Desk ID]

Exemplos:

* Somente [!DNL ECID]: não exportado
* [!DNL ECID] + [!DNL The Trade Desk ID]: exportado
* [!DNL ECID] + [!DNL IDFA]: exportado
* [!DNL ECID] + [!DNL GAID]: exportado
* [!DNL IDFA] + [!DNL The Trade Desk ID] (sem [!DNL ECID]): não exportado

>[!NOTE]
> 
>Após a atualização [de julho de 2025](/help/release-notes/2025/july-2025.md#destinations) para o serviço de destinos, os perfis com [!DNL ECID] ausente agora são relatados corretamente como descartados nas métricas de ativação. Esse sempre foi o comportamento da integração - perfis sem [!DNL ECID] nunca chegaram a [!DNL The Trade Desk] - mas as quedas agora estão adequadamente visíveis no monitoramento do fluxo de dados. As contagens de ativação mais baixas refletem relatórios precisos, não uma alteração na funcionalidade de destino.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL The Trade Desk], verifique sua conta [!DNL The Trade Desk]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.
